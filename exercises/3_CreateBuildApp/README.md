# In this exercise, you will build your app in SAP Build Apps to upload invoice.

## Table of Contents

- [Create a new app project ](#project)
- [Create the sales order page](#process)
- [Enable SAP BTP authentication](#data)
- [Create data resource to SAP Build Process Automation](#aprrovalform)
- [Test the trigger](#appnotification)
- [Create data variable](#rejnotification)
- [Bind data variable to UI elements](#processcondition)
- [Add logic to trigger workflow](#autoapproval)
- [Run app](#save)

# Overview <a name="project"></a>

In this exercise, you will build your app in SAP Build Apps to upload invoices.

![Image](images/1000.png)

## Create a new app project <a name="project"></a>

1. From [SAP Build Lobby](https://da160-96ork4sc-applicationdevelopment.lcnc.cfapps.eu10.hana.ondemand.com/lobby), Go to the SAP Build lobby, and click on <b>Create</b>.<br>

<br> 

![Image](images/100.png)

2. Select <b>Build an Application.</b>
   <br><br>
    ![Image](images/200.png)

3. Select <b>Web & Mobile Application.</b>
   <br><br>  
   ![Image](images/300.png)

4. For the project name, enter <i>Sales Order Trigger</i> then click <b> Create.</b>
   <br><br>
    ![Image](images/400.png)

## Create the sales order page <a name="process"></a>

1. By default your new application contains a page with title and text fields. In this step, you will focus on turning this page into your app, including how to build a UI and stylize the UI elements. <br><br>![home page]

2. Select the text field, and click the <b> X </b> to delete it. <br><br>![Title component](images/500.png)

3. Click on an open area, and in the <b>Properties</b> tab, change the <b>Page Name</b> to <i>Create Sales Order.</i><br><br> ![Image](images/600.png)

4. Select the <b> Style </b> tab. <br><br>![input component](images/700.png)

5. Click the <b> Background Color </b> (App Background), and then select New Palette.<br><br>![input properties]![Image](images/800.png)

6. For the color, enter _#F3D6A0_, name the color _SAP Orange Light_, and click <b> Save.</b>

7. Click the title field, and in the <b>Properties</b> tab change the <b>Content </b> text to _Sales Order Workflow_.<br><br>
   ![Image](images/900.png)

8. To the canvas, drag a Container component. With the container selected, in the <b> Properties </b> tab under Advanced Properties, change the <b> Component display name </b> to _Form_.

   ![Image](images/1100.png) <br>
   Still with the container selected, open the <b> Style </b> tab, and click <b> Edit </b> for the Layout Container. <br> ![Image](images/1200.png)
   For the background color, select **Level 4 background.** <br>
   For padding, set the padding on all 4 sides to 16px by going to **Theme** and selecting the **L** size. <br> ![Image](images/1300.png) <br>
   For **Effects**, create a shadow by setting these properties: <br>
   **Enable Shadow** : True <br>
   **Shadow**: Content Shadow 0 <br>
   **Color** : Any static color you like (I chose #8e8989) <br>
   Let’s save the style by scrolling up, clicking <b>New Style,</b> entering Layout _Form Container_, and clicking <b> OK.</b>

9. Inside the outer container, add another container, and inside that container add a text and input field. The result should look like this: <br><br>
   ![Image](images/1400.png) <br><br>
   For the inner container, go to **Layout** tab, and under **Layout** set the container to **Horizontal**. Then, set **Align components** to middle. <br>
   ![Image](images/1500.png) <br>
   For the text field, go to **Layout** tab and set the width to exactly 75px.<br>
   ![Image](images/1600.png)<br>
   For the input field, delete _Label_ from the **Label** property. <br><br>

10. From the Tree view, copy the inside container and paste it inside the outer ( Form ) container until you have 4 fields..<br>
    ![Image](images/1700.png)<br>
    <b>Fields </b> <br>
    Ship To Party <br>
    Material <br>
    Order Amount <br>
    Delivery Date<br>
    ![Image](images/1800.png)

11. At the bottom of the page (outside the outside container), add a button. In the **Properties** tab, set the **Label** to _Get Approval_. <br><br>
    ![Image](images/1900.png)

## Enable SAP BTP authentication <a name="data"></a>

You need to enable SAP BTP authentication since you want to use SAP BTP destinations.

1.  Go to the <b>Auth</b> tab.<br>

2.  Click Enable <b>Authentication</b>.<br>
    ![Image](images/2000.png)

3.  Select <b> SAP BTP Authentication.</b> On the confirmation popup, click <b>OK</b>.<br>

## Create data resource to SAP Build Process Automation <a name="approvalform"></a>

As part of setting up SAP Build Process Automation, you created a destination so you can make calls to the SAP Build Process Automation APIs, including the one that lets you trigger a workflow.
<br><br>
Now you will set up the connection from your app to SAP Build Process Automation on your tenant, using that destination. <br><br>
<br>

1.  Open the **Data** tab, at the top of the page <br><br>
2.  Scroll down, and click <b>Create Data Entity > SAP BTP Destination REST API Integration</b>.<br>
    The configuration screen appears, starting with the **Base** panel. <br>
    ![Image](images/2100.png)

3.  On the Base panel, enter the following:<br><br>
<table>
  <tr>
    <th>Field</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>Data resource name</td>
    <td><i>Trigger Workflow</i></td>
  </tr>
  <tr>
    <td>BTP destination name</td>
    <td><i>sap-process-destination (or the destination you created, if you created your own)</i> </td>
  </tr>
  </table> <br>

![Image](images/2200.png)

<br><br>
Under <b>Resource schema</b>, click Add New and add a field of type <i>Object</i> and with the name **salesorderdetails** .<br><br>
Click on the new field, and add the following sub-fields to the object: <br>

![Image](images/2300.png)
<br>
<b>IMPORTANT:</b> Click on the <b> Add New </b> button BELOW the salesorderdetails field. <br><br>

<table>
  <tr>
    <th>Field Name</th>
    <th>Type</th>
  </tr>
  <tr>
    <td>ShipToPartyl</td>
    <td>Text</td>
  </tr>
  <tr>
    <td>Material</td>
    <td>Text</td>
  </tr>
  <tr>
    <td>OrderAmount</td>
    <td>Number</td>
  </tr>
  <tr>
    <td>ExpectedDeliveryDate</td>
    <td>Text</td>
  </tr>
  <tr>
    <td>Division</td>
    <td>Text</td>
  </tr>
  <tr>
    <td>SalesOrderType</td>
    <td>Text</td>
  </tr>
  <tr>
    <td>ShippingCountry</td>
    <td>Text</td>
  </tr>
  <tr>
    <td>SalesOrganisation</td>
    <td>Text</td>
  </tr>
  <tr>
    <td>DistributionChannel</td>
    <td>Text</td>
  </tr>

</table>

4.  Click the **create** panel.<br>
    Then enable the create action with the toggle button.<br><br>
    ![Image](images/2400.png) <br>
    ![Image](images/2500.png) <br>

5.  For **Request headers**, click the binding **X**, then **List of values**.<br>

Click **Add a value**, and add the following key-value pair:<br>

<table>
  <tr>
    <th>Field Name</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>Header name</td>
    <td>Content-Type</td>
  </tr>
  <tr>
    <td>Header value</td>
    <td>application/json</td>
  </tr>
  </table>
        ![](images/32.png)
        Click <b>Save.</b>

6.  For <b>Request body mapper,</b> click the binding <b> X</b>, then <b>Formula > Create formula.</b><br>
    Enter the following for the formula – replace <your definition ID> with the ID for your process:<br><br>
    " ENCODE_JSON({ "definitionId": "<your definition ID>", "context": query.record })" <br><br>
    Click <b>Save </b>twice.

        ![](images/33.png)

7.  Click **Save Data Resource** (bottom right). <br>
    Click Save (in the upper right to save all your changes to the project).<br>
    ![](images/34.png)

## Test the trigger <a name="appnotification"></a>

1. Open the data resource again by clicking it.<br>
   ![Images](images/2600.png)

2. Click **create** on the left, and then the **Test tab**..<br>

3. Enter values for the fields (really, you only need to enter an order amount), and then scroll down and click **Run Test**. <br>
   ![Images](images/2700.png)

**IMPORTANT**: Date fields must be in the format of 2022-12-25 and the order amount must be a number.<br><br>
If all works **OK**, you will get a **201** status code and a response with information about the process instance you just triggered, something like this: <br><br>
Javascript: <br><br>
{
"id": "54988e48-8056-11ed-9a13-eeee0a99244a", <br>
"definitionId": "us10.my-account.salesorderapprovals.orderProcessing", <br>
"definitionVersion": "6",<br>
"subject": "Order Processing",<br>
"status": "RUNNING",<br>
"businessKey": "54988e48-8056-11ed-9a13-eeee0a99244a",<br>
"parentInstanceId": null,<br>
"rootInstanceId": "11118e48-8056-11ed-9a13-eeee0a99244a", <br>
"applicationScope": "own",<br>
"projectId": "us10.my-account.salesorderapprovals",<br>
"projectVersion": "1.0.5",<br>
"startedAt": "2022-12-20T11:06:19.318Z", <br>
"startedBy": "sb-clone-41c25609-33a1-9999-97d8-34fcd2316008!b3591|workflow!b116",<br>
"completedAt": null<br>
}<br>
![Images](images/2800.png) <br>

If you’ve gotten to here, your integration with SAP Build Process Automation is working!!<br>
You can go into the SAP Build Process Automation monitoring and see there the process you just triggered, and check the context to make sure the parameters were sent properly. <br>
![Images](images/2900.png)<br>
You can also check the Inbox to see the forms were created and the values properly passed into the workflow.<br>
![Images](images/3000.png)<br>

## Create data variable <a name="rejnotification"></a>

1. Back on the UI canvas, select **Variables**.<br>

2. On the left, click **Data Variables**.<br>

3. Click **Add Data Variable**, and choose **Trigger Workflow** as the data resource on which to base the data variable. <br>
   ![Image](images/3001.png)

4. On the right, choose **New data record**.<br>
   ![Image](images/3002.png)

5. Click **Save** (upper right).<br>

## Bind data variable to UI elements <a name="processcondition"></a>

1. Go back to **View** so you can see the UI canvas.<br>

2. Click on the first input field (for **Customer**).
   In the Properties tab, click the **X** next to the **Value** field, and select **Data and Variables > Data Variables > Trigger Workflow1 > shipToParty**.<br>
   ![Image](images/3003.png)

3. Click **Save**<br><br>

4. Click on the second input field (for **Material**). <br>
   In the Properties tab, click the **X** next to the Value field, and select **Data and Variables > Data Variables > Trigger Workflow1 > material.** <br>
   Click **Save**<br><br>

5. Click on the third input field (for **Amount**). <br>
   In the Properties tab, click the **X** next to the Value field, and select D**ata and Variables > Data Variables > Trigger Workflow1 > orderAmount.** <br>
   Click **Save**<br><br>

6. Click on the fourth input field (for **Delivery Date**).
   In the **Properties** tab, click the **X** next to the Value field, and select **Data and Variables > Data Variables > Trigger Workflow1 > expectedDeliveryDate.**
   Click **Save**<br><br>

7. Click **Save** (upper right).

## Add logic to trigger workflow <a name="autoapproval"></a>

1. Click on the **Get Approval** button, and open the logic canvas by clicking **Add logic to Button1** at the bottom right.<br>
   ![Image](images/3004.png)<br>

2. Drag a **Create record** flow function onto the canvas, and connect the component tap event to it.<br> ![Image](images/3005.png)<br>

3. Click on the **Create record** flow function and configure it in the **Properties** pane on the right.
   <br>
   For **Resource name**, this should already be set to **Trigger Workflow**, since you have only one data resource.<br> ![Image](images/3006.png) <br>
   For **Record** , you have to bind each of the data variable fields to the appropriate record field. <br>
   There are many ways to do binding. For **Properties** , you will use a formula. Click on the object binding button: <br> ![Image](images/3008.png) <br>
   Click **Formula** , then click on the existing formula, and replace it with the following: <br>
   Javascript: <br>
   {salesorderdetails: {division: "1010", orderAmount: NUMBER(data["Trigger Workflow1"].salesorderdetails.orderAmount), shipToParty: data["Trigger Workflow1"].salesorderdetails.shipToParty, salesOrderType: "OR", shippingCountry: "Barbados", salesOrganisation: "10", distributionChannel: "1000", expectedDeliveryDate: data["Trigger Workflow1"].salesorderdetails.expectedDeliveryDate, material: data["Trigger Workflow1"].salesorderdetails.material}}
   <br>

4. Click **Save**.<br>

5. Drag a **Toast** flow function onto the canvas, and connect the **top** output of the Create record flow function to it. <br> ![Image](images/3007.png)<br>

6. Click on the **Toast** flow function and configure it in the **Properties** pane on the right. <br>
   For **Toast message**, click on the **ABC**, and then select **Formula > Formula**. <br>
   Erase the quotation marks, and enter the following formula: <br>
   "Triggered process with ID: " + outputs["Create record"].response.id <br>
   Click **Save**.
   <br><br>

7. Click **Save** (upper right).

## Run App <a name="save"></a>

1. Click the **Launch** tab, and then **Open Preview Portal**. <br>
   ![Image](images/3009.png) <br>
2. Click **Open web preview** (left). <br>

3. Select your project, **Select Order Trigger**.<br> ![Image](images/3010.png) <br>
4. Enter the following values in your form: <br>
<table>
  <tr>
    <th>Field Name</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>Customer</td>
    <td>Joe's Bikes</td>
  </tr>
  <tr>
    <td>Material</td>
    <td>HT-1000</td>
  </tr>
  <tr>
    <td>Amount</td>
    <td>1000</td>
  </tr>
  <tr>
    <td>Delivery Date</td>
    <td>2023-03-31</td>
  </tr>
  </table> <br>
5. Click Get Approval. <br>
   You process should be triggered and require approval (since the amount is 1000 or above). <br>
   You should see the toast message indicating the workflow was triggered, and with the process instance ID. <br>

   ![Image](images/3011.png)
   You can also see the results of the call in SAP Build Process Automation. <br>
   Go to the Monitor tab, then Process and Workflow Instances. The first one should be the one you just triggered.<br>
   You can see the new process instance.<br>
   You can see the context, which is the values sent with the API. <br>
   You can also see the execution log, which in this case ran the auto-approve task because the amount was below 100000.<br>
   The context field in yellow are the ones that you entered via the UI.<br> ![Image](images/3012.png)
   You can also see that the process instance ID is the same: in the toast message and in the upper right of the Monitor tab.

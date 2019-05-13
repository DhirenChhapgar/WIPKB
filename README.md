[![Project Status](http://opensource.box.com/badges/active.svg)](http://opensource.box.com/badges)

Amazon Marketplace Integration
==================================
This integration supports Fulfillment by Amazon (FBA) and Fulfillment by Merchant (FBM) fulfillment channels. Using this integration user can import orders placed on Amazon Marketplace into Acumatica and can transfer order fulfillment details from Acumatica to Amazon Marketplace for FBM type of orders.

This integration doesn’t include 
* Return and refund of orders.
* Inventory/Stock, Products and Customers synchronize between Acumatica and Amazon Marketplace.
* Settlement/reconcile Amazon FBA, advertisement Fees etc.

### Prerequisites
* Acumatica 2018 R2 (18.204.0013+) or higher
* Inventory/Stock, Products and Customers has to be setup prior using this integration.
* This integration requires “Amazon Seller Professional Account” credentials for configuring integrations. Please visit (https://developer.amazonservices.com/) for more information on getting MWS Credentials.

Quick Start
-----------

### Installation

##### Install customization deployment package
1. Download PXAmazonIntegrationPkg.zip from this repository
2. In your Acumatica ERP instance, navigate to System -> Customization -> Customization Projects (SM204505), import PXAmazonIntegrationPkg.zip as a customization project
3. Publish customization project.

### Configuration

#### Sales Order Preferences

1. Navigate to Sales Order Preferences (SO101000) Distribution-> Sales Orders -> Configuration -> Sales Order Preferences -> Amazon Configuration Tab
2. Specify default configuration settings which will be applied to imported Amazon orders and these settings are common for both FBA and FBM type of orders

![Screenshot](/_ReadMeImages/IN207000.png)

##### Configuration Settings Summary

 | Element               | Description |
 | :---                  | :--- |
 | **Guest Customer ID** | All imported Amazon orders will be associated to this configured Guest customer.  |
 | **Tax Zone ID**       | This Tax ID will be default Tax ID to all imported Amazon orders. The details will be shown in Sales Order form’s Tax details tab. <ul><li>Only taxes which are created with the option “Propagate Manually Set Tax Amount from Sales Orders to Invoice” can be selected as default Tax ID</ul></li> |
 | **Payment Method ID** | This Payment Method will be applied to all imported Amazon orders. The details will be shown in Sales Order form’s Payments tab. |
 | **Ship Via**          | This Ship Via method will be applied to all imported Amazon orders. The details will be shown in Sales Order form’s Shipping settings tab. |
 | **Initial From Date** | Cut-off date after which orders will be available for sync in Schedule import orders screen. Assume that you have configured the date “1st Jan 2019”, then system will fetch amazon orders which are placed from 1st January 2019. |
 
#### Marketplace Configuration

Marketplace Configuration Screen is used to control various features of the Integration. The configuration settings will include following fields information.

![Screenshot](/_ReadMeImages/IN207000.png)

##### Marketplace Configuration Summary

| Element               | Description |
| :---                  | :--- |
| **Integration ID** | You can set a unique value that can be used to identify all the configuration details in other screens related to this integration ID. |
| **Status** | This field is used to mark a specific Integration as Active / Inactive. If the integration is marked as Inactive, then system will not display the details/logs related to this specific integration. |
| **Integration Type** | Depending on the selection of the Integration type, respective Marketplace ID will be used for the API calls to fetch the Orders / Data related to that respective Marketplace, example Marketplace ID will be “XXXXXXXXXXXXX” for Amazon FBA (US). The list of values for this field is provided below: <ul><li>Amazon FBA</li><li>Amazon.ca FBA</li><li>Amazon.co.uk FBA</li><li>Amazon.de FBA</li><li>Amazon.jp FBA</li><li>Amazon.in FBA</li><li>Amazon FBM</li></ul> |
| **Warehouse** | All active warehouses will be loaded from the system to select specific warehouse in Acumatica for order processing. All the imported orders under this specific integration will be associated to this configured warehouse by default. |
| **Order Type** | All the active order types will be loaded from the system to select specific Order type. Based on the selected integration type these order type template will be loaded for selection. <ul><li>For FBA integrations types the system will display the “IN – Invoice” type templates for the selection, whereas for FBM Integration type it will display “SO – Sales Order” template order types.</li></ul> |
| **Seller ID** | This field is used to configure the Amazon Marketplace Seller ID. |
| **Auth Token** | This field is used to configure the Auth Token of the respective Seller. This field is encrypted and cannot see the provided data in this field. |
| **Access Key** | This field is used to configure the Access Key of the respective Seller. This field is encrypted and cannot see the provided data in this field. |
| **Secret Key** | This field is used to configure the Secret Key of the respective Seller. This field is encrypted and cannot see the provided data in this field. |
| **Marketplace ID** | This field is used to configure the Marketplace ID of the respective Seller. Each integration type will have its own Marketplace ID. |
| **Description** | This field is used to add the custom description about the Integration. |
| **Test Connection** | This button is used to validate the provided credentials and shows the result whether given configuration details are correct or not for orders syncing. If the provided credentials are incorrect then the system will show an error message. |
| **Field Mapping Configuration** | This grid is used to make the field mappings for importing the Amazon order values into required target fields of Acumatica Sales Order. Ex: We can map the configuration, “Amazon Order ID” to be displayed as Sales Order’s Customer Order number. "Marketplace Configuration.xlsx" can be used to setup mapping.|

#### Amazon Tax Configuration
Amazon Tax Amount will be brought into Acumatica at the time of order sync (FBA & FBM). To match the order Taxes and Totals on both systems.
Following are the list of steps that need to be followed to enable manual taxes in Acumatica:

* Navigate to Tax Categories screen (TX205500) and create new tax category "AMAZONTC"
![Screenshot](/_ReadMeImages/PO302000Allocation.png)

* Navigate to Tax Zones screen (TX206000) and create new Tax Zone ID "AMAZONTZ" add assign default tax category created in prior step.
![Screenshot](/_ReadMeImages/PO302000Allocation.png)

* Navigate to Taxes Screen (TX205000) and create new Tax ID "AMAZONTAX" and assign an unlimited Tax Schedule. Make sure to check “Propagate Manually Set Tax….” check box.
![Screenshot](/_ReadMeImages/PO302000Allocation.png)

* In Taxes screen, select Tax Category "AMAZONTC" created in prior step.
![Screenshot](/_ReadMeImages/PO302000Allocation.png)

### Usage

#### Import Orders
This screen (SO509100) is used to sync the Amazon orders from Amazon Marketplace. All the orders will be displayed based on the mapped configuration and given input parameters.

![Screenshot](/_ReadMeImages/PO302000Allocation.png)

With the help of this screen, import/export of the orders can be done from any configured Amazon Marketplace. Once the order is imported, you can view the order details from Sales Order screen under configured order type. You can also modify any details of the order once it is imported to Acumatica, but these modifications will not have any impacts at Amazon Marketplace side.

| Element               | Description |
| :---                  | :--- |
| **From Date** | Start date can be selected, from which date the orders should be pulled for importing into Acumatica. |
| **To Date** | End date can be selected, till what date the orders should be pulled for importing into Acumatica. <ul><li>The Amazon orders will be retrieved by clicking on the prepare button for the period between the selected "From" and "To" Dates.</li><ul> |
| **Integration ID** | This field will display the list of all active Marketplace Configurations. With the help of this field, you can select from which seller account orders required to be prepared and imported. Both FBA and FBM type of orders can be processed with this field. |
| **Process All Integrations** | This option is used to retrieve the orders from all active marketplace configurations at once. |
| **Records Grid** | After providing the required input parameters at header sections, such as giving the required period and selecting the required integration ID, the pulled records can be viewed by using this grid. |
| **Prepare** | This button is used to retrieve the Amazon orders for the given period and under selected Integration ID. We can perform this action for any number of times and each time it will fetch new records if any new orders are created under the given period. After successful prepare operation, the system will display all the fetched Amazon orders under results grid which will be ready for importing into Acumatica. |
| **Import** | This button is used to import the fetched Amazon orders into Acumatica. Only the selected orders will be imported into the system. Once an order is imported, then the same order will no longer available for importing again. During this import process, all the successful imports and failed to sync the records due to various reasons details will be maintained in separate GI log screens. |
| **Import All** | Import button is used to import only the selected Amazon orders, whereas this "Import All" button is used to import all the available orders into Acumatica at once. One doesn’t have to select any specific order for processing all the records, by clicking on the "Import All" button the system will automatically selects all the available orders from the results grid and processes for importing. Start date can be selected, from which date the orders should be pulled for importing into Acumatica. |

#### Schedule Import Orders

With the help of this screen (SO509200), one can schedule “Prepare and Import” of orders from the last sync date to required date. We can also schedule prepare and import process of all the active integrations at a time.

![Screenshot](/_ReadMeImages/PO302000Allocation.png)

This screen is similar to Import Orders screen and the difference is that both Prepare and Import operations can be performed at once whereas these actions can be performed individually in Import Orders screen (SO509100).

| Element               | Description |
| :---                  | :--- |
| **From Date** | Start date can be selected, from which date the orders should be pulled for importing into Acumatica. |
| **To Date** | End date can be selected, till what date the orders should be pulled for importing into Acumatica. <ul><li>The Amazon orders will be retrieved by clicking on the prepare button for the period between the selected "From" and "To" Dates.</li><ul> |
| **Integration ID** | This field will display the list of all active Marketplace Configurations. With the help of this field, you can select from which seller account orders required to be prepared and imported. Both FBA and FBM type of orders can be processed with this field. |
| **Process All Integrations** | The above Integration ID field is used to retrieve the orders from one marketplace integration at a time, whereas this “Process All Integrations” option is used to retrieve the orders from all active marketplace configurations at once. |
| **Records Grid** | After providing the required input parameters at header sections, such as giving the required period and selecting the required integration ID, the pulled records can be viewed by using this grid. |
| **Prepare & Import	** | This button is used to import (no prepare and import separate actions required) all the Amazon orders into Acumatica for the displayed period and under selected Integration ID(s). After successful operation, the user can check all the imported orders in Sales order screen. All the GI log screens will be updated accordingly. <ul><li>Once the operation completed, the respective scheduled rows will be disappeared from this screen.</li><li>For each schedule, the system will assign one process ID automatically and the user can check all the details in GI log screens with this process ID.</li><ul> |


#### Import FBA Tracking #

#### Submit FBM Shipment Info


Known Issues
------------
None at the moment

## Copyright and License

Copyright © `2019` `Acumatica`

This component is licensed under the MIT License, a copy of which is available online [here](LICENSE.md)

[![Project Status](http://opensource.box.com/badges/active.svg)](http://opensource.box.com/badges)

Amazon Marketplace Integration
==================================
Using this integration user can import orders placed on Amazon Marketplace into Acumatica. Also, user can transfer order fulfillment details from Acumatica to Amazon Marketplace for FBM type of orders. Integration supports Fulfillment by Amazon (FBA) and Fulfillment by Merchant (FBM).

This integration doesn’t include any return and refund of the orders.

### Prerequisites
* Acumatica 2018 R2 (18.204.0013+) or higher
* Inventory, Stock Items and Customers has to be setup prior using this integration. And this integration doesn’t include Inventory, Products and Customers synchronize between Acumatica and Amazon Marketplace.
* Please make sure to have the Marketplace configurations created before the sync process initiated.
* Ensure to have the Tax configuration done before the sync process initiated.
* This integration requires the “Amazon Seller Professional Account” credentials for configuring the integrations. Please visit (https://developer.amazonservices.com/) for more information on getting MWS Credentials.

Quick Start
-----------

### Installation

##### Install customization deployment package
1. Download PXAmazonIntegrationPkg.zip from this repository
2. In your Acumatica ERP instance, navigate to System -> Customization -> Customization Projects (SM204505), import PXAmazonIntegrationPkg.zip as a customization project
3. Publish customization project.

### Configuration

#### Sales Order Preferences

1. The first configuration step is Sales Order Preferences and we can use this tab to select the default configuration settings which will be applied to the imported Amazon orders and these settings are common for both FBA and FBM type of orders
2. Navigate to Sales Order Preferences (SO101000) Distribution-> Sales Orders -> Configuration -> Sales Order Preferences -> Amazon Configuration Tab

![Screenshot](/_ReadMeImages/IN207000.png)

##### Configuration Settings Summary

 | Element               | Description |
 | :---                  | :--- |
 | **Guest Customer ID** | All the imported Amazon orders will be associated to this configured Guest customer.  |
 | **Tax Zone ID**       | This Tax ID will be default Tax ID to all the imported Amazon orders. The details will be shown in Sales Order form’s Tax details tab. <ul><li>Only taxes which are created with the option “Propagate Manually Set Tax Amount from Sales Orders to Invoice” can be selected as default Tax ID</ul></li> |
 | **Payment Method ID** | This Payment Method will be applied to all the imported Amazon orders. The details will be shown in Sales Order form’s Payments tab. |
 | **Ship Via**          | This Ship Via method will be applied to all the imported Amazon orders. The details will be shown in Sales Order form’s Shipping settings tab. Admin can change the Ship Via method if requires but this will not impact anything at Amazon side. |
 | **Initial From Date** | This field is used to set, after which date of orders the system should consider and available for sync in Schedule import orders screen. Assume that you have configured the date “1st Jan 2019”, then the system will display the amazon orders which are placed from 1st January 2019 only. A note is provided for this field as “Baseline Date beyond which Orders will be synced from Amazon into Acumatica. Please note that Initial From Date field cannot be changed as soon as an order is imported into Acumatica”. |
 
#### Marketplace Configuration

Marketplace Configuration Screen is used to control various features of the Integration. The configuration settings will include the following fields information. Please refer to the below screenshot.

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

#### Schedule Import Orders

#### Import FBA Tracking #

#### Submit FBM Shipment Info


Known Issues
------------
None at the moment

## Copyright and License

Copyright © `2019` `Acumatica`

This component is licensed under the MIT License, a copy of which is available online [here](LICENSE.md)

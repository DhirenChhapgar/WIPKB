[![Project Status](http://opensource.box.com/badges/active.svg)](http://opensource.box.com/badges)

Amazon Marketplace Integration
==================================
Using this integration user can import order details which are placed in Amazon Marketplace into Acumatica. Also, user can transfer order fulfillment details from Acumatica to Amazon Marketplace for FBM type of orders. With this approach, the sync will continuously runs between Acumatica and Amazon Marketplace for exchanging the data between two systems.

* FBA integrations assume that all orders are placed on Amazon, and will be fulfilled by Amazon.
* FBM orders will have sales originated on Amazon Marketplace, and merchant will fulfill the orders from their warehouse.

This integration doesn’t include the return and refund of the orders.

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
| **Tax Zone ID**       | This Tax ID will be default Tax ID to all the imported Amazon orders. The details will be shown in Sales Order form’s Tax details tab. Only taxes which are created with the option “Propagate Manually Set Tax Amount from Sales Orders to Invoice” can be selected as default Tax ID |
| **Payment Method ID** | This Payment Method will be applied to all the imported Amazon orders. The details will be shown in Sales Order form’s Payments tab. |
| **Ship Via**          | This Ship Via method will be applied to all the imported Amazon orders. The details will be shown in Sales Order form’s Shipping settings tab. Admin can change the Ship Via method if requires but this will not impact anything at Amazon side. |
| **Initial From Date** | This field is used to set, after which date of orders the system should consider and available for sync in Schedule import orders screen. Assume that you have configured the date “1st Jan 2019”, then the system will display the amazon orders which are placed from 1st January 2019 only. A note is provided for this field as “Baseline Date beyond which Orders will be synced from Amazon into Acumatica. Please note that Initial From Date field cannot be changed as soon as an order is imported into Acumatica”. |
 
#### Marketplace Configuration

Marketplace Configuration Screen is used to control various features of the Integration. The configuration settings will include the following fields information. Please refer to the below screenshot.
![Screenshot](/_ReadMeImages/IN207000.png)

##### Marketplace Configuration Summary

| Element               | Description |
| :---                  | :--- |
| **Integration ID** | You can set a unique value that can be used to identify all the configuration details in other screens related to this integration ID.  |
| **Status** | This field is used to mark a specific Integration as Active / Inactive. If the integration is marked as Inactive, then system will not display the details/logs related to this specific integration.  |
| **Integration Type** | Depending on the selection of the Integration type, respective Marketplace ID will be used for the API calls to fetch the Orders / Data related to that respective Marketplace, example Marketplace ID will be “XXXXXXXXXXXXX” for Amazon FBA (US). The list of values for this field is provided below: <ul><li>item1</li><li>item2</li></ul> |
| **Integration ID** | You can set a unique value that can be used to identify all the configuration details in other screens related to this integration ID.  |
| **Integration ID** | You can set a unique value that can be used to identify all the configuration details in other screens related to this integration ID.  |
| **Integration ID** | You can set a unique value that can be used to identify all the configuration details in other screens related to this integration ID.  |
| **Integration ID** | You can set a unique value that can be used to identify all the configuration details in other screens related to this integration ID.  |


3. Navigate to Stock Item Screen (IN202500) and create a new Stock Item having Lot/Serial class created in Step # 2.
4. Create Purchase Order (PO301000) for Stock Item created in Step # 3. And move forward with creating Purchase Receipt (PO302000) for this Purchase Order.
5. Click on Allocations button, you should be able to see Attributes specified in Step # 2 and can specify value for them.
![Screenshot](/_ReadMeImages/PO302000Allocation.png)

6. **Apply Attribute from First** button copies attribute values specified for very first Lot/Serial Number and applies to rest of the Lot/Serial Number displayed in the dialog. One can specify value for each individual Lot/Serial Number as well.
7. Attribute value can be assigned for Lot/Serial Number while receiving inventory via IN Receipt Screen (IN301000) similarly via Allocations dialog.
8. Attribute values and image can be assigned to Lot/Serial Number/s via custom **Item Lot/Serial # Info** screen (IN202501) as well.
![Screenshot](/_ReadMeImages/IN202501.png)

9. Attribute values can be imported via **Import Lot/Serial Attributes** custom import scenario available via customization package.
![Screenshot](/_ReadMeImages/SM206025.png)
![Screenshot](/_ReadMeImages/SM206036.png)

10. **Item Lot/Serial Search** option can be utilized to search Lot/Serial Number by attribute value and allocate in Sales Order Entry screen (SO301000). Columns for Attribute/s will be dynamically added/removed based on specified Lot/Serial class value.
![Screenshot](/_ReadMeImages/SO301000-1.png)
![Screenshot](/_ReadMeImages/SO301000-2.png)

Known Issues
------------
None at the moment

## Copyright and License

Copyright © `2018` `Acumatica`

This component is licensed under the MIT License, a copy of which is available online [here](LICENSE.md)

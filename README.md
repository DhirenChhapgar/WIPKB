[![Project Status](http://opensource.box.com/badges/active.svg)](http://opensource.box.com/badges)

Adding Attribute Support to out-of-box Lot/Serial Number
==================================
An extension that allows to add attribute support to out-of-box Lot/Serial Number.

### Prerequisites
* Acumatica 6.1 or higher

Quick Start
-----------

### Installation

##### Install the customization deployment package
1. Download PXLotSertialNbrAttributeExtPkg.zip from this repository
2. In your Acumatica ERP instance, navigate to System -> Customization -> Customization Projects (SM204505), import PXLotSertialNbrAttributeExtPkg.zip as a customization project
3. Publish the customization project.

### Usage

1. Go to Attributes Screen (CS205000) and create new attributes if you need to.
2. Navigate to Lot/Serial Classes Screen (IN207000) and select the Class for which you need to specify list of Attributes, a new Attribute Tab is available to include attributes.
![Screenshot](/_ReadMeImages/IN207000.png)
3. Navigate to Stock Item Screen (IN202500) and create a new Stock Item having Lot/Serial Class created in Step # 2.
4. Create Purchase Order (PO301000) for Stock Item created in Step # 3. And move forward with creating Purchase Receipt (PO302000) for this Purchase Order.
5. Click on Allocation button, you should be able to see Attributes specified in Step # 2 and can specify value for them.
![Screenshot](/_ReadMeImages/PO302000Allocation.png)
6. Apply Attribute From First button copies attribute value specified for very first Lot/Serial Number and applies to rest of the Lot/Serial Number displayed in the dialog. One can specify value for each individual Lot/Serial Number as well.
7. Attribute value can be assigned for Lot/Serial Number while receiving inventory via IN Receipt Screen (IN301000) as well. Allocation dialog is modified same as for Purchase Receipt.
8. Attribute value and image can be assigned to Lot/Serial Number/s via custom Item Lot/Serial # Info screen (IN202501) as well.
9. Attribute value can be imported via Import Lot/Serial Attributes import scenario made available via customization package.
10. 

Known Issues
------------
None at the moment

## Copyright and License

Copyright © `2018` `Acumatica`

This component is licensed under the MIT License, a copy of which is available online [here](LICENSE.md)

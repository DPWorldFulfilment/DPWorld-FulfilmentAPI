# Inventory APIs

### Inventory Summary API
Inventory summary for products
- **URL**:  {dns}/api/ims/v1/inventory/summary/warehouse 
- **Request Type**: POST

#### Query params
|**Field**|**Description**|**Datatype**|**Mandatory**|**Example**|
| :- | :- | :- | :- | :- |
|pageNo|Page Number|integer|no|1|
|pageSize|Page Size|integer|no|100|

#### Request
Note — Pass productFilterParams as null in case you don’t want to filter out based on any specific criterion.
```json
{
  "merchantId": "string",
  "productFilterParams": {
    "productCategory": "string",
    "productVertical": "string",
    "productActiveStatus": true,
    "customPackagingInventory": true,
    "serialised": true,
    "lotManaged": true,
    "dangerous": true,
    "digital": true,
    "bundled": true
  },
  "warehouseFilterList": [
    "string"
  ],
  "productSearchQuery": "string",
  "sortParams": {
    "sortBy": "string",
    "sortOrder": "string"
  },
  "showOnlyNeedsReorder": true
}
```

|**Field**|**Description**|**Datatype**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|merchantId|Unique identifier for the merchant|string|Yes|"merchant123"|
|productFilterParams.productCategory|Filter parameter for the category of the product|string|No|"Electronics"|
|productFilterParams.productVertical|Filter parameter for the vertical of the product|string|No|"Smartphones"|
|productFilterParams.productActiveStatus|Filter parameter to check if the product is active|boolean|No|true|
|productFilterParams.customPackagingInventory|Filter parameter for products with custom packaging|boolean|No|true|
|productFilterParams.serialised|Filter parameter to check if the product is serialized|boolean|No|false|
|productFilterParams.lotManaged|Filter parameter to check if the product is lot managed|boolean|No|true|
|productFilterParams.dangerous|Filter parameter to check if the product is marked as dangerous|boolean|No|false|
|productFilterParams.digital|Filter parameter to check if the product is digital|boolean|No|false|
|productFilterParams.bundled|Filter parameter to check if the product is sold as bundled|boolean|No|true|
|warehouseFilterList|To filter based on warehouseIds|array of strings|No|["warehouseid1", "warehouseId2"]|
|productSearchQuery|Query string to search for products|string|No|"4k television"|
|sortParams.sortBy|Parameter to specify the field to sort by productName or inventoryId|string|No|<p>"inventoryName"</p><p>Or</p><p>“inventoryId”</p>|
|sortParams.sortOrder|Parameter to specify the order of sorting|string|No|"ASC" or "DESC"|
|showOnlyNeedsReorder|Flag to show only products that need reordering|boolean|No|true|

Curl
```bash
curl --location '{dns}/api/ims/v1/inventory/inventory-summary/warehouse?pageNo=1&pageSize=10' \
--header 'Content-Type: application/json' \
--data '{
    "merchantId": "0541d94f-d590-5",
    "productFilterParams": {
    "productCategory": null,
    "productVertical": null,
    "productActiveStatus": true,
    "customPackagingInventory": null,
    "serialised": null,
    "lotManaged":null,
    "dangerous": null,
    "digital": null,
    "bundled": null
  },
    "warehouseFilterList": [],
    "productSearchQuery": "",
    "sortParams": {
        "sortBy": "",
        "sortOrder": ""
    },
    "showOnlyNeedsReorder":false
}'
```
#### Response
200
```json
{
  "status": true,
  "httpStatus": "OK",
  "inventorySummaryList": [
    {
      "inventoryId": "A024-0811E47B2BEAE501",
      "inventoryName": "Samsung Laptop",
      "needsReorder": false,
      "total": 120,
      "incoming": 0,
      "onHand": 120,
      "committed": 0,
      "available": 120,
      "exceptions": 0,
      "batchCount": 1,
      "warehouseInventoryMap": {
        "WAREHOUSE_UK": {
          "warehouseId": "WAREHOUSE_UK",
          "inventoryId": "A024-0811E47B2BEAE501",
          "warehouseName": "Hinckley-UK",
          "needsReorder": false,
          "total": 120,
          "incoming": 0,
          "onHand": 120,
          "committed": 0,
          "available": 120,
          "exceptions": 0,
          "batchCount": 1
        }
      }
    },
    {
      "inventoryId": "A024-0829C9DE075DFC34",
      "inventoryName": "Office Bag",
      "needsReorder": false,
      "total": 150,
      "incoming": 0,
      "onHand": 150,
      "committed": 24,
      "available": 126,
      "exceptions": 0,
      "batchCount": 1,
      "warehouseInventoryMap": {
        "WAREHOUSE_UK": {
          "warehouseId": "WAREHOUSE_UK",
          "inventoryId": "A024-0829C9DE075DFC34",
          "warehouseName": "Hinckley-UK",
          "needsReorder": false,
          "total": 150,
          "incoming": 0,
          "onHand": 150,
          "committed": 24,
          "available": 126,
          "exceptions": 0,
          "batchCount": 1
        }
      }
    },
    {
      "inventoryId": "A024-08E95A43E1536BF6",
      "inventoryName": "One Plus Mobile",
      "needsReorder": false,
      "total": 140,
      "incoming": 150,
      "onHand": 140,
      "committed": 4,
      "available": 136,
      "exceptions": 0,
      "batchCount": 1,
      "warehouseInventoryMap": {
        "WAREHOUSE_UK": {
          "warehouseId": "WAREHOUSE_UK",
          "inventoryId": "A024-08E95A43E1536BF6",
          "warehouseName": "Hinckley-UK",
          "needsReorder": false,
          "total": 140,
          "incoming": 150,
          "onHand": 140,
          "committed": 4,
          "available": 136,
          "exceptions": 0,
          "batchCount": 1
        }
      }
    },
    {
      "inventoryId": "A024-146DB3299CE9E810",
      "inventoryName": "Levis Shirt",
      "needsReorder": false,
      "total": 210,
      "incoming": 0,
      "onHand": 210,
      "committed": 28,
      "available": 182,
      "exceptions": 0,
      "batchCount": 1,
      "warehouseInventoryMap": {
        "WAREHOUSE_UK": {
          "warehouseId": "WAREHOUSE_UK",
          "inventoryId": "A024-146DB3299CE9E810",
          "warehouseName": "Hinckley-UK",
          "needsReorder": false,
          "total": 210,
          "incoming": 0,
          "onHand": 210,
          "committed": 28,
          "available": 182,
          "exceptions": 0,
          "batchCount": 1
        }
      }
    },
    {
      "inventoryId": "A024-14A45C22C3008094",
      "inventoryName": "Chair Sfs",
      "needsReorder": false,
      "total": 120,
      "incoming": 0,
      "onHand": 120,
      "committed": 0,
      "available": 120,
      "exceptions": 0,
      "batchCount": 1,
      "warehouseInventoryMap": {
        "WAREHOUSE_UK": {
          "warehouseId": "WAREHOUSE_UK",
          "inventoryId": "A024-14A45C22C3008094",
          "warehouseName": "Hinckley-UK",
          "needsReorder": false,
          "total": 120,
          "incoming": 0,
          "onHand": 120,
          "committed": 0,
          "available": 120,
          "exceptions": 0,
          "batchCount": 1
        }
      }
    },
    {
      "inventoryId": "A024-1666A79DAA7DC826",
      "inventoryName": "Dell Laptop",
      "needsReorder": false,
      "total": 130,
      "incoming": 0,
      "onHand": 130,
      "committed": 0,
      "available": 130,
      "exceptions": 0,
      "batchCount": 1,
      "warehouseInventoryMap": {
        "WAREHOUSE_UK": {
          "warehouseId": "WAREHOUSE_UK",
          "inventoryId": "A024-1666A79DAA7DC826",
          "warehouseName": "Hinckley-UK",
          "needsReorder": false,
          "total": 130,
          "incoming": 0,
          "onHand": 130,
          "committed": 0,
          "available": 130,
          "exceptions": 0,
          "batchCount": 1
        }
      }
    },
    {
      "inventoryId": "A024-1FF4DC76ACA0DA3D",
      "inventoryName": "Puma Shoes",
      "needsReorder": false,
      "total": 0,
      "incoming": 100,
      "onHand": 0,
      "committed": 0,
      "available": 0,
      "exceptions": 0,
      "batchCount": 1,
      "warehouseInventoryMap": {
        "WAREHOUSE_UK": {
          "warehouseId": "WAREHOUSE_UK",
          "inventoryId": "A024-1FF4DC76ACA0DA3D",
          "warehouseName": "Hinckley-UK",
          "needsReorder": false,
          "total": 0,
          "incoming": 100,
          "onHand": 0,
          "committed": 0,
          "available": 0,
          "exceptions": 0,
          "batchCount": 1
        }
      }
    },
    {
      "inventoryId": "A024-254F4B4EA9C8A363",
      "inventoryName": "Arjun Product SFS",
      "needsReorder": false,
      "total": 0,
      "incoming": 100,
      "onHand": 0,
      "committed": 0,
      "available": 0,
      "exceptions": 0,
      "batchCount": 1,
      "warehouseInventoryMap": {
        "WAREHOUSE_UK": {
          "warehouseId": "WAREHOUSE_UK",
          "inventoryId": "A024-254F4B4EA9C8A363",
          "warehouseName": "Hinckley-UK",
          "needsReorder": false,
          "total": 0,
          "incoming": 100,
          "onHand": 0,
          "committed": 0,
          "available": 0,
          "exceptions": 0,
          "batchCount": 1
        }
      }
    },
    {
      "inventoryId": "A024-286099DEB090496A",
      "inventoryName": "WaterBottle",
      "needsReorder": false,
      "total": 140,
      "incoming": 0,
      "onHand": 140,
      "committed": 1,
      "available": 139,
      "exceptions": 0,
      "batchCount": 1,
      "warehouseInventoryMap": {
        "WAREHOUSE_UK": {
          "warehouseId": "WAREHOUSE_UK",
          "inventoryId": "A024-286099DEB090496A",
          "warehouseName": "Hinckley-UK",
          "needsReorder": false,
          "total": 140,
          "incoming": 0,
          "onHand": 140,
          "committed": 1,
          "available": 139,
          "exceptions": 0,
          "batchCount": 1
        }
      }
    },
    {
      "inventoryId": "A024-37E8DC094ED9510E",
      "inventoryName": "Puma Shoes Red",
      "needsReorder": false,
      "total": 80,
      "incoming": 0,
      "onHand": 80,
      "committed": 0,
      "available": 80,
      "exceptions": 0,
      "batchCount": 1,
      "warehouseInventoryMap": {
        "WAREHOUSE_UK": {
          "warehouseId": "WAREHOUSE_UK",
          "inventoryId": "A024-37E8DC094ED9510E",
          "warehouseName": "Hinckley-UK",
          "needsReorder": false,
          "total": 80,
          "incoming": 0,
          "onHand": 80,
          "committed": 0,
          "available": 80,
          "exceptions": 0,
          "batchCount": 1
        }
      }
    }
  ],
  "pageInfo": {
    "page": 1,
    "size": 10,
    "totalPages": 5,
    "totalElements": 48,
    "hasNext": false
  }
}
```
400
```json
{
  "status": false,
  "message": "Could not find any products with the provided search criteria. ",
  "httpStatus": "BAD_REQUEST"
}
```

### Inventory Product Search API
Fetches the Inventory details based on the various filters like customPackagingInventory, orderSubType, lotManaged, warehouseId, sellable, unsellable
- **URL**:  {dns}/api/ims/v1/inventory/products
- **Request Type**: GET

#### Query params
|**Field**|**Description**|**Datatype**|**Mandatory**|**Example**|
| :- | :- | :- | :- | :- |
|searchProduct|Search by Sku, inventoryId or productName|String|Yes|Iphone|
|sellable|Enter true if product is sellable|Boolean|No|true|
|unsellable|Enter true if product is unsellable|Boolean|No|true|
|warehouseId|Warehouse in which inventory is kept|String|No|WAREHOUSE\_UK|
|lotManaged|Bundled product or not|Boolean|No|true|
|orderSubType|Kitting or dekitting|String|No|KITTING/ DE\_KITTING|
|customPackagingInventory|Product is packaged type |integer|no|1|

Curl
```bash
curl --location --request GET 'http://ecom-qa-ims.dpworld.com/api/ims/v1/inventory/products?searchProduct=A102-0AAF2174F2DA4994&sellable=true&unsellable=true&warehouseId=WAREHOUSE_UK&lotManaged=false' \
--header 'Content-Type: application/json' \
--header 'Cookie: cookiesession1=678A40EFCB896BCC71A5513E9DE2DB58'
```

#### Response
200
```json
{
  "inventoryProductList": [
    {
      "inventoryId": "A102-0AAF2174F2DA4994",
      "productName": "Anker Quick Charge 3.0 63W 5-Port USB Wall Charger, PowerPort Speed 5 for Galaxy S9/S8/S7/S6/Edge/+, Note 5/4 and PowerIQ for iPhone X/8/7/6s/Plus, iPad, LG, Nexus, HTC and More",
      "sku": "B01IUTIUEA",
      "barcode": "X0015PLASL",
      "price": 0,
      "image": null,
      "availableQuantity": 0,
      "totalSellable": 0,
      "totalUnsellable": 0,
      "batch": null,
      "lotManaged": false,
      "kitted": false,
      "hazmat": false,
      "reversePickUp": "Restock",
      "returnToSenderFromCourier": "Restock",
      "backupActionForInspectionFails": null
    }
  ],
  "status": true
}
```
400
```json
{
  "timestamp": "2024-03-08T11:01:47.411070642",
  "errorReasonCode": "BAD_REQUEST_EXCEPTION",
  "status": "BAD_REQUEST",
  "message": "SearchProduct can't be null",
  "requestId": "65eaf01bce077e4b3d7aab62de69a49f",
  "errors": [
    "BAD_REQUEST_EXCEPTION"
  ]
}
```

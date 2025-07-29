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

### Inventory History API (Inventory Ledger API)
Inventory Ledger
- **URL**:  {dns}/api/ims/v1/inventory/inventory/history?inventoryId=B732-TEST_PARENT&fromDate=2025-07-01&toDate=2025-07-29&warehouseId=IMS_1723_MIDDLETOWN&direction=DESC&pageNo=1&pageSize=15&referenceId=RO-10000099615&action=EN_ROUTE&sortOn=createdAt
- **Request Type**: GET

#### Query params
| **Field**                  | **Description**                                   | **Datatype**      | **Mandatory** | **Example**           |
| -------------------------- | ------------------------------------------------- | ----------------- | ------------- | --------------------- |
| `inventoryId`              | Inventory ID to filter                            | String            | No            | B732-TEST\_PARENT     |
| `fromDate`                 | Start date for inventory movement or status       | Date (YYYY-MM-DD) | No            | 2025-07-01            |
| `toDate`                   | End date for inventory movement or status         | Date (YYYY-MM-DD) | No            | 2025-07-29            |
| `warehouseId`              | Warehouse in which inventory is kept              | String            | No            | IMS\_1723\_MIDDLETOWN |
| `direction`                | Sort direction                                    | String            | No            | DESC                  |
| `pageNo`                   | Page number for pagination                        | Integer           | No            | 1                     |
| `pageSize`                 | Number of records per page                        | Integer           | No            | 15                    |
| `referenceId`              | Related transaction or document reference         | String            | No            | RO-10000099615        |
| `action`                   | Current inventory action                          | String            | No            | EN\_ROUTE             |
| `sortOn`                   | Field name to sort results on                     | String            | No            | createdAt             |

Curl
```bash
curl --location 'https://ecom-sfs-nonprod.dpworld.com/sfs-preprod/api/ims/v1/inventory/history?inventoryId=B732-TEST_PARENT&fromDate=2025-07-01&toDate=2025-07-29&warehouseId=IMS_1723_MIDDLETOWN&direction=DESC&pageNo=1&pageSize=15&referenceId=RO-10000099615&action=EN_ROUTE&sortOn=createdAt' \
--header 'accept: */*' \
--header 'Content-Type: application/json' \
--header 'Ocp-Apim-Subscription-Key: <subscriptionKey>' \
--header 'Authorization: Bearer <token>'
```

#### Response
200
```json
{
  "inventoryHistoryProjectionList": [
    {
      "action": "EN_ROUTE",
      "inventoryId": "B732-TEST_PARENT",
      "event": "ORACLE_PUT_AWAY_EVENT",
      "warehouseId": "IMS_1723_MIDDLETOWN",
      "quantity": "10",
      "eventTimeStamp": null,
      "batchNumber": "NA",
      "ledgerEvent": null,
      "createdAt": "2025-07-28 07:16:32.0",
      "eventRefId": "RO-10000099615",
      "adjustmentType": "DEBIT",
      "inventoryBalance": "10"
    },
    {
      "action": "EN_ROUTE",
      "inventoryId": "B732-TEST_PARENT",
      "event": "RO_CREATION",
      "warehouseId": "IMS_1723_MIDDLETOWN",
      "quantity": "10",
      "eventTimeStamp": null,
      "batchNumber": "NA",
      "ledgerEvent": null,
      "createdAt": "2025-07-28 07:10:54.0",
      "eventRefId": "RO-10000099615",
      "adjustmentType": "CREDIT",
      "inventoryBalance": "0"
    }
  ],
  "inventoryHistoryDtos": [
    {
      "event": "ORACLE_PUT_AWAY_EVENT",
      "action": "EN_ROUTE",
      "eventRefId": "RO-10000099615",
      "eventTimeStamp": null,
      "inventoryId": "B732-TEST_PARENT",
      "warehouseId": "IMS_1723_MIDDLETOWN",
      "warehouseLabel": "Middletown (United States)",
      "batchNumber": "NA",
      "adjustmentType": "DEBIT",
      "quantity": "10",
      "createdAt": "2025-07-28 07:16:32.0"
    },
    {
      "event": "RO_CREATION",
      "action": "EN_ROUTE",
      "eventRefId": "RO-10000099615",
      "eventTimeStamp": null,
      "inventoryId": "B732-TEST_PARENT",
      "warehouseId": "IMS_1723_MIDDLETOWN",
      "warehouseLabel": "Middletown (United States)",
      "batchNumber": "NA",
      "adjustmentType": "CREDIT",
      "quantity": "10",
      "createdAt": "2025-07-28 07:10:54.0"
    }
  ],
  "pageInformation": {
    "page": 1,
    "size": 15,
    "totalPages": 1,
    "totalElements": 2,
    "hasNext": false
  }
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
## 📘 Supported `action` Filters for Inventory History API

The `action` parameter in the Inventory History API helps filter inventory events based on their specific lifecycle transitions or system-triggered changes. This is useful for tracking movements, anomalies, and stock state updates.

Below is the complete list of supported `action` values:

| Action | Description |
|--------|-------------|
| `EN_ROUTE` | Inventory that is currently in transit. |
| `AVAILABLE` | Inventory available for allocation or reservation. |
| `SOFT_ALLOCATE` | Inventory tentatively reserved but not finalized. |
| `ALLOCATED` | Inventory committed to an order. |
| `IN_PROCESS` | Inventory involved in ongoing warehouse operations. |
| `REJECTED` | Items rejected during receiving or inspection. |
| `BLOCKED` | Inventory blocked due to quality or compliance issues. |
| `LOST` | Inventory that has been lost or cannot be accounted for. |
| `RECEIVED` | Inventory successfully received into the warehouse. |
| `EXCESS_RECEIVED` | Extra units received over expected quantity. |
| `EXCESS_PUT_AWAY` | Excess inventory placed into storage. |
| `EXCESS_BROKEN` | Broken or damaged excess inventory. |
| `RESERVED` | Inventory set aside for specific use or future allocation. |
| `DAMAGED` | Items marked as damaged and unavailable for normal use. |
| `EXPIRED` | Inventory past its expiration date. |
| `NEAR_EXPIRED` | Inventory approaching expiration date. |
| `FACTORY_FAULT` | Items marked defective from the manufacturer. |
| `RECALL` | Items under manufacturer or supplier recall. |
| `IN_TRANSIT_DAMAGED` | Inventory damaged while in transit. |
| `DAMAGED_RESERVED` | Reserved inventory that is damaged. |
| `EXPIRED_RESERVED` | Reserved inventory that has expired. |
| `NEAR_EXPIRED_RESERVED` | Reserved inventory nearing expiration. |
| `DAMAGED_ALLOCATED` | Allocated inventory found to be damaged. |
| `FACTORY_FAULT_RESERVED` | Reserved inventory flagged as factory fault. |
| `EXPIRED_ALLOCATED` | Allocated inventory that has expired. |
| `FACTORY_FAULT_ALLOCATED` | Allocated inventory with factory defects. |
| `NEAR_EXPIRED_ALLOCATED` | Allocated inventory nearing expiry. |
| `ON_HOLD` | Inventory placed on hold for manual review or issue resolution. |
| `NEAR_EXPIRY` | Alternate label for items close to expiration. |
| `INTRANSIT_DAMAGED` | Another label for damaged items during transit. |

>

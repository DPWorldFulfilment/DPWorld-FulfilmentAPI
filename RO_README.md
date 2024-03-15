

# Receiving Order / Inbound

To receive stock at the warehouse, a Receiving Order (inbound) needs to be created beforehand so that the warehouse becomes aware of the incoming shipment. The inbound must contain a detailed list of items in the shipment. The inbound can either be created through the fulfillment portal or through the API.

## Receiving Order APIs

### RO Create API

- **Description**: This API creates an Inbound Order.
- **URL**: `/api/v1/ims/ro/create`
- **Verb**: POST
#### Request Header: 
  | Field        | Description | Data Type | Mandatory | Example | 
|--------------|-------------|-----------|-----------|---------| 
| languageCode | Language    | Enum      | Yes       | En, Fr  | 
  
#### Request Body:

| Field              | Description                                     | Data Type | Mandatory | Example          |
|--------------------|-------------------------------------------------|-----------|-----------|------------------|
| orderChannelId     | Identifier for the order channel.               | String    | Yes       | CL               |
| orderSourceId      | Identifier for the order source.                | String    | Yes       | PARCEL_NINJA     |
| buId               | Business unit ID: Unique for each seller.       | String    | Yes       | PARCEL_NINJA     |
| orderType          | Order Type (Accepts only “RECEIVING_ORDER”).    | String    | Yes       | RECEIVING_ORDER  |
| subOrderType       | Defines type of inbound.                        | String    | Yes       | DEFAULT/RTO/RVP  |
| consigneeOrderId   | To be provided by the user.                     | String    | No        | "20243544"       |
| orderPlacedAt      | Date of order placed (YYYY-MM-DD).              | String    | Yes       | "2024-01-23"     |
| fulfillmentType    | It defines the flow of inbound.                 | String    | Yes       | C2W/S2W/W2W      |
| currency           | Currency (USD, ZAR, AED).                       | String    | Yes       | USD, ZAR, AED    |
| shippingMethod     | Type of shipping the user wants.                | String    | Yes       | PARCEL_NINJA_SHIPPING, DROP_AT_WAREHOUSE |
| shippingOptions    | Additional option over shipping method.         | String    | Yes       | NA, CHEAPEST, FASTEST |
|consignorDetails |This field contains all the information related to the seller or user who is requesting inbound| Object | Yes ||
|warehouseInfo| This field contains warehouseId for which inbound is created| Object | Yes ||
|parcelDetails| This field contains parcel details| Object | Yes ||
|fulfillmentLines| Contains items info| Object | Yes ||
|additionalAttributes| Some additional data can be sent in this object| Object | Yes ||
|lineDates| This field contains dates related fields| Object | Yes ||
|boxInfo| Contains box details if a user wants to give the configuration of boxes. (Yes, if parcelConfigs selected is of parcel type)| Object | Yes ||

```json
{
  "orderChannelId": "PARCEL_NINJA",
  "orderSourceId": "PARCEL_NINJA",
  "buId": "PARCEL_NINJA",
  "orderType": "RECEIVING_ORDER",
  "subOrderType": "DEFAULT",
  "consigneeOrderId": "999999001",
  "orderPlacedAt": "2023-09-04",
  "fulfillmentType": "S2W",
  "shippingMethod": "DROP_AT_WAREHOUSE",
  "shippingOptions": "NA",
  "carrierMethod": "BLUE_DART",
  "currency": "USD",
  "consignorDetails": {
    "consignorId": "4cf19e27-3fe0-5",
    "pickUpInfo": {
      "customerAddressId": "142",
      "contact": {
        "name": {
          "firstName": "David",
          "lastName": "Warner",
          "middleName": "",
          "nickName": ""
        },
        "phone": "0813073399",
        "email": "david@yahoo.com"
      },
      "address": {
        "unitNumber": "",
        "lineOne": "4 Huntingdon Road",
        "lineTwo": "xyzRajan",
        "geographicLocation": "",
        "street": "LANKAN STREET",
        "poBox": "",
        "city": "Sandton",
        "region": "Gauteng",
        "country": "South Africa",
        "zip": "2196",
        "suburb": "Sandton",
        "addressType": "Residential"
      }
    }
  },
  "warehouseInfo": {
    "warehouseId": "IMS_PARCEL_NINJA_WAREHOUSE_1_PARCEL_NINJA",
    "labelName": "PARCEL_NINJA_WAREHOUSE"
  },
  "lineDates": {
    "pickUpDate": "2024-12-30",
    "expectedShipDate": "2024-12-30"
  },
  "parcelDetails": {
    "parcelConfigs": [
      {
        "unitOfMeasure": "Boxes",
        "measurementValue": "2"
      },
      {
        "unitOfMeasure": "container",
        "measurementValue": "60ft * 40ft"
      },
      {
        "unitOfMeasure": "Pallets",
        "measurementValue": "150"
      }
    ],
    "attributeData": [
      {
        "attributeName": "multipleSkuPerBox",
        "attributeValue": "true"
      },
      {
        "attributeName": "oneSkuPerBox",
        "attributeValue": "false"
      }
    ]
  },
  "fulfillmentLines": {
    "totalLineQty": 3450,
    "orderLineDetails": [
      {
        "fulfillmentLineId": "1",
        "itemDetails": {
          "inventoryId": "DPW-4cf19e27-3fe0-5-re4",
          "barcode": "test321312",
          "quantity": {
            "orderQty": 15,
            "unitOfMeasure": "EA",
            "measurementValue": "12"
          },
          "packingConfig": {
            "labeling": "true",
            "bubbleWrapping": "false",
            "bagging": "false",
            "bubbleMail": "false"
          }
        }
      },
      {
        "fulfillmentLineId": "2",
        "itemDetails": {
          "inventoryId": "DPW-4cf19e27-3fe0-5-PX123",
          "barcode": "test32131sc2",
          "quantity": {
            "orderQty": 15,
            "unitOfMeasure": "EA",
            "measurementValue": "12"
          },
          "packingConfig": {
            "labeling": "true",
            "bubbleWrapping": "false",
            "bagging": "false",
            "bubbleMail": "false"
          }
        }
      }
    ]
  },
  "boxInfo": [
    {
      "boxId": "01",
      "trackingId": "21qweqwrw",
      "boxCount": "1",
      "boxConfig": [
        {
          "fulfillmentLineId": "1",
          "parcelConfig": {
            "unitOfMeasure": "EA",
            "measurementValue": "15"
          }
        },
        {
          "fulfillmentLineId": "1",
          "parcelConfig": {
            "unitOfMeasure": "EA",
            "measurementValue": "15"
          }
        }
      ]
    }
  ],
  "additionalAttributes": [
    {
      "attributeType": "LINE_ATTRIBUTES",
      "attributeData": [
        {
          "attributeName": "name",
          "attributeValue": "hrithik"
        }
      ]
    },
    {
      "attributeType": "ADDITIONAL_ATTRIBUTES",
      "attributeData": [
        {
          "attributeName": "role",
          "attributeValue": "dancing"
        },
        {
          "attributeName": "class",
          "attributeValue": "2016"
        }
      ]
    },
    {
      "attributeType": "ORDER_ATTRIBUTES",
      "attributeData": [
        {
          "attributeName": "priorityInbound",
          "attributeValue": "false"
        }
      ]
    }
  ]
}
```

#### Response:
200 OK

```json
{ 
   "receivingOrderId": "RO-11000001742" 
}
```

400
```json
{
  "timestamp": "2024-03-06T11:07:36.600482",
  "errorReasonCode": null,
  "status": "BAD_REQUEST",
  "message": "No enum constant ecom.ims.enums.ShippingOptions.NASA",
  "requestId": "65e84e78f6997518f94174045644f13e",
  "errors": [
    "BAD_REQUEST_EXCEPTION"
  ]
}
```

### RO Detail API

- **Description**: This API is used to fetch Inbound details  
- **Verb**: GET      
- **URL**: /api/v1/ims/ro/receving-orders/{orderId} 
#### Request Header: 
| Field       | Description        | Data Type | Mandatory | Example     | 
|-------------|--------------------|-----------|-----------|-------------| 
| languageCode| Language           | Enum      | Yes       | En, Fr      | 
| tenantCode  | Takes Tenant type  | Enum      | Yes       | SFS, DUBUY_COM, THREE_PE | 

#### RequestBody:
No Body 

```bash
curl --location 'localhost:8080/api/ims/v1/ro/receiving-order/RO-11000001314' \
--header 'languageCode: en' \
--header 'tenantCode: DUBUY_COM'
```

#### Response
200 OK
```json
{
  "fulfillmentOrderId": 2414,
  "orderChannelId": null,
  "orderSourceId": null,
  "buId": null,
  "orderType": "RECEIVING_ORDER",
  "subOrderType": "RTO",
  "consigneeOrderId": "999999001",
  "sellerId": "4cf19e27-3fe0-5",
  "warehouseId": "IMS_PARCEL_NINJA_WAREHOUSE_1_PARCEL_NINJA",
  "fulfillmentType": "C2W",
  "shippingMethod": "DROP_AT_WAREHOUSE",
  "carrierMethod": "NA",
  "customerLanguageId": 1,
  "currentStatus": "AWAITING_ARRIVAL",
  "statusBar": [],
  "currency": "USD",
  "onHoldRODetails": null,
  "additionalAttributes": [
    {
      "attributeType": "LINE_ATTRIBUTES",
      "attributeData": [
        {
          "id": 4582,
          "attributeName": "name",
          "attributeValue": "hrithik"
        }
      ]
    },
    {
      "attributeType": "ORDER_ATTRIBUTES",
      "attributeData": [
        {
          "id": 4585,
          "attributeName": "priorityInbound",
          "attributeValue": "false"
        }
      ]
    },
    {
      "attributeType": "ADDITIONAL_ATTRIBUTES",
      "attributeData": [
        {
          "id": 4583,
          "attributeName": "role",
          "attributeValue": "dancing"
        },
        {
          "id": 4584,
          "attributeName": "class",
          "attributeValue": "2016"
        }
      ]
    }
  ],
  "lineDates": {
    "id": 1656,
    "minDeliveryDate": null,
    "maxDeliveryDate": null,
    "orderProcessingDate": null,
    "preciseDeliveryDate": null,
    "expectedShipDate": "2024-12-30T00:00:00.000+00:00",
    "pickUpDate": null
  },
  "fulfillmentLines": {
    "totalLineQty": 0,
    "orderDetails": [
      {
        "id": 4597,
        "orderPlacedQuantity": 15,
        "fulfillmentLineId": 1,
        "inventoryId": "A002-3B2B4BF6CCD274A7",
        "unitOfMeasure": "EA",
        "measurementValue": "15"
      },
      {
        "id": 4598,
        "orderPlacedQuantity": 30,
        "fulfillmentLineId": 1,
        "inventoryId": "A002-F95D3A30296F578C",
        "unitOfMeasure": "EA",
        "measurementValue": "30"
      }
    ]
  },
  "parcelDetails": [
    {
      "measurementValue": "60ft * 40ft",
      "quantityUOM": "container",
      "oneSkuPerBox": null,
      "multipleSkuPerBox": null
    },
    {
      "measurementValue": "150",
      "quantityUOM": "Pallets",
      "oneSkuPerBox": false,
      "multipleSkuPerBox": true
    }
  ],
  "boxInfo": [],
  "attachment": {},
  "itemsInfo": [
    {
      "inventoryId": "A002-3B2B4BF6CCD274A7",
      "sku": "FINAL TEST1",
      "itemName": "Gucci Bag",
      "qtySent": 15,
      "qtyReceived": 0,
      "hazardous": false,
      "barcode": "123457"
    },
    {
      "inventoryId": "A002-F95D3A30296F578C",
      "sku": "33333",
      "itemName": "3323333",
      "qtySent": 30,
      "qtyReceived": 0,
      "hazardous": false,
      "barcode": "4444444"
    }
  ],
  "sellerAddressDetails": {
    "consigneeId": "4cf19e27-3fe0-5",
    "shippingTo": {
      "id": null,
      "contact": {
        "contactId": 2588,
        "name": {
          "customerInfoId": 2586,
          "firstName": "David",
          "lastName": "Warner",
          "middleName": null,
          "nickName": null
        },
        "phone": "0813073399",
        "email": "david@yahoo.com"
      },
      "address": {
        "addressId": 1593,
        "unitNumber": "",
        "lineOne": "4 Huntingdon Road",
        "lineTwo": "xyzRajan",
        "geographicLocation": "",
        "street": "LANKAN STREET",
        "poBox": null,
        "cityName": "Sandton",
        "countryName": "South Africa",
        "zipCode": "2196",
        "regionName": "Gauteng",
        "addressType": "Residential",
        "suburb": "Sandton",
        "suburbId": 414051
      }
    }
  },
  "vasResponse": [
    {
      "actualFulfillmentLineId": 1,
      "packingConfigTypes": {
        "labeling": true,
        "bubbleWrapping": false,
        "bagging": false,
        "bubbleMail": false
      },
      "totalCost": "60"
    },
    {
      "actualFulfillmentLineId": 1,
      "packingConfigTypes": {
        "labeling": true,
        "bubbleWrapping": false,
        "bagging": false,
        "bubbleMail": false
      },
      "totalCost": "60"
    }
  ],
  "trackingTypeToTrackingDetailsMap": {}
}
```

404
```json
{
  "timestamp": "2024-03-07T06:12:43.43539",
  "errorReasonCode": null,
  "status": "NOT_FOUND",
  "message": "Resource not found",
  "requestId": "65e95adb05026deec22ed6176023e5cb",
  "errors": [
    "No receiving order found for RO-11000001314ws"
  ]
}
```

417
```json
{
  "timestamp": "2024-03-07T06:13:07.257954",
  "errorReasonCode": null,
  "status": "EXPECTATION_FAILED",
  "message": "Required request header 'tenantCode' for method parameter type String is not present",
  "requestId": "65e95af30bb3238172b7b7491a738007",
  "errors": [
    "INVENTORY_EVENT_EXCEPTION"
  ]
}
```

### RO Listing API

- **Description**: This API is used to fetch all the inbounds based on filters
- **Verb**:  POST
- **URL**: /api/v1/ims/ro/receving-orders

#### Request Param
|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|limit|Number of elemnts in one page|Integer|No|10|
|page|Page Number|Integer|No|2|
|sortOn|It will give you sorted response based on field you applied sorting|String|No|Value must be from the fields that are there in response only|
|direction|ASC, DESC|String|No|ASC, DSC|

#### Request
```json
{

  "sellerId": "4cf19e27-3fe0-5",
  "subOrderType": [
       "RVP",
       "DEFAULT"
  ],
  "orderStatuses": [],
  "warehouseIds": [],
  "startDate": "2023-10-12",
  "endDate": "2024-11-15",
  "searchParam": null
}
```

|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|sellerId|SellerId of user to fetch its inbounds|String|Yes|"sellerId”|
|subOrderType|It filters inbounds based on subOrderType|List<String>|Yes|[“RVP”,” RTO”,”DEFAULT”]|
|orderStatuses|It filters inbounds based on orderStatus|List<String>|No|[“PENDING”, CREATED”]|
|warehouseIds|It filters inbounds based on warehouseId|List<String>|No|[“warehouseId”]|
|startDate|It filters inbounds based on date|String |Yes|“2024-01-23"Format must be “YYYY-MM-DD"|
|endDate|It filters inbounds based on date|String|Yes|“2024-02-15"Format must be “YYYY-MM-DD"|
|searchParam|It filters inbounds based on search param |String |No|“RO-123”|

```bash
Curl:
curl --location 'localhost:8080/api/ims/v1/ro/receiving-orders?limit=2&page=1&sortOn=createdOn&direction=DESC' \
--header 'Content-Type: application/json' \
--data '{
    "sellerId": "4cf19e27-3fe0-5",
    "subOrderType": ["RVP","DEFAULT"],
    "orderStatuses":[],
    "warehouseIds": [],
    "startDate": "2023-10-12",
    "endDate": "2024-11-15",
    "searchParam": null
}'
```

#### Response

200
```json
{
  "receivingOrdersResponses": [
    {
      "orderId": "RO-11000001742",
      "poNbr": "999999001",
      "subOrderType": "DEFAULT",
      "orderStatus": "AWAITING_ARRIVAL",
      "sellerId": "4cf19e27-3fe0-5",
      "fulfillmentCenter": "Linbro - South Africa",
      "createdOn": "2024-03-06T11:06:01.000+00:00",
      "manifestLink": "https://stsfsakamaipreprod.blob.core.windows.net/static-content-preprod-sfs/pdf/MANIFEST/uploaded/RO-11000001742.pdf"
    },
    {
      "orderId": "RO-11000001712",
      "poNbr": "999999001",
      "subOrderType": "DEFAULT",
      "orderStatus": "AWAITING_ARRIVAL",
      "sellerId": "4cf19e27-3fe0-5",
      "fulfillmentCenter": "EUROPE",
      "createdOn": "2024-02-26T07:53:06.000+00:00",
      "manifestLink": "https://stsfsakamaipreprod.blob.core.windows.net/static-content-preprod-sfs/pdf/MANIFEST/uploaded/RO-11000001712.pdf"
    }
  ],
  "totalElements": 271,
  "status": true
}
```

400 
```json
{
  "timestamp": "2024-03-07T07:12:11.502452",
  "errorReasonCode": "ERR-IMS-136",
  "status": "BAD_REQUEST",
  "message": "provide valid date format \"yyyy-MM-dd\"",
  "requestId": "65e968cb415fe7f4000bf87c52d65ce7",
  "errors": [
    "BAD_REQUEST_EXCEPTION"
  ]
}
```

404 
```json
{
  "timestamp": "2024-03-07T07:12:44.612571",
  "errorReasonCode": null,
  "status": "NOT_FOUND",
  "message": "Resource not found",
  "requestId": "65e968ec0d0e8e6dc7bbe88625089a31",
  "errors": [
    "No data Found for request"
  ]
}
```

417
```json
{
  "timestamp": "2024-03-07T07:13:03.482849",
  "errorReasonCode": null,
  "status": "EXPECTATION_FAILED",
  "message": "Content-Type is not supported",
  "requestId": "65e968ffd9c36c06e30a6dc83cc9e053",
  "errors": [
    "INVENTORY_EVENT_EXCEPTION"
  ]
}
```

### Create Draft Inbound API

- **Description**: This API is used to create draft inbounds which can then be used to create inbound and you can update the draft
- **URL**: {DNS}/api/v1/ims/ro/draft
- **Request Type**: POST 
- **Request Header**: languageCode

|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|languageCode|Language|Enum|Yes|En, Fr |

#### Request
```json
{
  "platformId": "Contractual Logistics:Imperial:WWHC",
  "sellerId": "4cf19e27-3fe0-5",
  "warehouseId": "IMS_DEFAULT",
  "orderType": "DRAFT_RECEIVING_ORDER",
  "draftPayload": "{\"consigneeOrderId\":\"\",\"fulfillmentType\":\"S2W\",\"shippingMethod\":\"DROP_AT_WAREHOUSE\",\"shippingOptions\":null,\"carrierMethod\":\"\",\"currency\":\"USD\",\"consignorDetails\":{\"consignorId\":\"ee00c1d4-9c25-5\",\"merchantTag\":null,\"pickUpInfo\":{\"customerAddressId\":null,\"contact\":{\"name\":{\"firstName\":\"ramanMechant 2\",\"lastName\":\"Warner\",\"middleName\":null,\"nickName\":null},\"phone\":\"R5wJgNioSTX2qFQlEyub0g\",\"email\":\"nike.merchant@maildrop.cc\"},\"address\":{\"unitNumber\":null,\"lineOne\":\"23423541\",\"lineTwo\":\"PEOPLES COLONY\",\"geographicLocation\":null,\"street\":\"RAJAN\",\"poBox\":null,\"city\":\"Zastron\",\"country\":\"South Africa\",\"zip\":\"9950\",\"region\":\"Free State\",\"addressType\":\"PICKUP\",\"suburb\":\"Nuwe Lokasie\",\"suburbId\":null,\"orderType\":null}}},\"warehouseInfo\":{\"warehouseId\":\"149091_ORACLE\",\"labelName\":null,\"name\":null,\"providerName\":null},\"parcelDetails\":{\"parcelConfigs\":[{\"unitOfMeasure\":\"container\",\"measurementValue\":\"40 feet\"}],\"attributeData\":[{\"attributeName\":\"multipleSkuPerBox\",\"attributeValue\":\"true\"},{\"attributeName\":\"oneSkuPerBox\",\"attributeValue\":\"false\"}]},\"lineDates\":{\"expectedShipDate\":\"2024-03-07\"},\"fulfillmentLines\":{\"totalLineQty\":10,\"orderLineDetails\":[{\"fulfillmentLineId\":1,\"refId\":null,\"itemDetails\":{\"inventoryId\":\"A126-F200229620C31629\",\"barcode\":\"TESTVENREY\",\"weight\":null,\"volume\":null,\"action\":null,\"quantity\":{\"orderQty\":10,\"unitOfMeasure\":\"EA\",\"measurementValue\":\"10\"},\"packingConfig\":{\"labeling\":false,\"bubbleWrapping\":false,\"bagging\":false,\"bubbleMail\":false},\"shnId\":null,\"issue\":null,\"sellerAction\":null}}]},\"boxInfo\":null,\"additionalAttributes\":[{\"attributeType\":\"ORDER_ATTRIBUTES\",\"attributeData\":[{\"attributeName\":\"priorityInbound\",\"attributeValue\":\"false\"}]}]}"
}
```

|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|platformId|PlatformId, it is field validated from our end|String|Yes|"platformId”|
|sellerId|SellerId of user creating draft inbound|String|Yes|“sellerId”|
|warehouseId|WarehouseId for which inbound needs to be created|String|Yes|“warehouseId”|
|orderType|DRAFT_RECEIVING_ORDER|String|Yes|“DRAFT_RECEIVING_ORDER”|
|draftPayload|This field will have all the payload in string format that user has given|String |Yes|"draftPayload”|

#### Response
200
```json
{
  "orderId": "DRAFT-RO-11000001744",
  "sellerId": "4cf19e27-3fe0-5",
  "createdOn": "2024-03-07T08:04:59.004+00:00",
  "updatedAt": "2024-03-07T08:04:59.004+00:00",
  "poNbr": null,
  "fulfillmentCenter": "PARCEL_NINJA_WAREHOUSE TEST 3",
  "warehouseId": "IMS_DEFAULT",
  "orderStatus": "DRAFT",
  "subOrderType": "DEFAULT",
  "manifestLink": "NA"
}
```

400
```json
{
  "timestamp": "2024-03-07T08:06:54.59977",
  "errorReasonCode": "CREATE_DRAFT_RECEIVING_ORDER_BAD_REQUEST_EXCEPTION",
  "status": "BAD_REQUEST",
  "message": "sellerId cannot be null",
  "requestId": "65e9759d7a19674e94ef3dd96402795d",
  "errors": [
    "BAD_REQUEST_EXCEPTION"
  ]
}
```

417
```json
{
  "timestamp": "2024-03-07T08:07:10.050725",
  "errorReasonCode": null,
  "status": "EXPECTATION_FAILED",
  "message": "Required request header 'languageCode' for method parameter type String is not present",
  "requestId": "65e975ae4a76b66babd3940eee35c96b",
  "errors": [
    "INVENTORY_EVENT_EXCEPTION"
  ]
}
```

### Update Draft Inbound API

- ***Description**: This API is used to update draft inbounds that was already created
- ***URL**: {DNS}/api/v1/ims/ro/draft
- ***Verb**: PUT
#### Request Header: - languageCode

|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|languageCode|Language|Enum|Yes|En, Fr |

#### Request

```json
{
  "platformId": "Contractual Logistics:Imperial:WWHC",
  "draftOrderId": "DRAFT-RO-10000000352",
  "sellerId": "M1233",
  "warehouseId": "IMS_DEFAULT",
  "orderType": "DRAFT_RECEIVING_ORDER",
  "draftPayload": "{\"consigneeOrderId\":\"\",\"fulfillmentType\":\"S2W\",\"shippingMethod\":\"DROP_AT_WAREHOUSE\",\"shippingOptions\":null,\"carrierMethod\":\"\",\"currency\":\"USD\",\"consignorDetails\":{\"consignorId\":\"ee00c1d4-9c25-5\",\"merchantTag\":null,\"pickUpInfo\":{\"customerAddressId\":null,\"contact\":{\"name\":{\"firstName\":\"ramanMechant 2\",\"lastName\":\"Warner\",\"middleName\":null,\"nickName\":null},\"phone\":\"R5wJgNioSTX2qFQlEyub0g\",\"email\":\"nike.merchant@maildrop.cc\"},\"address\":{\"unitNumber\":null,\"lineOne\":\"23423541\",\"lineTwo\":\"PEOPLES COLONY\",\"geographicLocation\":null,\"street\":\"RAJAN\",\"poBox\":null,\"city\":\"Zastron\",\"country\":\"South Africa\",\"zip\":\"9950\",\"region\":\"Free State\",\"addressType\":\"PICKUP\",\"suburb\":\"Nuwe Lokasie\",\"suburbId\":null,\"orderType\":null}}},\"warehouseInfo\":{\"warehouseId\":\"149091_ORACLE\",\"labelName\":null,\"name\":null,\"providerName\":null},\"parcelDetails\":{\"parcelConfigs\":[{\"unitOfMeasure\":\"container\",\"measurementValue\":\"40 feet\"}],\"attributeData\":[{\"attributeName\":\"multipleSkuPerBox\",\"attributeValue\":\"true\"},{\"attributeName\":\"oneSkuPerBox\",\"attributeValue\":\"false\"}]},\"lineDates\":{\"expectedShipDate\":\"2024-03-07\"},\"fulfillmentLines\":{\"totalLineQty\":10,\"orderLineDetails\":[{\"fulfillmentLineId\":1,\"refId\":null,\"itemDetails\":{\"inventoryId\":\"A126-F200229620C31629\",\"barcode\":\"TESTVENREY\",\"weight\":null,\"volume\":null,\"action\":null,\"quantity\":{\"orderQty\":10,\"unitOfMeasure\":\"EA\",\"measurementValue\":\"10\"},\"packingConfig\":{\"labeling\":false,\"bubbleWrapping\":false,\"bagging\":false,\"bubbleMail\":false},\"shnId\":null,\"issue\":null,\"sellerAction\":null}}]},\"boxInfo\":null,\"additionalAttributes\":[{\"attributeType\":\"ORDER_ATTRIBUTES\",\"attributeData\":[{\"attributeName\":\"priorityInbound\",\"attributeValue\":\"false\"}]}]}"
}
```

|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|platformId|PlatformId, it is field validated from our end|String|Yes|"platformId”|
|sellerId|SellerId of user creating draft inbound|String|Yes|“sellerId”|
|warehouseId|WarehouseId for which inbound needs to be created|String|Yes|“warehouseId”|
|orderType|DRAFT_RECEIVING_ORDER|String|Yes|“DRAFT_RECEIVING_ORDER”|
|draftPayload|This field will have all the payload in string format that user has given|String |Yes|"draftPayload”|
|draftOrderId|Draft inbound id which you want to update|String|Yes|“orderId”|

#### Response
```json
{
  "orderId": "DRAFT-RO-11000001744",
  "sellerId": "4cf19e27-3fe0-5",
  "createdOn": "2024-03-07T08:04:59.004+00:00",
  "updatedAt": "2024-03-07T08:04:59.004+00:00",
  "poNbr": null,
  "fulfillmentCenter": "PARCEL_NINJA_WAREHOUSE TEST 3",
  "warehouseId": "IMS_DEFAULT",
  "orderStatus": "DRAFT",
  "subOrderType": "DEFAULT",
  "manifestLink": "NA"
}
```

400
```json
{
  "timestamp": "2024-03-07T08:13:58.720717",
  "errorReasonCode": "UPDATE_DRAFT_RECEIVING_ORDER_BAD_REQUEST_EXCEPTION",
  "status": "BAD_REQUEST",
  "message": "No draft order found for this orderId",
  "requestId": "65e97746bb10162cbf5a1148530b06f1",
  "errors": [
    "BAD_REQUEST_EXCEPTION"
  ]
}
```

417
```json
{
  "timestamp": "2024-03-07T08:07:10.050725",
  "errorReasonCode": null,
  "status": "EXPECTATION_FAILED",
  "message": "Required request header 'languageCode' for method parameter type String is not present",
  "requestId": "65e975ae4a76b66babd3940eee35c96b",
  "errors": [
    "INVENTORY_EVENT_EXCEPTION"
  ]
}
```

### Get Draft Inbound Details API
- **Description**: This API is used to fetch draft inbound details 
- **URL**: {DNS}/api/v1/ims/ro/draft-order/{orderId}
- **Verb**: GET
#### Request Header
languageCode
|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|languageCode|Language|Enum|Yes|En, Fr |

#### Request Param
sellerId
|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|sellerId|SellerId of user who created draft Inbound |String|Yes|“sellerId”|

Curl 
```bash
curl --location 'localhost:8080/api/ims/v1/ro/draft-order/DRAFT-RO-11000001003?sellerId=4cf19e27-3fe0-5' \
--header 'languageCode: en'
```
#### Response

200
```json
{
  "draftReceivingOrderId": "DRAFT-RO-11000001003",
  "sellerId": "4cf19e27-3fe0-5",
  "createdAt": "2023-11-02T12:33:55.000+00:00",
  "updatedAt": "2023-12-04T07:47:23.000+00:00",
  "fulfillmentCenter": "Linbro - South Africa",
  "warehouseId": "IMS_PARCEL_NINJA_WAREHOUSE_1_PARCEL_NINJA",
  "status": "CREATED",
  "draftPayload": "{\"consigneeOrderId\":\"\",\"fulfillmentType\":\"S2W\",\"shippingMethod\":\"DROP_AT_WAREHOUSE\",\"shippingOptions\":null,\"carrierMethod\":\"\",\"currency\":\"USD\",\"consignorDetails\":{\"consignorId\":\"ee00c1d4-9c25-5\",\"merchantTag\":null,\"pickUpInfo\":{\"customerAddressId\":null,\"contact\":{\"name\":{\"firstName\":\"ramanMechant 2\",\"lastName\":\"Warner\",\"middleName\":null,\"nickName\":null},\"phone\":\"R5wJgNioSTX2qFQlEyub0g\",\"email\":\"nike.merchant@maildrop.cc\"},\"address\":{\"unitNumber\":null,\"lineOne\":\"23423541\",\"lineTwo\":\"PEOPLES COLONY\",\"geographicLocation\":null,\"street\":\"RAJAN\",\"poBox\":null,\"city\":\"Zastron\",\"country\":\"South Africa\",\"zip\":\"9950\",\"region\":\"Free State\",\"addressType\":\"PICKUP\",\"suburb\":\"Nuwe Lokasie\",\"suburbId\":null,\"orderType\":null}}},\"warehouseInfo\":{\"warehouseId\":\"149091_ORACLE\",\"labelName\":null,\"name\":null,\"providerName\":null},\"parcelDetails\":{\"parcelConfigs\":[{\"unitOfMeasure\":\"container\",\"measurementValue\":\"40 feet\"}],\"attributeData\":[{\"attributeName\":\"multipleSkuPerBox\",\"attributeValue\":\"true\"},{\"attributeName\":\"oneSkuPerBox\",\"attributeValue\":\"false\"}]},\"lineDates\":{\"expectedShipDate\":\"2024-03-07\"},\"fulfillmentLines\":{\"totalLineQty\":10,\"orderLineDetails\":[{\"fulfillmentLineId\":1,\"refId\":null,\"itemDetails\":{\"inventoryId\":\"A126-F200229620C31629\",\"barcode\":\"TESTVENREY\",\"weight\":null,\"volume\":null,\"action\":null,\"quantity\":{\"orderQty\":10,\"unitOfMeasure\":\"EA\",\"measurementValue\":\"10\"},\"packingConfig\":{\"labeling\":false,\"bubbleWrapping\":false,\"bagging\":false,\"bubbleMail\":false},\"shnId\":null,\"issue\":null,\"sellerAction\":null}}]},\"boxInfo\":null,\"additionalAttributes\":[{\"attributeType\":\"ORDER_ATTRIBUTES\",\"attributeData\":[{\"attributeName\":\"priorityInbound\",\"attributeValue\":\"false\"}]}]}"
}
```

400
```json
{
  "timestamp": "2024-03-07T08:52:27.948066",
  "errorReasonCode": "CREATE_DRAFT_RECEIVING_ORDER_BAD_REQUEST_EXCEPTION",
  "status": "BAD_REQUEST",
  "message": "No draft orders found",
  "requestId": "65e9804bec4f686a2b925b09c22ab253",
  "errors": [
    "BAD_REQUEST_EXCEPTION"
  ]
}
```

417
```json
{
  "timestamp": "2024-03-07T08:52:48.884405",
  "errorReasonCode": null,
  "status": "EXPECTATION_FAILED",
  "message": "Required request header 'languageCode' for method parameter type String is not present",
  "requestId": "65e98060bf547548f698a5242a6bd33d",
  "errors": [
    "INVENTORY_EVENT_EXCEPTION"
  ]
}
```

### Draft RO Listing API
- **Description**:This API is used to fetch all the draft inbounds based on filters
- **Rest URL**: {DNS}/api/v1/ims/ro/draft-orders
- **Verb**: GET
#### Request Param
limit, page, sortOn, direction,sellerId,searchParam

|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|limit|Number of elemnts in one page|Integer|No|10|
|page|Page Number|Integer|No|3|
|sortOn|It will give you sorted response based on field you applied sorting|String|No|Value must be from the fields that are there in response only|
|direction|ASC, DESC|String|No|ASC, DSC|
|sellerId|SellerId of user who has created draft inbounds|String|Yes||
|searchParam|This field will fetch draft orders based on searchParam on OrderId|String|Yes|“1118”|

Curl 
```bash
curl --location 'localhost:8080/api/ims/v1/ro/draft-orders?sellerId=4cf19e27-3fe0-5&limit=5&page=1&sortOn=fulfillmentCenter&direction=ASC&searchParam=1118' \
--header 'languageCode: en'
```
#### Response
200
```json
{
  "orderResponses": [
    {
      "orderId": "DRAFT-RO-11000001118",
      "sellerId": "4cf19e27-3fe0-5",
      "createdOn": "2023-12-13T10:14:56.000+00:00",
      "updatedAt": "2023-12-13T10:14:56.000+00:00",
      "poNbr": null,
      "fulfillmentCenter": "EUROPE",
      "warehouseId": "148796_ORACLE",
      "orderStatus": "CREATED",
      "subOrderType": "DEFAULT",
      "manifestLink": "NA"
    }
  ],
  "totalElements": 1,
  "status": true
}
```

400
```json
{
  "timestamp": "2024-03-07T09:10:27.353116",
  "errorReasonCode": null,
  "status": "BAD_REQUEST",
  "message": "BadRequestProvided: ",
  "requestId": "65e984838206f58107a72556956984a2",
  "errors": [
    "Required request parameter 'sellerId' for method parameter type String is not present"
  ]
}
```

417
```json
{
  "timestamp": "2024-03-07T09:11:07.361941",
  "errorReasonCode": null,
  "status": "EXPECTATION_FAILED",
  "message": "Required request header 'languageCode' for method parameter type String is not present",
  "requestId": "65e984ab1d674099ae64b3facdc65db3",
  "errors": [
    "INVENTORY_EVENT_EXCEPTION"
  ]
}
```

### Cancel RO API
- **Description**: This API is used to cancel order that is in state which can be cancelled
- **Rest URL**: {DNS}/api/v1/ims/inventory/cancel-order

#### Request Param 
|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|orderId|OrderId of order that user want to cancel|String|Yes|“orderId”|
|orderType|Type of order that user want to cancel|String|Yes|“RECEIVING_ORDER”|
|sellerId|SellerId of user who has created order|String|Yes|“sellerId”|

#### Response
200
```json
{
  "message": "Cancel Order Successfully"
}
```

400
```json
{
  "timestamp": "2024-03-07T09:25:06.078617",
  "errorReasonCode": null,
  "status": "BAD_REQUEST",
  "message": "BadRequestProvided: ",
  "requestId": "65e987f12f8fba4c7c2844a2462714c2",
  "errors": [
    "Required request parameter 'orderId' for method parameter type String is not present"
  ]
}
```

417
```json
{
  "timestamp": "2024-03-07T09:25:25.254235",
  "errorReasonCode": null,
  "status": "EXPECTATION_FAILED",
  "message": "Required request header 'languageCode' for method parameter type String is not present",
  "requestId": "65e988058e6ca8b39a32aace6567fd73",
  "errors": [
    "INVENTORY_EVENT_EXCEPTION"
  ]
}
```

## Save Stock Hold Notes API

Encountering On-Hold receiving orders may result from two common reasons:

1. **Unknown SKU**:
   Unknown SKUs present challenges that may require attached documents or images, making the `url` field invaluable. Administrators have the ability to create or update SKUs, inventory IDs, or barcodes based on existing records. Products can also be identified using barcodes.

2. **Excess Units**:
   In cases of excess units, the inventory ID or SKU is typically already identified.

To resolve the On-Hold status, users must create a new receiving order using the provided API endpoint (`RO Create API`). Once pending seller actions are addressed, a new receiving order will become visible in the UI, and the corresponding action will be marked as closed.

### Save Stock Hold Note API (On Hold details)
- **Description**: This API creates and updates stock hold notes for a particular Receiving order.
- **URL**: /api/ims/v1/ro/save-stock-notes
- **Verb**: PUT

#### Request  
```json
{
  "receivingOrderID": "DPW-RO-10000000818",
  "pendingSellerActions": [
    {
      "stockHoldId": "SH789012",
      "shnUiId": "DPW-SHN-1",
      "issues": "Unknown SKU",
      "unitsVariance": 2,
      "action": "Inward as sellable",
      "inventoryId": "DPW-A001-SDF432",
      "url": "https://example.com/product-image",
      "sku": "SKU789012",
      "barcode": "1234567890123"
    }
  ]
}
```

|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|receivingOrderID|Receiving Order created initially|String|Yes|DPW-RO-10000000818|


|Field|Desc|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|stockHoldId|Problem Id on Warehouse|<p>String</p><p></p>||SH789012|
|shnUiId|SHN ID shown on UI|<p>String</p><p></p>||DPW-SHN-1|
|issues|Reason for On-HOLD|<p>String</p><p></p>||(Unknown SKU/ Excess units)|
|unitsVariance|Number of units received|<p>Integer</p><p></p>||20|
|action|Status of SHN|<p>String</p><p></p>||(Inward as sellable/ Move to unsellable Inventory)|
|inventoryId||<p>String</p><p></p>||DPW-A001-SDF432|
|url|In case of unknown sku, url of document/Image|<p>String</p><p></p>|||
|sku|Sku at warehouse|||SKU789012|
|barcode|Barcode of product|||1234567890123|

Curl 
```bash
curl -X 'PUT' \ 
  'https://ecom-qa-ims.dpworld.com/api/ims/v1/ro/save-stock-notes' \ 
  -H 'accept: application/json' \ 
  -H 'Content-Type: application/json' \ 
  -d '{ 
  "receivingOrderID": "DPW-RO-10000000818", 
  "pendingSellerActions": [ 
    { 
      "stockHoldId": "SH789012", 
      "shnUiId": "DPW-SHN-1", 
      "issues": "Unknown SKU", 
      "unitsVariance": 2, 
      "taggedNewFOId": "FO123456", 
      "action": "Inward as sellable", 
      "inventoryId": "DPW-A001-SDF432", 
      "url": "https://example.com/product-image", 
      "sku": "SKU789012", 
      "barcode": "1234567890123" 
    } 
  ] 
} 
'
```

#### Response
200 
```json
{
  "data": {
    "status": true
  },
  "message": "Success",
  "httpStatus": "OK",
  "requestId": "65e7fd2f884dc26c91dcc45ab136ad8e"
}
```

400
```json
{
  "timestamp": "2024-03-06T05:21:28.328138256",
  "errorReasonCode": "UPDATE_RECEIVING_ORDER_BAD_REQUEST_EXCEPTION",
  "status": "BAD_REQUEST",
  "message": "receivingOrderId is NULL",
  "requestId": "65e7fd5852556ad23b0bf0e7ceaaeec6",
  "errors": [
    "BAD_REQUEST_EXCEPTION"
  ]
}
```

404
```json
{
  "timestamp": "2024-03-06T05:21:57.234943627",
  "errorReasonCode": null,
  "status": "NOT_FOUND",
  "message": "Resource not found",
  "requestId": "65e7fd75b08dc8bcce0ae9dc7db2aef0",
  "errors": [
    "Error occurred while updating StockHoldNotes "
  ]
}
```

### Get onhold inventories
- **Description**: This API retrieves the complete list of Receiving Orders with a current status of ON-HOLD.
- **URL**: /ims/v1/ro/on-hold-inventories
- **Verb**: GET

#### Request
Curl 
```bash
curl --location 'http://ecom-qa-ims.dpworld.com/api/ims/v1/ro/on-hold-inventories' 
```

#### Response 
200
```json
[
  "DPW-RO-10000000820",
  "DPW-RO-10000000823",
  "DPW-RO-10000000824",
  "DPW-RO-10000000825",
  "DPW-RO-10000000829"
]
```

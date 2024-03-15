

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

- **Description**: - This API is used to fetch Inbound details  
- **Verb**: - GET      
- **URL**: - /api/v1/ims/ro/receving-orders/{orderId} 
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

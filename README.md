

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

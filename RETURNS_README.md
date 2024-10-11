# Returns
Returns are an integral part of the order fulfillment process, allowing customers to return products for various reasons. There are two primary types of returns: Manual Return RVP (Return Vendor Pickup) and automatic return on Return To Origin by courier RTO.

## Types of Returns
- **Manual Return RVP (Return Vendor Pickup)**:
In this type of return, the customer initiates the return process, and the vendor arranges for the pickup of the returned items.
- **Automatic Return on Return To Origin by Courier (RTO)**:
Returns are automatically initiated when a courier is unable to deliver the shipment to the customer and marks it for return to the origin.

## Shipment Types
Returns can be associated with two types of shipments:
- **DPW_SHIPPING** : Courier pickup: The return items are collected by the courier from the customer's location.
- **DROP_AT_WAREHOUSE**: The customer drops off the return items at a designated warehouse location.

## Return Actions
While creating a return, users can specify the action to be taken on the returned products. Two common actions are:
- **Restock**: The returned products are restocked back into inventory for future sale.
- **Disposed**: The returned products are disposed of or marked for disposal due to damage or other reasons.

## Return Statuses
| Status              | Description                                                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------|
| CREATED                  | Return has been created.                                                                                               |
| AWAITING_ARRIVAL         | Processing, Inbound has been created.                                                                                  |
| COLLECTED_BY_COURIER     | Processing, Once a return is picked up by courier.                                                                     |
| OUT_FOR_DELIVERY         | Processing, Once a return is out for delivery by courier.                                                               |
| DELIVERED                | Processing, Once a return is delivered by the courier.                                                                 |
| COMPLETED                | Completed, Once a return is inbounded successfully into the Warehouse, as confirmed by PN.                             |
| COMPLETED_WITH_VARIANCE  | Completed, Once a return is inbounded successfully into the Warehouse with Variance as confirmed by PN.               |
| UNRECOVERABLE            | Failed, Courier is unrecoverable as marked by the Courier.                                                              |
| COURIER_CANCELLED        | Failed, Courier is cancelled as marked by the Courier.                                                                  |
| FAILED_RETURN_DELIVERY   | Failed, Courier is not able to deliver to warehouse as marked by the courier.                                           |
| RETURN_TO_ORIGIN         | Failed, Courier is being returned to origin/Sender as marked by courier.                                               |
| CANCELLED                | Failed, Return is cancelled by the Seller.                                                                             |

### Create a Return
Create a return order
- **Verb**: POST
- **Path**: /v1/return/place-return
#### Request
```json
{
  "buId": "5cb23705-2667-7",
  "rmaId": "#1007",
  "orderId": "OMS-10000011006",
  "currency": "EURO",
  "orderType": "RETURN",
  "pickupFrom": {
    "id": 2584,
    "address": {
      "zip": "2196",
      "city": null,
      "state": null,
      "region": null,
      "street": null,
      "suburb": "Johannesburg",
      "country": "South Africa",
      "lineOne": "86 11th Street, Parkmore, Sandton",
      "lineTwo": ""
    },
    "contact": {
      "name": {
        "lastName": "David",
        "nickName": null,
        "firstName": "Warner",
        "middleName": null
      },
      "email": "daveid@gmail.com",
      "phone": "763567802",
      "countryCode": null
    }
  },
  "customerType": "CONSUMER",
  "orderPlacedAt": 1707955200000,
  "orderSourceId": "WAREHOUSE_UK",
  "parentOrderId": "10000010977",
  "orderChannelId": "WAREHOUSE_UK",
  "fulfillmentType": "DPW_FULFILLMENT",
  "shippingDetails": {
    "shippingType": "DPW_SHIPPING",
    "shippingOption": "CHEAPEST",
    "fulfillmentCenter": "PN_WAREHOUSE_1_WAREHOUSE_UK"
  },
  "consigneeOrderId": null,
  "fulfillmentLines": {
    "currencyUnit": "EURO",
    "totalLineQty": 1,
    "orderLineDetails": [
      {
        "notes": null,
        "quantity": {
          "unitOfMeasure": "EA",
          "measurementValueInDouble": 1.0
        },
        "itemDetails": {
          "barcode": "2302001130",
          "sellerId": "5cb23705-2667-7",
          "inventoryId": "SCW/OSFA"
        },
        "returnAction": "RESTOCK",
        "fulfillmentLineId": 1,
        "lineOrderPlacedAt": 1707955200000
      }
    ]
  },
  "parentShipmentId": "SHP-10000010959",
  "orderCreationType": "SFS_PORTAL"
}
```
| Field              | Description                                           | Data Type    | Mandatory | Example                      |
|--------------------|-------------------------------------------------------|--------------|-----------|------------------------------|
| buId               | Business unit ID                                      | String       | Yes       | "5cb23705-2667-7"            |
| rmaId              | Return merchandise authorization ID                   | String       | No        | "#1007"                      |
| orderId            | Order ID                                              | String       | Yes       | "OMS-10000011006"            |
| currency           | Currency                                              | String       | Yes       | "EURO"                        |
| orderType          | Type of order (e.g., RETURN)                          | String       | Yes       | "RETURN"                     |
| pickupFrom         | Details of the pickup location                        | Object       | Yes       | See below                    |
| customerType       | Type of customer (e.g., CONSUMER)                    | String       | Yes       | "CONSUMER"                   |
| orderPlacedAt      | Timestamp when the order was placed                   | Long         | Yes       | 1707955200000                |
| orderSourceId      | Identifier for the order source                      | String       | Yes       | "WAREHOUSE_UK"               |
| parentOrderId      | ID of the parent order                                | String       | Yes       | "10000010977"                |
| orderChannelId     | Identifier for the order channel                     | String       | Yes       | "WAREHOUSE_UK"               |
| fulfillmentType    | Type of fulfillment                                   | String       | Yes       | "DPW_FULFILLMENT"            |
| shippingDetails    | Details of the shipping                               | Object       | Yes       | See below                    |
| consigneeOrderId   | ID of the consignee order                             | String       | No        | null                         |
| fulfillmentLines   | Details of the fulfillment lines                      | Object       | Yes       | See below                    |
| parentShipmentId   | ID of the parent shipment                             | String       | Yes       | "SHP-10000010959"            |
| orderCreationType  | Type of order creation                                | String       | Yes       | "SFS_PORTAL"                 |

### pickupFrom:
| Field    | Description                               | Data Type | Mandatory | Example                                  |
|----------|-------------------------------------------|-----------|-----------|------------------------------------------|
| id       | Identifier for the pickup location        | Integer   | Yes       | 2584                                     |
| address  | Details of the pickup location's address | Object    | Yes       | See below                                |
| contact  | Contact details                           | Object    | Yes       | See below                                |

#### address:
| Field                | Description                    | Data Type | Mandatory | Example                      |
|----------------------|--------------------------------|-----------|-----------|------------------------------|
| zip                  | ZIP code                       | String    | Yes       | "2196"                       |
| city                 | City name                      | String    | No        | null                         |
| state                | State name                     | String    | No        | null                         |
| region               | Region name                    | String    | No        | null                         |
| street               | Street name                    | String    | No        | null                         |
| suburb               | Suburb name                    | String    | Yes       | "Johannesburg"               |
| country              | Country name                   | String    | Yes       | "South Africa"               |
| lineOne              | Address line 1                 | String    | Yes       | "86 11th Street, Parkmore, Sandton" |
| lineTwo              | Address line 2                 | String    | No        | ""                           |

#### contact:
| Field    | Description          | Data Type | Mandatory | Example       |
|----------|----------------------|-----------|-----------|---------------|
| name     | Name of the contact | Object    | Yes       | See below     |
| email    | Email address       | String    | Yes       | "daveid@gmail.com" |
| phone    | Phone number        | String    | Yes       | "763567802"   |

##### name:
| Field       | Description     | Data Type | Mandatory | Example  |
|-------------|-----------------|-----------|-----------|----------|
| lastName    | Last name       | String    | Yes       | "David"  |
| nickName    | Nickname        | String    | No        | null     |
| firstName   | First name      | String    | Yes       | "Warner" |
| middleName  | Middle name     | String    | No        | null     |

### shippingDetails:
| Field             | Description                   | Data Type | Mandatory | Example                           |
|-------------------|-------------------------------|-----------|-----------|-----------------------------------|
| shippingType      | Type of shipping              | String    | Yes       | "DPW_SHIPPING"                   |
| shippingOption    | Shipping option               | String    | Yes       | "CHEAPEST"                       |
| fulfillmentCenter | Fulfillment center            | String    | Yes       | "PN_WAREHOUSE_1_WAREHOUSE_UK"    |

### fulfillmentLines:
| Field               | Description                               | Data Type | Mandatory | Example                      |
|---------------------|-------------------------------------------|-----------|-----------|------------------------------|
| currencyUnit        | Currency                                  | String    | Yes       | "EURO"                        |
| totalLineQty        | Total quantity of fulfillment lines       | Integer   | Yes       | 1                            |
| orderLineDetails    | Details of each fulfillment line          | Array     | Yes       | See below                    |

#### orderLineDetails:
| Field               | Description                              | Data Type | Mandatory | Example                         |
|---------------------|------------------------------------------|-----------|-----------|---------------------------------|
| notes               | Additional notes                         | String    | No        | null                            |
| quantity            | Quantity details                         | Object    | Yes       | See below                       |
| itemDetails         | Details of the item                      | Object    | Yes       | See below                       |
| returnAction        | Action for the return                    | String    | Yes       | "RESTOCK/DISPOSE"                       |
| fulfillmentLineId   | Fulfillment line ID                      | Integer   | Yes       | 1                               |
| lineOrderPlacedAt   | Timestamp when the line order was placed | Long      | Yes       | 1707955200000                   |

##### quantity:
| Field                   | Description                   | Data Type | Mandatory | Example             |
|-------------------------|-------------------------------|-----------|-----------|---------------------|
| unitOfMeasure           | Unit of measure               | String    | Yes       | "EA"                |
| measurementValueInDouble| Quantity in double            | Double

#### Response
```json
{
  "data": {
    "orderId": "string"
  },
  "message": "string",
  "httpStatus": "100 CONTINUE"
}
```

### Returns List
- **Verb**: POST
- **Path**: /v2/return/returns?limit=20&page=0&sortOn=shipmentId&direction=DESC

#### QueryParams
|**Field**|**Type**|**Default Value**|**Comments**|
| :- | :- | :- | :-: |
|limit|Integer|20| |
|<p>page</p><p> </p>|Integer|0|Starts with 0|
|<p>sortOn</p><p> </p>|String |shipmentId|<p>Accepted values: [orderId, returnId, sourceStore, orderDate,fulfillmentCentre, returnStatus, returnSubStatus]</p>|
|<p>direction</p><p> </p>|String|DESC|Case ignored; order will be “desc” if input is “desc” otherwise “asc”|

#### Request
```json
{
  "returnsStatuses": [
    "CREATED"
  ],
  "startDate": "2024-03-17T06:36:04.727Z",
  "endDate": "2024-03-17T06:36:04.727Z",
  "fulfillmentCentre": [
    "string"
  ],
  "search": "string"
}
```

|**Fields**|**Type**|**Description**|**Example**|
| :- | :- | :- | :- |
|search|String|Pattern matching  order\_id, return_id, RMA| |
|startDate|LocalDateTime|Filter on ordered\_at including startDate|"2024-03-06T08:48:36.643Z"|
|endDate|LocalDateTime|Filter on ordered\_at including endDate|"2024-03-06T08:48:36.643Z"|
|returnsStatuses|Array|List of shipment statuses|[“COMPLETED”, “PICKED”]|
|fulfillmentCentre|Array|List of warehouses (fulfillment\_center)|["PN\_WAREHOUSE\_1\WAREHOUSE\_UK"]|

#### Response
```json
{
    "data": {
        "returns": [
            {
                "returnId": "RET-10000010959-1",
                "orderId": "OMS-10000011006",
                "sourceStore": "5cb23705-2667-7",
                "orderDate": "2024-02-15T00:00:00.000+00:00",
                "fulfillmentCentre": "PN_WAREHOUSE_1_WAREHOUSE_UK",
                "returnStatus": "DELIVERED",
                "returnSubStatus": null,
                "rmaId": "#1007",
                "parentShipmentId": "SHP-10000010959",
                "parentOrderId": "10000010977",
                "trackingId": "OPT-320204834"
            },
            {
                "returnId": "RET-10000010924-1",
                "orderId": "OMS-10000010979",
                "sourceStore": "5cb23705-2667-7",
                "orderDate": "2024-02-14T00:00:00.000+00:00",
                "fulfillmentCentre": "PN_WAREHOUSE_1_WAREHOUSE_UK",
                "returnStatus": "DELIVERED",
                "returnSubStatus": null,
                "rmaId": null,
                "parentShipmentId": "SHP-10000010924",
                "parentOrderId": "10000010942",
                "trackingId": "OPT-070294653"
            },
            {
                "returnId": "RET-10000000804-1",
                "orderId": "OMS-10000009790",
                "sourceStore": "5cb23705-2667-7",
                "orderDate": "2024-01-30T00:00:00.000+00:00",
                "fulfillmentCentre": "PN_WAREHOUSE_1_WAREHOUSE_UK",
                "returnStatus": "DELIVERED",
                "returnSubStatus": null,
                "rmaId": "#1003",
                "parentShipmentId": "SHP-10000000804",
                "parentOrderId": "10000000816",
                "trackingId": "OPT-659594417"
            },
            {
                "returnId": "RET-10000000808-1",
                "orderId": "OMS-10000009688",
                "sourceStore": "5cb23705-2667-7",
                "orderDate": "2024-01-25T00:00:00.000+00:00",
                "fulfillmentCentre": "PN_WAREHOUSE_1_WAREHOUSE_UK",
                "returnStatus": "CANCELLED",
                "returnSubStatus": null,
                "rmaId": "#1004",
                "parentShipmentId": "SHP-10000000808",
                "parentOrderId": "10000000820",
                "trackingId": null
            },
            {
                "returnId": "RET-10000000808-2",
                "orderId": "OMS-10000009698",
                "sourceStore": "5cb23705-2667-7",
                "orderDate": "2024-01-25T00:00:00.000+00:00",
                "fulfillmentCentre": "PN_WAREHOUSE_1_WAREHOUSE_UK",
                "returnStatus": "DELIVERED",
                "returnSubStatus": null,
                "rmaId": null,
                "parentShipmentId": "SHP-10000000808",
                "parentOrderId": "10000000820",
                "trackingId": null
            }
        ],
        "pageDetails": {
            "totalCount": 5
        }
    },
    "message": "Success",
    "httpStatus": "OK"
}
```

### Get Return Order
Get a specific return order using the orderId
- **Method**: GET
- **Path**: - /v1/order/{orderId}
  
#### Response
```json
{
  "data": {
    "orderId": "string",
    "fulfillmentOrderId": 0,
    "orderChannelId": "3PE",
    "orderSourceId": "DUBUY",
    "buId": "Nike.com",
    "orderCreationType": "AssistedChannel",
    "orderType": "string",
    "customerType": "string",
    "customerInfo": {
      "customerReference": "WH001",
      "customerAccountId": "ACC123",
      "customerFullName": "XYZ Pharmacy"
    },
    "consigneeOrderId": "string",
    "orderPlacedAt": "2024-03-17T06:19:42.816Z",
    "shippingMethod": "EXPEDITED",
    "carrierMethod": "string",
    "customerLanguageId": 0,
    "fulfillmentType": "DPW_FULFILLMENT",
    "currency": "string",
    "fulfillmentLines": {
      "totalLineQty": 0,
      "currencyUnit": "string",
      "country": "string",
      "lineTotal": {
        "currencyAmount": "100.0",
        "currencyUnit": "USD"
      },
      "orderLineDetails": [
        {
          "id": 0,
          "fulfillmentLineId": 0,
          "lineOrderPlacedAt": "2024-03-17T06:19:42.816Z",
          "lineOrderStatus": "string",
          "shippingMethod": "EXPEDITED",
          "shippingDetail": {
            "shippingType": "DPW_SHIPPING",
            "shippingOption": "CHEAPEST",
            "shippingMethod": "Super Fast",
            "fulfillmentCenter": "Joberg, South Africa",
            "quoteId": "Q12345",
            "courierName": "FedEx"
          },
          "quantity": {
            "unitOfMeasure": "string",
            "measurementValueInDouble": 0
          },
          "itemDetails": {
            "itemId": "123456",
            "sku": "SKU123",
            "variantId": "VARIANT789",
            "itemType": "PHYSICAL",
            "sellerId": "SELLER123",
            "upc": "123456789012",
            "gtin": "GTIN123",
            "itemDesc": "High-quality T-shirt",
            "itemUrl": "https://example.com/item123",
            "offerId": "OFFER456",
            "externalRefId": "REF456",
            "inventoryId": "INV12345",
            "itemAttributes": {
              "height": "10",
              "length": "20",
              "width": "15",
              "weight": "1",
              "depth": "1",
              "vnpkQty": "10",
              "whpkQty": "5"
            },
            "quantity": {
              "unitOfMeasure": "string",
              "measurementValue": 0,
              "measurementValueInDouble": 0
            },
            "requestedQuantity": {
              "unitOfMeasure": "string",
              "measurementValue": 0,
              "measurementValueInDouble": 0
            },
            "status": "string"
          },
          "lineDates": {
            "id": 0,
            "minDeliveryDate": "2024-03-17T06:19:42.816Z",
            "maxDeliveryDate": "2024-03-17T06:19:42.816Z",
            "orderProcessingDate": "2024-03-17T06:19:42.816Z",
            "preciseDeliveryDate": "2024-03-17T06:19:42.816Z",
            "expectedShipDate": "2024-03-17T06:19:42.816Z"
          },
          "chargeDetails": [
            {
              "id": 0,
              "chargeCategory": "PRODUCT",
              "chargeName": "string",
              "currencyAmount": "string"
            }
          ],
          "notes": [
            {
              "commentType": "SellerNote",
              "comment": "Please pack items securely."
            }
          ]
        }
      ],
      "additionalAttributes": [
        {
          "attributeType": "string",
          "attributeData": [
            {
              "id": 0,
              "attributeName": "string",
              "attributeValue": "string"
            }
          ]
        }
      ]
    },
    "lineDates": {
      "id": 0,
      "minDeliveryDate": "2024-03-17T06:19:42.816Z",
      "maxDeliveryDate": "2024-03-17T06:19:42.816Z",
      "orderProcessingDate": "2024-03-17T06:19:42.816Z",
      "preciseDeliveryDate": "2024-03-17T06:19:42.816Z",
      "expectedShipDate": "2024-03-17T06:19:42.816Z"
    },
    "shippingTo": {
      "id": 0,
      "contact": {
        "contactId": 0,
        "name": {
          "customerInfoId": 0,
          "firstName": "string",
          "lastName": "string",
          "middleName": "string",
          "nickName": "string"
        },
        "phone": "string",
        "countryCode": "string",
        "email": "string"
      },
      "address": {
        "unitNumber": "Apt 4B",
        "lineOne": "123 Main St",
        "lineTwo": "Apt 4B",
        "geographicLocation": "string",
        "street": "Maple Avenue",
        "city": "New York",
        "state": "NY",
        "country": "USA",
        "zip": "10001",
        "suburb": "Downtown",
        "addressType": "Residential",
        "latitude": "45.41634",
        "longitude": "-75.6868",
        "companyId": "12345",
        "locationId": "1234"
      }
    },
    "totalChargeDetails": [
      {
        "id": 0,
        "chargeCategory": "PRODUCT",
        "chargeName": "string",
        "currencyAmount": "string"
      }
    ],
    "attachments": [
      {
        "documentId": 0,
        "documentOwner": "string",
        "documentOwnerId": "string",
        "documentName": "string",
        "documentCategory": "string",
        "documentSubCategory": "string",
        "documentLink": "string",
        "notes": "string",
        "createdAt": "2024-03-17T06:19:42.816Z",
        "createdBy": "string",
        "documentAttributes": [
          {
            "attributeName": "string",
            "attributeValue": "string"
          }
        ]
      }
    ],
    "paymentDetails": {
      "paymentType": "PRE_PAID",
      "status": "UNSPECIFIED_PAYMENT_STATUS",
      "amountPaid": 100,
      "payments": [
        {
          "id": 0,
          "paymentReferenceId": "PAY12345",
          "pg": "PayPal",
          "paymentMethod": "Credit Card",
          "transactionDate": "2023-08-09T12:34:56Z",
          "amount": 100,
          "status": "UNSPECIFIED_PAYMENT_STATUS"
        }
      ],
      "billTo": {
        "id": 0,
        "contact": {
          "contactId": 0,
          "name": {
            "customerInfoId": 0,
            "firstName": "string",
            "lastName": "string",
            "middleName": "string",
            "nickName": "string"
          },
          "phone": "string",
          "countryCode": "string",
          "email": "string"
        },
        "address": {
          "unitNumber": "Apt 4B",
          "lineOne": "123 Main St",
          "lineTwo": "Apt 4B",
          "geographicLocation": "string",
          "street": "Maple Avenue",
          "city": "New York",
          "state": "NY",
          "country": "USA",
          "zip": "10001",
          "suburb": "Downtown",
          "addressType": "Residential",
          "latitude": "45.41634",
          "longitude": "-75.6868",
          "companyId": "12345",
          "locationId": "1234"
        }
      }
    },
    "orderStatus": "string",
    "rmaId": "string",
    "parentOrderId": "string",
    "parentShipmentId": "string",
    "pickupFrom": {
      "id": 0,
      "contact": {
        "contactId": 0,
        "name": {
          "customerInfoId": 0,
          "firstName": "string",
          "lastName": "string",
          "middleName": "string",
          "nickName": "string"
        },
        "phone": "string",
        "countryCode": "string",
        "email": "string"
      },
      "address": {
        "unitNumber": "Apt 4B",
        "lineOne": "123 Main St",
        "lineTwo": "Apt 4B",
        "geographicLocation": "string",
        "street": "Maple Avenue",
        "city": "New York",
        "state": "NY",
        "country": "USA",
        "zip": "10001",
        "suburb": "Downtown",
        "addressType": "Residential",
        "latitude": "45.41634",
        "longitude": "-75.6868",
        "companyId": "12345",
        "locationId": "1234"
      }
    },
    "inventoryTypeSelection": "string"
  },
  "message": "string",
  "httpStatus": "100 CONTINUE"
}
```
### Get specific return using returnId
Get a specific return using the returnId of the return order
- **Method**: GET
- **Path**: - /v1/shipment/{returnId}
  
#### Response
```json
{
  "data": {
    "state": {
      "status": "string",
      "subStatus": "string",
      "orderType": "string",
      "previousStatus": "string",
      "shippingType": "DPW_SHIPPING",
      "isAllReturned": true
    },
    "cardList": [
      {
        "cardId": "ACTIONS",
        "cardRank": 0,
        "actionList": [
          "string"
        ],
        "labelList": [
          {
            "additionalProp1": {},
            "additionalProp2": {},
            "additionalProp3": {}
          }
        ]
      }
    ],
    "orderItems": [
      {
        "itemId": "string",
        "itemUrl": "string",
        "itemDesc": "string",
        "quantity": 0,
        "sku": "string",
        "variantId": "string",
        "itemType": "string",
        "externalRefId": "string",
        "inventoryId": "string",
        "fulfillmentLineId": 0,
        "itemSelectionCriteria": "string",
        "expiryStartDate": "2024-03-17T06:24:04.686Z",
        "expiryEndDate": "2024-03-17T06:24:04.686Z",
        "batchDetails": "string",
        "returnAction": "string",
        "actionTaken": "string",
        "reason": "string",
        "sellerId": "string",
        "omsItemId": "string",
        "barcode": "string",
        "returnQuantity": 0
      }
    ],
    "orderDetail": {
      "orderId": "string",
      "customerType": "string",
      "sourceStore": "string",
      "orderValueCurrency": "string",
      "orderValue": 0,
      "store": "string",
      "orderPlacedOn": "2024-03-17T06:24:04.686Z",
      "orderStatus": "string",
      "orderType": "string",
      "rmaId": "string",
      "parentOrderId": "string",
      "parentShipmentId": "string",
      "consigneeOrderId": "string",
      "inventoryTypeSelection": "string"
    },
    "paymentDetail": {
      "paymentType": "PRE_PAID",
      "status": "UNSPECIFIED_PAYMENT_STATUS",
      "amountPaid": 100,
      "payments": [
        {
          "id": 0,
          "paymentReferenceId": "PAY12345",
          "pg": "PayPal",
          "paymentMethod": "Credit Card",
          "transactionDate": "2023-08-09T12:34:56Z",
          "amount": 100,
          "status": "UNSPECIFIED_PAYMENT_STATUS"
        }
      ],
      "billTo": {
        "id": 0,
        "contact": {
          "contactId": 0,
          "name": {
            "customerInfoId": 0,
            "firstName": "string",
            "lastName": "string",
            "middleName": "string",
            "nickName": "string"
          },
          "phone": "string",
          "countryCode": "string",
          "email": "string"
        },
        "address": {
          "unitNumber": "Apt 4B",
          "lineOne": "123 Main St",
          "lineTwo": "Apt 4B",
          "geographicLocation": "string",
          "street": "Maple Avenue",
          "city": "New York",
          "state": "NY",
          "country": "USA",
          "zip": "10001",
          "suburb": "Downtown",
          "addressType": "Residential",
          "latitude": "45.41634",
          "longitude": "-75.6868",
          "companyId": "12345",
          "locationId": "1234"
        }
      }
    },
    "contactInfo": {
      "id": 0,
      "contact": {
        "contactId": 0,
        "name": {
          "customerInfoId": 0,
          "firstName": "string",
          "lastName": "string",
          "middleName": "string",
          "nickName": "string"
        },
        "phone": "string",
        "countryCode": "string",
        "email": "string"
      },
      "address": {
        "unitNumber": "Apt 4B",
        "lineOne": "123 Main St",
        "lineTwo": "Apt 4B",
        "geographicLocation": "string",
        "street": "Maple Avenue",
        "city": "New York",
        "state": "NY",
        "country": "USA",
        "zip": "10001",
        "suburb": "Downtown",
        "addressType": "Residential",
        "latitude": "45.41634",
        "longitude": "-75.6868",
        "companyId": "12345",
        "locationId": "1234"
      }
    },
    "attachments": [
      {
        "documentId": 0,
        "documentOwner": "string",
        "documentOwnerId": "string",
        "documentName": "string",
        "documentCategory": "string",
        "documentSubCategory": "string",
        "documentLink": "string",
        "notes": "string",
        "createdAt": "2024-03-17T06:24:04.686Z",
        "createdBy": "string",
        "documentAttributes": [
          {
            "attributeName": "string",
            "attributeValue": "string"
          }
        ]
      }
    ],
    "shipmentDetail": {
      "shippingType": "DPW_SHIPPING",
      "shippingOption": "CHEAPEST",
      "shippingMethod": "Super Fast",
      "fulfillmentCenter": "Joberg, South Africa",
      "quoteId": "Q12345",
      "courierName": "FedEx"
    },
    "additionalAttributes": [
      {
        "attributeType": "string",
        "attributeData": [
          {
            "id": 0,
            "attributeName": "string",
            "attributeValue": "string"
          }
        ]
      }
    ],
    "remarkResponses": [
      {
        "remarkOwner": "string",
        "remarkOwnerId": "string",
        "remarkCategory": "string",
        "message": "string",
        "createdAt": "2024-03-17T06:24:04.686Z",
        "createdBy": "string"
      }
    ],
    "pickupInfo": {
      "id": 0,
      "contact": {
        "contactId": 0,
        "name": {
          "customerInfoId": 0,
          "firstName": "string",
          "lastName": "string",
          "middleName": "string",
          "nickName": "string"
        },
        "phone": "string",
        "countryCode": "string",
        "email": "string"
      },
      "address": {
        "unitNumber": "Apt 4B",
        "lineOne": "123 Main St",
        "lineTwo": "Apt 4B",
        "geographicLocation": "string",
        "street": "Maple Avenue",
        "city": "New York",
        "state": "NY",
        "country": "USA",
        "zip": "10001",
        "suburb": "Downtown",
        "addressType": "Residential",
        "latitude": "45.41634",
        "longitude": "-75.6868",
        "companyId": "12345",
        "locationId": "1234"
      }
    },
    "packInfo": {
      "StoreName": "string",
      "EmployeeId": "string",
      "PackCreatedDate": "2024-03-17T06:24:04.686Z",
      "PackStartedDate": "2024-03-17T06:24:04.686Z",
      "PackFinishedDate": "2024-03-17T06:24:04.686Z",
      "LatestDateStarted": "2024-03-17T06:24:04.686Z",
      "PackStarted": true,
      "PackFinished": true,
      "StoreId": "string",
      "Boxes": [
        {
          "BoxId": "string",
          "BoxType": "string",
          "BoxDimensions": {
            "Length": 0,
            "Width": 0,
            "Height": 0,
            "Weight": 0
          },
          "BoxBarcode": "string",
          "Products": [
            {
              "ItemId": "string",
              "Description": "string",
              "Sku": "string",
              "Quantity": 0,
              "CaptureSerial": true,
              "CaptureIMEI": true,
              "Length": 0,
              "Width": 0,
              "Height": 0,
              "Weight": 0,
              "Volume": 0,
              "TotalVolume": 0
            }
          ],
          "PackingMaterials": [
            "string"
          ]
        }
      ],
      "ForCollection": true,
      "WarehouseId": "string",
      "WarehouseName": "string"
    },
    "deliveryInfo": {
      "customer": "string",
      "contactNo": "string",
      "email": "string",
      "companyName": "string",
      "addressLine1": "string",
      "addressLine2": "string",
      "suburb": "string",
      "postalCode": "string",
      "deliveryOption": {
        "deliveryQuoteId": "string",
        "nominatedServiceCode": "string",
        "courier": "string",
        "dispatchDate": "string",
        "deliveryStartDate": "string",
        "deliveryEndDate": "string",
        "businessDays": 0,
        "validUntil": "string",
        "chargeWeightKG": 0,
        "priceExVAT": 0,
        "specialServiceCode": 0
      },
      "dispatchDate": "string",
      "arrivalDate": "string",
      "estimatedArrivalDate": "string",
      "forCollection": true,
      "trackingNo": "string",
      "trackingUrl": "string",
      "trackingSignedBy": "string",
      "podImgUrl": "string",
      "courierName": "string",
      "traderPaid": true,
      "courierPaid": true,
      "status": {
        "message": "string",
        "timestamp": 0,
        "level": 0,
        "throwable": {
          "stackTrace": [
            {
              "classLoaderName": "string",
              "moduleName": "string",
              "moduleVersion": "string",
              "methodName": "string",
              "fileName": "string",
              "lineNumber": 0,
              "nativeMethod": true,
              "className": "string"
            }
          ],
          "message": "string",
          "suppressed": [
            {
              "stackTrace": [
                {
                  "classLoaderName": "string",
                  "moduleName": "string",
                  "moduleVersion": "string",
                  "methodName": "string",
                  "fileName": "string",
                  "lineNumber": 0,
                  "nativeMethod": true,
                  "className": "string"
                }
              ],
              "message": "string",
              "localizedMessage": "string"
            }
          ],
          "localizedMessage": "string"
        },
        "origin": {},
        "effectiveLevel": 0
      },
      "events": [
        {
          "message": "string",
          "timestamp": 0,
          "level": 0,
          "throwable": {
            "stackTrace": [
              {
                "classLoaderName": "string",
                "moduleName": "string",
                "moduleVersion": "string",
                "methodName": "string",
                "fileName": "string",
                "lineNumber": 0,
                "nativeMethod": true,
                "className": "string"
              }
            ],
            "message": "string",
            "suppressed": [
              {
                "stackTrace": [
                  {
                    "classLoaderName": "string",
                    "moduleName": "string",
                    "moduleVersion": "string",
                    "methodName": "string",
                    "fileName": "string",
                    "lineNumber": 0,
                    "nativeMethod": true,
                    "className": "string"
                  }
                ],
                "message": "string",
                "localizedMessage": "string"
              }
            ],
            "localizedMessage": "string"
          },
          "origin": {},
          "effectiveLevel": 0
        }
      ],
      "courierBillingInfo": {
        "boxList": [
          {
            "name": "string",
            "quantity": 0,
            "weight": 0
          }
        ],
        "cost": 0,
        "deliveryEndDate": "string",
        "deliveryStartDate": "string",
        "dispatchDate": "string",
        "region": "string",
        "service": {
          "code": "string",
          "description": "string",
          "workingDays": 0
        },
        "shippingWeight": 0
      },
      "totalBoxes": 0,
      "inboundReference": "string",
      "takealot": true,
      "bookingDate": "2024-03-17T06:24:04.686Z",
      "totes": [
        "string"
      ]
    },
    "warehouseDetails": {
      "id": 0,
      "label": "string",
      "name": "string",
      "warehouseId": "string",
      "actualWarehouseId": "string",
      "providerName": "string",
      "channelId": "string",
      "location": {
        "contact": {
          "name": {
            "firstName": "David",
            "lastName": "Warner",
            "middleName": "Andrew",
            "nickName": "Bull"
          },
          "countryCode": "+91",
          "phone": "234567210206",
          "unparsedPhoneNo": "string",
          "email": "david@yahoo.com"
        },
        "address": {
          "id": 0,
          "lineOne": "string",
          "lineTwo": "string",
          "street": "string",
          "poBox": "string",
          "city": "string",
          "state": "string",
          "country": "string",
          "zip": "string",
          "addressType": "string"
        }
      }
    },
    "dimsUom": {
      "weightUom": "string",
      "lengthUom": "string"
    },
    "returnReferences": [
      {
        "returnType": "string",
        "returnId": "string"
      }
    ],
    "boxLabels": "string",
    "items": [
      {
        "id": 0,
        "internalId": "string",
        "itemNo": "string",
        "serialNumbers": [
          "string"
        ],
        "name": "string",
        "imageURL": "string",
        "qty": 0,
        "dims": {
          "shippingWeightGrams": 0,
          "length": 0,
          "width": 0,
          "height": 0,
          "weight": 0
        },
        "specializedItemBarcode": "string",
        "barcode": "string",
        "allocateFromReserve": true,
        "receivedQty": 0,
        "instock": 0,
        "allocated": 0,
        "unallocated": 0,
        "onReorder": 0,
        "broken": 0,
        "reserved": 0,
        "stockItemId": 0,
        "clientStockItemId": "string",
        "status": {
          "code": 0,
          "timeStamp": "string",
          "description": "string"
        },
        "events": [
          {
            "code": 0,
            "timeStamp": "string",
            "description": "string"
          }
        ],
        "onHold": true,
        "forwardCover": 0,
        "startExpiryDate": "string",
        "endExpiryDate": "string",
        "lastReceivedBarcode": "string",
        "returnReason": "string",
        "returnDetail": "string",
        "virtualSku": "string",
        "warehouseName": "string",
        "lastModifiedDate": "2024-03-17T06:24:04.686Z",
        "requiredBatchNos": [
          "string"
        ],
        "packingSuggestion": "string",
        "costPrice": 0,
        "sellingPrice": 0,
        "captureSerial": true,
        "captureExpiry": true,
        "captureIMEI": true,
        "fromReserve": true,
        "dateAdded": "2024-03-17T06:24:04.686Z",
        "lastSoldDate": "2024-03-17T06:24:04.686Z",
        "lastReceivedDate": "2024-03-17T06:24:04.686Z",
        "inspect": true,
        "unsellable": true,
        "createdFromVirtual": true,
        "StoreSupplierId": "string",
        "warehouseId": "string"
      }
    ]
  },
  "message": "string",
  "httpStatus": "100 CONTINUE"
}
```

### Cancel Return
- **Method**: POST
- **Path**: - v1/return/{returnId}/cancel

#### Response
```json
{
  "data": true,
  "message": "string",
  "httpStatus": "100 CONTINUE"
}
```

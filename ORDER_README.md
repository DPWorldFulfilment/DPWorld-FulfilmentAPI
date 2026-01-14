# Orders
There are two types of orders that will be created by the system which will trigger outbounds from warehouses.  

1. **Customer Orders:** Standard consumer orders which are sent to OMS for fulfilment
1. **Supplier Orders:** Supplier orders are typically the orders triggered by the seller, where the seller wants the stock stored in our warehouse either back to his location or back to the supplier’s location
   1. **Batch Orders:** Pick items from specific batch specifying the batch number
   1. **Expiring Orders: Pick** items that are between specific expiry dates

In orders, there are two possible shipment types that can be used:

1. **DPW Shipping –** Order is shipped to the customer
1. **Warehouse Pickup –** Seller provides a pickup date and picks it up from the warehouse himself. In the case of warehouse pickup, the seller should able select the exact pickup date by when the items should be ready.

## Order Statuses
| Status | Description                                                                               |
|------------|-------------------------------------------------------------------------------------------|
| COMPLETED  | The order is completed.                                                  |
| CREATED    | The order was placed or created.                                                          |
| CANCELLED  | The order was canceled|
| PROCESSING | The order fulfillment is in progress.                                                      |

## Fulfilment Statuses
| Status             | Description                                                                                                      |
|------------------------|------------------------------------------------------------------------------------------------------------------|
| CREATED                | Order has been created.                                                                                          |
| AWAITING_STOCK         | Order is in awaiting stock and will be processed once the item is available.                                       |
| IN_VALIDATION          | The order is in validation process.                                                                             |
| READY_FOR_PICKING      | Order is ready for picking.|
| IN_PICKING_QUEUE       | Order is in the picking queue.                                                                                   |
| PICKED                 | Order items have been picked|
| PACKED                 | Order items have been packed|
| SHIPPED                | Order has been shipped|
| OUT_FOR_DELIVERY       | Order is out for delivery|
| DELIVERED              | Order has been delivered                                                 |
| COLLECTED              | Order has been collected            |
| ON_HOLD                | Order is on hold, Internal Validations failed / Manual movement to On Hold.                                       |
| EXCEPTION              | Order is in an exception state, Internal Validations failed / Shipment moved to On Hold.                       |
| FAILED_DELIVERY_ATTEMPT | Failed attempt to deliver order                                            |
| RETURN_TO_ORIGIN       | Order is being returned to origin, RTO/Return is sutomatically created for the same |
| UNRECOVERABLE          | Order is in an unrecoverable state                                          |
| COURIER_CANCELLED      | Order was cancelled by the courier                                  |
| CANCELLED              | Order has been cancelled                                              |
| COURIER_PICKUP_UNSUCCESSFUL | Courier pickup attempt was unsuccessful.                                                                     |
| COURIER_DELIVERY_UNSUCCESSFUL | Courier delivery attempt was unsuccessful.                                                                 |
| COURIER_COLLECTION_UNSUCCESSFUL | Courier collection attempt was unsuccessful.                                                             |

### Create Order
- **Description**: This api is used to create a filfilment order
- **Path**: /v1/order/place-order
- **Verb**: POST

#### Request
```json
{
  "orderType": "NEW",
  "orderChannelId": "CL",
  "orderSourceId": "SFS",
  "orderCreationType": "API",
  "buId": "2f6823d4-8dfb-5",
  "customerType": "CONSUMER",
  "fulfillmentType": "DPW_FULFILLMENT",
  "orderPlacedAt": "2024-03-01T06:11:59.865Z",
  "currency": "EUR",
  "orderStatus": "CREATED",
  "consigneeOrderId": "C-01",
  "marketplaceFlag": 1,
  "marketplaceDesc": "Amazon",
  "consignee": {
    "contact": {
      "name": {
        "firstName": "David",
        "lastName": "Warner",
        "middleName": "Andrew",
        "nickName": "Bull"
      },
      "phone": "0726014424",
      "email": "test@test.com",
      "countryCode": "+27"
    }
  },
  "customerInfo": {
    "customerReference": "",
    "customerAccountId": "2f6823d4-8dfb-5",
    "customerFullName": "AmitS2Smigration"
  },
  "shippingTo": {
    "contact": {
      "name": {
        "firstName": "David",
        "lastName": "Warner",
        "middleName": "Andrew",
        "nickName": "Bull"
      },
      "phone": "0726014424",
      "email": "test@test.com",
      "countryCode": "+27"
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
      "region": "string",
      "companyId": "12345",
      "locationId": "1234"
    }
  },
  "shippingDetails": {
    "shippingType": "DPW_SHIPPING",
    "shippingOption": "CHEAPEST",
    "fulfillmentCenter": "WAREHOUSE_UK",
    "quoteId": null,
    "shippingMethod": [
      "Evri Standard Delivery (2–3 working days)"
    ]
  },
  "fulfillmentLines": {
    "totalLineQty": 1,
    "currencyUnit": "EUR",
    "lineTotal": {
      "currencyAmount": 0
    },
    "orderLineDetails": [
      {
        "fulfillmentLineId": "1",
        "lineOrderPlacedAt": "2024-03-01",
        "quantity": {
          "measurementValue": 1,
          "unitOfMeasure": "EA"
        },
        "itemDetails": {
          "inventoryId": "SCOTT",
          "itemDesc": "",
          "sellerId": "2f6823d4-8dfb-5",
          "itemUrl": ""
        },
        "chargeDetails": [
          {
            "chargeCategory": "PRODUCT",
            "chargeName": "ITEM_PRICE",
            "currencyAmount": 0
          }
        ]
      }
    ],
    "additionalAttributes": [
      {
        "attributeData": [
          {
            "attributeName": "PACKLIST",
            "attributeValue": "YES"
          }
        ],
        "attributeType": "ADDITIONAL_ATTRIBUTES"
      }
    ]
  },
  "totalChargeDetails": [
    {
      "chargeCategory": "PRODUCT",
      "chargeName": "ITEM_PRICE",
      "currencyAmount": "0"
    },
    {
      "chargeCategory": "ORDER_TOTAL",
      "chargeName": "TOTAL",
      "currencyAmount": "0"
    }
  ],
  "paymentDetails": {
    "paymentType": "PRE_PAID",
    "status": "UNSPECIFIED_PAYMENT_STATUS",
    "amountPaid": 100,
    "payments": [
      {
        "paymentReferenceId": "PAY12345",
        "pg": "PayPal",
        "paymentMethod": "Credit Card",
        "transactionDate": "2023-08-09T12:34:56Z",
        "amount": 100,
        "status": "UNSPECIFIED_PAYMENT_STATUS"
      }
    ],
    "billTo": {
      "contact": {
        "name": {
          "firstName": "David",
          "lastName": "Warner",
          "middleName": "Andrew",
          "nickName": "Bull"
        },
        "phone": "0726014424",
        "email": "test@test.com",
        "countryCode": "+27"
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
        "region": "string",
        "companyId": "12345",
        "locationId": "1234"
      }
    }
  },
  "notes": [
    {
      "commentType": "SellerNote",
      "comment": "Please pack items securely."
    }
  ],
  "platformAttributes": {
    "brandCode": "20959"
  },
  "attachments": [
    {
      "documentName": "Not Available.pdf",
      "documentCategory": "SHIPPING_LABEL",
      "documentLink": "https://newOmsFolder%2Fe94b0d7a-ca66-4039-987c-9b23876da1e1-Not%20Available.pdf",
      "createdBy": "amit.test",
      "documentAttributes": [
        {
          "attributeName": "QUANTITY",
          "attributeValue": "1"
        },
        {
          "attributeValue": "PLACE_INSIDE",
          "attributeName": "DOCUMENT_PLACE_ATTRIBUTE"
        }
      ]
    }
  ]
}
```

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :- | :- | :- | :- | :- |
|orderType|<p>Type of order:<br>1\. NEW – new orders</p><p>2\. RETURN – return orders</p>|String|Yes|"NEW"|
|orderChannelId|Identifier for the order channel.<br>Default value is CL|String|Yes|"CL"|
|orderSourceId|Identifier for the order source|String|Yes|"DPWorld"|
|orderCreationType|Medium of creation for the order|String|No|"AssistedChannel"|
|buId|Business unit ID: Unique for each seller to be provided at the time of onboarding|String|Yes|"2f6823d4-8dfb-5": |
|customerType|<p>Type of order:<br>1\. CONSUMER: consumer order</p><p>2\. SUPPLIER: supplier order</p>|String|Yes|"CONSUMER"|
|fulfillmentType|Type of fulfilment:<br>1\. DPW\_FULFILLMENT: DPW Warehouse - Yes, DPW Shipping - Yes<br>2\. SELLER\_FULFILLMENT: DPW Warehouse - No, DPW Shipping - No<br>3\. PICKUP\_AT\_WH: DPW Warehouse - Yes, DPW Shipping - No<br>4\. DROP\_AT\_WH DPW Warehouse - No, DPW Shipping - Yes|String|Yes|"DPW\_FULFILLMENT"|
|orderPlacedAt|Timestamp indicating when the order was placed (UTC)|String (ISO 8601)|Yes|"2024-03-01T06:11:59.865Z"|
|currency|Currency code|String|Yes|"EUR"|
|consigneeOrderId|Consignee order ID|String|No|"C-01"|
|marketplaceFlag|market place flag|int|No|default - 0<br> Amazon - 1<br>Otto - 2<br>John Lewis - 3|
|marketplaceDesc|market place description|String|No|"Amazon"|
#### Consignee Details

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|contact|Contact information of the consignee|Object|Yes|See nested fields: **contact**|
##### **Nested Fields: contact**

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|name|Name|Object|Yes|See nested fields|
|phone|Phone number|String|Yes|"0726014424"|
|email|Email address|String|Yes|"<test@test.com>"|
|countryCode|Country code|String|Yes|"+27"|
#### Customer Information

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|customerReference|Reference Id/tag for the order|String|No|""|
|customerAccountId|Account ID of the seller, same as buid|String|Yes|"2f6823d4-8dfb-5"|
|customerFullName|Seller Name|String|No|"AmitS2Smigration"|
#### Shipping Details

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|contact|Contact information of the shipping destination|Object|Yes|See nested fields: **contact**|
|address|Address information of the shipping destination|Object|Yes|See nested fields: **address**|
##### **Nested Fields: address**

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|unitNumber|Unit number of the address|String|No|Apt 4B|
|lineOne|First line of the address|String|Yes|123 Main St|
|lineTwo|Second line of the address|String|No|Apt 4B|
|city|City of the address|String|No|Mumbai|
|state|State of the address|String|Yes|Maharastra|
|country|Country of the address|String|Yes|India|
|zip|The postal code (zip, postcode, or Eircode)|String|Yes|721304|
|suburb|Suburb|String|No||
|companyId|Locker Company Name/ID|String|No|Pargo|
|locationId|Locker Id|String|No|1234|

#### Shipping Details
| Field            | Description                          | Data Type | Mandatory | Example                     |
|------------------|--------------------------------------|-----------|-----------|-----------------------------|
| shippingType     | Type of shipping                     | String    | Yes       | "DPW_SHIPPING"             |
|                  | **Options:**                        |           |           |                             |
|                  | DPW_SHIPPING: warehouseApplicable = Yes, shippingApplicable = Yes |           |           |                             |
|                  | SELLER_SHIPPING: warehouseApplicable = No, shippingApplicable = No |           |           |                             |
|                  | WAREHOUSE_PICKUP: warehouseApplicable = Yes, shippingApplicable = No |           |           |                             |
|                  | DROP_AT_WAREHOUSE: warehouseApplicable = No, shippingApplicable = Yes |           |           |                             |
| shippingOption   | Shipping option                      | String    | Yes       | "CHEAPEST"                  |
|                  | **Options:**                        |           |           |                             |
|                  | CHEAPEST                           |           |           |                             |
|                  | FASTEST                            |           |           |                             |
|                  | RESPECTIVE_COURIERS                |           |           |                             |
| fulfillmentCenter| Fulfillment center                   | String    | Yes       | "WAREHOUSE_UK" |


#### Fulfillment Lines

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|totalLineQty|Total quantity of fulfillment lines|Integer|Yes|1|
|currencyUnit|Currency unit for fulfillment lines|String|Yes|"EUR"|
|lineTotal|Total amount for fulfillment lines|Object|Yes|See nested fields|
|orderLineDetails|Details of individual order lines|Array|Yes|See nested fields|
|additionalAttributes|Additional attributes for fulfillment lines|Array|No|Empty array|
##### **Nested Fields: lineTotal**

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|currencyAmount|Total amount|Integer|Yes|0|
##### **Nested Fields: orderLineDetails**

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|fulfillmentLineId|Identifier for the fulfillment line|String|Yes|"1"|
|lineOrderPlacedAt|Timestamp when the order line was placed (UTC)|String (ISO 8601)|Yes|"2024-03-01T00:00:00.000Z"|
|quantity|Quantity of items|Object|Yes|See nested fields|
|itemDetails|Details of the item|Object|Yes|See nested fields|
|chargeDetails|Details of charges for the order line|Array|No|See nested fields|
##### **Nested Fields: quantity**

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|measurementValueInDouble|Quantity value|Double|Yes|1.0|
|unitOfMeasure|Unit of measurement|String|Yes|"EA"|
##### **Nested Fields: itemDetails**

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|inventoryId|Inventory ID|String|Yes|"SCOTT"|
|itemDesc|Description of the item|String|No|""|
|sellerId|ID of the seller|String|Yes|"2f6823d4-8dfb-5"|
|itemUrl|URL of the item|String|No|""|
##### **Nested Fields: chargeDetails**

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|chargeCategory|Category of the charge|String|Yes|"PRODUCT"|
|chargeName|Name of the charge|String|Yes|"ITEM_PRICE"|
|currencyAmount|Amount of the charge|Double|Yes|1.0|
#### Payment Details

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|paymentType|Type of payment|String|Yes|"PRE_PAID"|
|status|Status of the payment|String|Yes|"UNSPECIFIED\_PAYMENT\_STATUS"|
|amountPaid|Amount paid for the order|Integer|Yes|100|
|payments|Details of individual payments|Array|Yes|See nested fields|
|billTo|Billing details|Object|Yes|See nested fields|
##### **Nested Fields: payments**

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|paymentReferenceId|Reference ID for the payment|String|Yes|"PAY12345"|
|pg|Payment gateway used|String|Yes|"PayPal"|
|paymentMethod|Payment method|String|Yes|"Credit Card"|
|transactionDate|Timestamp of the transaction (UTC)|String (ISO 8601)|Yes|"2023-08-09T12:34:56.000Z"|
|amount|Amount of the payment|Integer|Yes|100|
|status|Status of the payment|String|Yes|"UNSPECIFIED\_PAYMENT\_STATUS"|
##### **Nested Fields: billTo**

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|contact|Contact information of the bill recipient|Object|Yes|See nested fields|
|address|Address information of the bill recipient|Object|Yes|See nested fields|
#### Notes

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|commentType|Type of comment|String|Yes|"SellerNote"|
|comment|Comment text|String|Yes|"Please pack items securely."|
#### Attachments

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|documentName|Name of the document|String|Yes|"Not Available.pdf"|
|documentCategory|Category of the document|String|Yes|"SHIPPING\_LABEL"|
|documentLink|URL link to the document|String|Yes|"<https://example.com/document.pdf>"|
|createdBy|Creator of the document|String|Yes|"amit.test"|
|documentAttributes|Additional attributes of the document|Array|No|See nested fields|
##### **Nested Fields: documentAttributes**

|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|attributeName|Attribute name|String|Yes|"QUANTITY"|
|attributeValue|Attribute value|String|Yes|"1"|
|attributeName|Attribute name|String|Yes|"DOCUMENT\_PLACE\_ATTRIBUTE"|
|attributeValue|Attribute value|String|Yes|"PLACE\_INSIDE"|

##### **Nested Fields: AdditionalAttribute

| Field | Type | Required | Description | Example |
|-------|------|----------|-------------|---------|
| `attributeType` | String | Yes | Type/category of additional attributes | `LINE_ATTRIBUTES` |
| `attributeData` | Array | Yes | List of attribute name-value pairs | See AttributeData below |

##### ** AttributeData

| Field | Type | Required | Description | Example |
|-------|------|----------|-------------|---------|
| `attributeName` | String | Yes | Name of the attribute | `PACKLIST` |
| `attributeValue` | String | Yes | Value of the attribute | `YES` |

##### Allowed Attribute Names

The following attribute names are supported:

- `PACKLIST` - Packing list information
- `BACK_DOOR_DELIVERY` - Back door delivery requirement
- `INSURANCE` - Insurance coverage flag
- `PRIORITY_DELIVERY` - Priority/expedited delivery flag
- `AGE_VERIFICATION` - Age verification requirement

##### ** PlatformAttributes (Optional)

| Field | Type | Required | Description | Example |
|-------|------|----------|-------------|---------|
| `isBrand` | Boolean | No | Whether the product is branded | `true` |
| `brandCode` | String | No | The code of the brand | `NIKE` |


#### Response
```json
{
  "data": {
    "orderId": "OMS-10000080964"
  },
  "message": "Success! Your order with ID OMS-10000080964 has been created.",
  "httpStatus": "OK"
}
```

### Orders List
Gives list of orders based on the requested filters. Filtering is based on the fields provided in the request body. If a field is empty or null, no filtering is applied to the data.
- **Verb**: POST
- **Path**: /v2/order/orders?limit=20&page=0&sortOn=orderDate&direction=DESC

#### QueryParams
|**Field**|**Type**|**Default Value**|**Comments**|
| :- | :- | :- | :-: |
|limit|Integer|20| |
|<p>page</p><p> </p>|Integer|0|Starts with 0|
|<p>sortOn</p><p> </p>|String |orderDate|Accepted values: [orderId, shipmentId, sourceStore, orderDate, fulfillmentCentre, shipmentStatus, shipmentSubStatus, status, returnStatus, returnSubStatus, returnId]|
|<p>direction</p><p> </p>|String|DESC|Case ignored; order will be “desc” if input is “desc” otherwise “asc”|

#### Request
```json
{
  "searchValue": "",
  "startDate": "2024-01-01T00:00:00.000Z",
  "endDate": "2024-03-05T23:59:59.000Z",
  "sourceStore": [],
  "paymentOptions": [
    "CASH_ON_DELIVERY"
  ],
  "fulfilmentCenter": [],
  "consumerType": [],
  "orderStatuses": [],
  "accounts": [
    "4cf19e27-3fe0-5"
  ]
}
```
|**Field**|**Type**|**Description**|**Comments**|**Example**|
| :- | :- | :- | :- | :- |
|searchValue|String|Pattern matching order\_id and consignee\_order\_id| |“OMS-100000022”|
|startDate|LocalDateTime|Filter on ordered\_at including startDate|If startDate not specified, filter will default to lowest date.|"2024-03-06T08:48:36.643Z"|
|endDate|LocalDateTime|Filter on ordered\_at including endDate|If endDate not specified, filter will default to highest date.|"2024-03-06T08:48:36.643Z"|
|orderStatuses|Array|List of order statuses|Null values included in response|[“COMPLETED”,” CREATED”]|
|accounts|Array|List of customer\_accound\_id|Null values not included in response|[“41a1c66d-f989-5”]|
|sourceStore|Array|<p>List of order\_creation\_type,</p><p>SFS or 3PE</p>|Null values included in response|["SFS\_PORTAL"]|
|paymentOptions|Array|<p>List of payment\_type</p><p>Prepaid or cashOnDelivery</p>|Null values included in response|[“PRE\_PAID”]|
|fulfillmentCenter|Array|List of warehouses (fulfillment\_center)|Null values included in response|["WAREHOUSE\_UK"]|
|consumerType|Array|List of consumer\_type|Null values included in response|["CONSUMER"]|

#### Sample Query Parameters
limit=15&page=0&direction=DESC&sortOn=orderDate

#### Response 
|**Field**|**Type**|**Description**|
| :- | :- | :- |
|orders|Array|List of filtered Orders objects |
|pageDetails|Object|PageDetails Object|

**Orders**
|**Field**|**Type**|**Columns Mapped in Solr**|**Example**|
| :- | :- | :- | :- |
|orderId|String|order\_id|“OMS-10000000027”|
|sourceStore|String|order\_creaton\_type|“WWHCNIGERIA”|
|orderDate|Date|ordered\_at|"2023-10-26T13:42:56Z”|
|customerFullName|String|customer\_account\_name|"La Med Pharmacy-SDZ"|
|status|String|order\_status|“CREATED”|
|adjustments|Boolean|Is\_adjusted|True|
|orderTotal|Double|currency\_amount|106\.0|
|currency|String|currency\_unit|“USD”|
|customerReference|String|customer\_reference|“4765936517272”|
|customerAccountUserId|String|customer\_account\_id|"41a1c66d-f989-5”|
|consigneeOrderId|String|consignee\_order\_id|“5803194155160”|
|orderType|String|order\_type|“NEW”|
|outboundId|String|outbound\_id|“62395842”|

**PageDetails**
|**Field**|**Type**|**Description**|
| :- | :- | :- |
|totalCount|Long|Total count of filtered data|

#### Response
```json
{
  "data": {
    "orders": [
      {
        "orderId": "OMS-10000003111",
        "sourceStore": "SFS_PORTAL",
        "orderDate": "2024-01-12T00:00:00.000+00:00",
        "customerFullName": null,
        "status": "CREATED",
        "adjustments": null,
        "orderTotal": null,
        "currency": null,
        "shippingStatus": null,
        "trackingId": null,
        "shipmentId": null,
        "orderType": "RETURN",
        "fulfillmentCentre": null,
        "outboundId": null,
        "customerReference": null,
        "consigneeOrderId": null,
        "customerAccountUserId": "4cf19e27-3fe0-5",
        "approvalStatus": null
      },
      {
        "orderId": "OMS-10000003112",
        "sourceStore": "SFS_PORTAL",
        "orderDate": "2024-01-12T00:00:00.000+00:00",
        "customerFullName": null,
        "status": "PROCESSING",
        "adjustments": null,
        "orderTotal": null,
        "currency": null,
        "shippingStatus": null,
        "trackingId": null,
        "shipmentId": null,
        "orderType": "RETURN",
        "fulfillmentCentre": null,
        "outboundId": null,
        "customerReference": null,
        "consigneeOrderId": null,
        "customerAccountUserId": "4cf19e27-3fe0-5",
        "approvalStatus": null
      }
    ],
    "pageDetails": {
      "totalCount": 2
    }
  },
  "message": "Success",
  "httpStatus": "OK"
}
```

### Shipments List API
- **Verb**: POST
- **Path**: /v2/shipment/shipments?limit=20&page=0&sortOn=shipmentId&direction=DESC

#### QueryParams
|**Field**|**Type**|**Default Value**|**Comments**|
| :- | :- | :- | :-: |
|limit|Integer|20| |
|<p>page</p><p> </p>|Integer|0|Starts with 0|
|<p>sortOn</p><p> </p>|String |shipmentId|<p>Accepted values: [orderId, shipmentId, sourceStore, orderDate, fulfillmentCentre, shipmentStatus, shipmentSubStatus]</p>|
|<p>direction</p><p> </p>|String|DESC|Case ignored; order will be “desc” if input is “desc” otherwise “asc”|

#### Request
```json
{
  "shipmentStatuses": [],
  "sourceStore": [],
  "paymentOption": [
    "PRE_PAID"
  ],
  "customerType": [
    "CONSUMER",
    "SUPPLIER"
  ],
  "startDate": "2024-01-24T00:00:00.000Z",
  "endDate": "2024-03-06T23:59:59.000Z",
  "shipmentType": [
    "DPW_SHIPPING",
    "WAREHOUSE_PICKUP"
  ],
  "shipmentOption": [
    "CHEAPEST",
    "FASTEST"
  ],
  "carrierService": [],
  "fulfillmentCentre": [
    "148796_ORACLE"
  ],
  "tabSelected": "All",
  "search": ""
}
```

|**Fields**|**Type**|**Description**|**Example**|
| :- | :- | :- | :- |
|search|String|Pattern matching  order\_id, shipping\_tag\_id, consignee\_order\_id| |
|startDate|LocalDateTime|Filter on ordered\_at including startDate|"2024-03-06T08:48:36.643Z"|
|endDate|LocalDateTime|Filter on ordered\_at including endDate|"2024-03-06T08:48:36.643Z"|
|shipmentStatuses|Array|List of shipment statuses|[“COMPLETED”, “PICKED”]|
|accounts|Array|List of  customer\_accound\_id|[“41a1c66d-f989-5”]|
|sourceStore|Array|List of order\_creation\_type|["SFS\_PORTAL"]|
|shipmentOption|Array|List of shipment\_option|[“CHEAPEST”]|
|fulfillmentCentre|Array|List of warehouses (fulfillment\_center)|["WAREHOUSE\_1"]|
|consumerType|Array|List of consumer\_type|["CONSUMER"]|
|shipmentType|Array|List of shipment\_type|["DPW\_SHIPPING”, “WAREHOUSE\_PICKUP”]|

#### Response
```json
{
  "data": {
    "shipments": [
      {
        "shipmentId": "SHP-10000002297",
        "orderId": "OMS-10000003157",
        "sourceStore": "DPWFulfillment",
        "orderDate": "2024-02-12T06:59:18.000+00:00",
        "fulfillmentCentre": "WAREHOUSE_UK",
        "shipmentStatus": "AWAITING_STOCK",
        "shipmentSubStatus": "Stock unavailable",
        "outboundId": null,
        "consigneeOrderId": null
      },
      {
        "shipmentId": "SHP-10000002284",
        "orderId": "OMS-10000003144",
        "sourceStore": "DPWFulfillment",
        "orderDate": "2024-02-05T10:50:32.000+00:00",
        "fulfillmentCentre": "WAREHOUSE_UK",
        "shipmentStatus": "AWAITING_STOCK",
        "shipmentSubStatus": "Stock unavailable",
        "outboundId": null,
        "consigneeOrderId": null
      },
      {
        "shipmentId": "SHP-10000002283",
        "orderId": "OMS-10000003143",
        "sourceStore": "DPWFulfillment",
        "orderDate": "2024-02-05T10:30:04.000+00:00",
        "fulfillmentCentre": "WAREHOUSE_UK",
        "shipmentStatus": "IN_VALIDATION",
        "shipmentSubStatus": null,
        "outboundId": "62534169",
        "consigneeOrderId": null
      },
      {
        "shipmentId": "SHP-10000002272",
        "orderId": "OMS-10000003135",
        "sourceStore": "DPWFulfillment",
        "orderDate": "2024-02-01T13:25:02.000+00:00",
        "fulfillmentCentre": "WAREHOUSE_UK",
        "shipmentStatus": "CANCELLED",
        "shipmentSubStatus": null,
        "outboundId": null,
        "consigneeOrderId": null
      }
    ],
    "pageDetails": {
      "totalCount": 4
    }
  },
  "message": "Success",
  "httpStatus": "OK"
}
```
|**Field**|**Type**|**Description**|
| :- | :- | :- |
|shipments|Array|List of filtered Shipments objects |
|pageDetails|Object|PageDetails Object|

**Shipments**
|**Field**|**Type**|**Columns Mapped in Solr**|**Example**|
| :- | :- | :- | :- |
|shipmentId|String|shipping\_tag\_id|“SHP-10000000015"|
|sourceStore|String|order\_creaton\_type|“WWHCNIGERIA”|
|orderDate|Date|ordered\_at|"2023-10-26T13:42:56Z”|
|shipmentStatus|String|shipment\_status|"ON\_HOLD"|
|shipmentSubStatus|String|shipment\_sub\_status|"Address validation for failed"|
|fulfillmentCentre|Boolean|fulfillment\_center|"WAREHOUSE\_UK"|
|consigneeOrderId|String|consignee\_order\_id|"5803194155160"|
|orderId|String|order\_id|"OMS-10000000019"|
|outboundId|String|outbound\_id|“62395838”|

**PageDetails**
|**Field**|**Type**|**Description**|
| :- | :- | :- |
|totalCount|Long|Total count of filtered data|

### Get Order
Get a specific order using the orderId
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
          "shippingDetail": {
            "shippingType": "DPW_SHIPPING",
            "shippingOption": "CHEAPEST",
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
            "status": "SHIPPED",
            "lineId": "1665263",
            "promotionOnly": null,
            "erpTrackingId": null,
            "specializedItemBarcode": null,
            "serialNumbers": [
              "WP5000000002579",
              "WP5000000002542",
              "WP5000000003407",
              "WP5000000003198",
              "WP5000000003258",
              "WP5000000004372",
              "WP5000000003064",
              "WP5000000003032",
              "WP5000000001368",
              "WP5000000001211",
              "WP5000000001369",
              "WP5000000003096",
              "WP5000000001336",
              "WP5000000001314",
              "WP5000000003013"
            ],
            "imeiNumbers": [
              "353111150048575",
              "353111150047841",
              "353111150065132",
              "353111150060950",
              "353111150062154",
              "353111150084430",
              "353111150058277",
              "353111150057634",
              "353111150024352",
              "353111150021218",
              "353111150024378",
              "353111150058913",
              "353111150023719",
              "353111150023271",
              "353111150057253"
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
### Get Shipment
Get a specific shipment using the shipmentId of order
- **Method**: GET
- **Path**: - /v1/shipment/{shippingId}
  
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
### Cancel Order
- **Method**: PUT
- **Path**: - v1/order/{orderId}/cancel

#### Response
```json
{
  "data": {
    "shipmentIds": [
      "shipmentId1"
    ],
    "result": " Success/Failure "
  },
  "message": " Success! Your order has been canceled. ",
  "httpStatus": "200 OK"
}
```

### Shipment update
Allows shipment to be either cancelled or put the shipment on –hold .

1. Cancelling the shipment will cancel the shipment and no further action will be taken
1. Putting a shipment on hold mean the shipment will not be further processed and will be halt at current status . Later on the shipment can be released for further processing or even cancelled.
- **Method**: PATCH
- **Path**: v1/shipment/{shipmentTagId}/status-update

##### Request
```json
{
  "status": "CREATED",
  "reserveInventory": true,
  "userId": "string",
  "sellerId": "string"
}
```
|**Field**|**Description**|**Data Type**|**Mandatory**|**Example**|
| :-: | :-: | :-: | :-: | :-: |
|status|New updated status for the shipment|Enum|Yes|CANCELLED, ON_HOLD|
|reserveInventory|Reserve inventory in warehouse when putting shipment on hold|Boolean|No|true/false|
|userId|User id of user performing action|<p>String</p><p></p>|No|“acef-id1”|
|sellerId|Id of seller of order|<p>String</p><p></p>|No|<p>“acef-id1”</p><p></p>|

#### Response
```json
{
  "data": true,
  "message": "string",
  "httpStatus": "100 CONTINUE"
}
```

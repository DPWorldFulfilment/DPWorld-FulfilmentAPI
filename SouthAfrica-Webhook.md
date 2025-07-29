# 📦 South Africa / Parcel Ninja Webhook Documentation

This document provides the format and explanation of different webhook payloads received from Parcel Ninja for **Inventory Adjustments**, **Orders**, and **Inbounds**.

---

## 📘 1. Adjustment Webhook Payload (Sample)

Webhook payloads for stock adjustments look like this:

```json
{"sku":"A042-5401132325316","timestamp":"20250417010824","stockType":"InStock","oldQuantity":13,"newQuantity":12,"change":-1,"reason":"Outbound Created","quantity":0}
{"sku":"YOU3010","timestamp":"20250204142443","stockType":"InStock","oldQuantity":82,"newQuantity":83,"change":1,"reason":"Stock Put Away","expiryDate":"2026-04-30 00:00:00.000","batchNumber":"22042024"}
{"sku":"GD3","timestamp":"20250417055000","stockType":"InStock","oldQuantity":12,"newQuantity":13,"change":1,"reason":"Stock Put Away","expiryDate":"0001-01-01 00:00:00.000","inboundReference":"RO-10000009473","storeName":"HPH Publishing cc","quantity":1}
{"sku":"A135-010-02906-12","timestamp":"20250417065724","stockType":"InStock","oldQuantity":0,"newQuantity":1,"change":1,"reason":"Unreserve Stock","quantity":0}
{"sku":"A135-010-02906-12","timestamp":"20250417065724","stockType":"Reserved","oldQuantity":1,"newQuantity":0,"change":-1,"reason":"Unreserve Stock","quantity":0}
{"sku":"A272-OUKITEL RT9 BLACK","timestamp":"20250417075655","stockType":"Reserved","oldQuantity":3,"newQuantity":0,"change":-3,"reason":"Unreserve Stock","quantity":0}
{"sku":"A272-OUKITEL RT9 BLACK","timestamp":"20250417075851","stockType":"InStock","oldQuantity":18,"newQuantity":21,"change":3,"reason":"Unreserve Stock","quantity":0}
```

### Fields:

* `sku`: Item identifier
* `timestamp`: Event time (format: `yyyyMMddHHmmss`)
* `stockType`: `"InStock"` or `"Reserved"`
* `oldQuantity`, `newQuantity`: Quantity before and after the adjustment
* `change`: Difference between new and old quantity
* `reason`: Why the stock was changed
* Optional: `expiryDate`, `batchNumber`, `inboundReference`, `storeName`, `quantity`

---

## 🔄 2. Adjustment Reasons

| Reason Type                       |
| --------------------------------- |
| Transition Stock                  |
| Reserve Stock                     |
| Unreserve Stock                   |
| Outbound Deleted                  |
| Allocate Broken or Missing Stock  |
| Resolve Stock as Missing or Found |
| Stock Put Away                    |
| Decrease Stock at Location        |
| Increase Stock at Location        |
| CYCLE\_COUNT                      |
| ECOM\_S2NS                        |

---

## 📦 3. Orders Webhook (Sample)

```json
{
  "id": 12154235,
  "clientId": "GHJLAOK987",
  "type": {
    "id": 2,
    "description": "Order"
  },
  "timeStamp": "20210719062140",
  "events": [
    {"code": 245, "timeStamp": "20220225114251", "description": "Delivered"},
    {"code": 244, "timeStamp": "20220224123933", "description": "Dispatched with courier"},
    ...
  ],
  "deliveryInfo": {
    "trackingURL": "https://store.parcelninja.com/tracking.aspx?WaybillNo=PNJ12154235",
    "waybillNumber": "PNJ12154235"
  }
}
```

---

## 🚚 4. Order Event Status Codes

| Code | Rank | Description                                                |
| ---- | ---- | ---------------------------------------------------------- |
| 240  | 1    | Awaiting Stock                                             |
| 290  | 2    | In Picking Queue                                           |
| 241  | 3    | Ready to be Picked                                         |
| 282  | 4    | On Hold                                                    |
| 291  | 5    | In Packing Queue                                           |
| 242  | 6    | Ready to be Packed                                         |
| 246  | 7    | Awaiting Collection *(Collect from warehouse)*             |
| 391  | 8    | Courier Collection Unsuccessful *(Collect from warehouse)* |
| 247  | 9    | Collected *(Collect from warehouse)*                       |
| 243  | 10   | Awaiting Courier Pickup *(Courier Shipping)*               |
| 244  | 11   | Dispatched with Courier *(Courier Shipping)*               |
| 390  | 12   | Courier Pickup Unsuccessful *(Courier Shipping)*           |
| 300  | 13   | Scheduled for Delivery with Courier *(Courier Shipping)*   |
| 392  | 14   | Courier Delivery Unsuccessful *(Courier Shipping)*         |
| 280  | 15   | Unable to Deliver *(Courier Shipping)*                     |
| 245  | 16   | Delivered *(Courier Shipping)*                             |

---

## 📥 5. Inbound Webhook (Sample)

```json
{
  "id": 10601048,
  "clientId": "RO-10000009473",
  "warehouseId": null,
  "type": {
    "id": 1,
    "description": "Stock"
  },
  "timeStamp": "20240905071151",
  "events": [
    {"code": 203, "timeStamp": "20250416141448", "description": "Processing complete"},
    {"code": 202, "timeStamp": "20250416131304", "description": "Being Processed"},
    {"code": 201, "timeStamp": "20250416083930", "description": "Arrived at warehouse"},
    {"code": 200, "timeStamp": "20250331045500", "description": "Awaiting arrival"}
  ]
}
```

---

## 🧾 6. Inbound Status Codes

| Code | Rank | Description                       |
| ---- | ---- | --------------------------------- |
| 200  | 1    | Awaiting Arrival                  |
| 201  | 2    | Arrived at warehouse              |
| 202  | 3    | Being Processed                   |
| 203  | 4    | Processing complete               |
| 204  | 5    | Processing complete with variance |

---

## 🏷️ 7. Inbound Types

| Type ID | Description   |
| ------- | ------------- |
| 1       | Stock Inbound |
| 3       | RMA           |

---

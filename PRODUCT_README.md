### Create Bundled Product
- **Description**: Converts a product into bundled product.
- **URL**: /api/ims/v1/bundle
- **Verb**: POST

#### RequestHeaders 
|Key|Value|
| :- | :- |
|languageCode|en/fr|

#### Request
```json
{
  "merchantId": "2f6823d4-8dfb-5",
  "mergeOrigin": "B291-E8A4E4F8C7D0E283",
  "channelId": "PARCEL_NINJA",
  "inventoryInfoList": [
    {
      "inventoryId": "B291-F55D039CE4EF4EEE",
      "quantity": 5
    },
    {
      "inventoryId": "B291-G85D039CE4EF4ADF",
      "quantity": 2
    }
  ]
}
```

#### Request Params
|Field|Description|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|merchantId|sellerId|String|Y|2f6823d4-8dfb-5|
|mergeOrigin|Parent inventory to be made into bundle product|String|Y|B291-E8A4E4F8C7D0E283|
|channelId|channel|String|Y|PARCEL\_NINJA|
|inventoryInfoList|List of child inventory id configs per bundle|List|Y|-|
|InventoryInfoList[\*].inventoryId|Child inventory Id|String|Y|B291-F55D039CE4EF4EEE|
|<p>InventoryInfoList[\*].quantity</p><p></p>|Inventory of child InventoryId per bundle|Integer|Y|5|

#### Response
```json
{
  "groupId": "a8740efa-fa7a-4768-af0d-aeade5451804",
  "status": true
}
```

### Response
|Field|Description|Datatype|Example|
| :- | :- | :- | :- |
|groupId|Unique groupId for the created bundle|String|a8740efa-fa7a-4768-af0d-aeade5451804|
|status|Success status|boolean|true/false|

Curl
```bash
curl --location --request POST ‘{{HOST}}api/ims/v1/bundle' \ 
--header 'Content-Type: application/json' \ 
--header 'languageCode: en' \ 
--data-raw '{ 
    "merchantId" : "2f6823d4-8dfb-5", 
    "mergeOrigin" : "B291-E8A4E4F8C7D0E283", 
    "channelId": "PARCEL_NINJA", 
    "inventoryInfoList" : [ 
        { 
            "inventoryId" : "B291-F55D039CE4EF4EEE", 
            "quantity" : 5 
        } 
    ] 
}'
```

### Update Bundle
- **Description**: Updates the child configuration of a bundled product
- **URL**: /api/ims/v1/bundle
- **Verb**: PUT

#### RequestHeaders:
|Key|Value|
| :- | :- |
|languageCode|en/fr|


#### Request
```json{
  "merchantId": "2f6823d4-8dfb-5",
  "mergeOrigin": "B291-E8A4E4F8C7D0E283",
  "channelId": "PARCEL_NINJA",
  "groupId": "a8740efa-fa7a-4768-af0d-aeade5451804",
  "inventoryInfoList": [
    {
      "inventoryId": "B291-F55D039CE4EF4EEE",
      "quantity": 10
    }
  ]
}
```

#### Request Params:
|Field|Description|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|merchantId|sellerId|String|Y|2f6823d4-8dfb-5|
|mergeOrigin|Bundled inventory Id to be updated|String|Y|B291-E8A4E4F8C7D0E283|
|channelId|channel|String|Y|PARCEL\_NINJA|
|groupId|Unique groupId of bundled product|String|Y|a8740efa-fa7a-4768-af0d-aeade5451804|
|inventoryInfoList|List of updated child inventory id configs per bundle|List|Y|-|
|InventoryInfoList[\*].inventoryId|Child inventory Id|String|Y|B291-F55D039CE4EF4EEE|
|<p>InventoryInfoList[\*].quantity</p><p></p>|Inventory of child InventoryId per bundle|Integer|Y|10|

#### Response
```json
{
  "groupId": "a8740efa-fa7a-4768-af0d-aeade5451804",
  "status": true
}
```

#### Response Params:
|Field|Description|Datatype|Example|
| :- | :- | :- | :- |
|groupId|New Unique groupId for the updated bundle|String|a8740efa-fa7a-4768-af0d-aeade5451804|
|status|Success status|boolean|true/false|

Curl
```bash
curl --location --request PUT ‘{{HOST}}/api/ims/v1/bundle' \ 
--header 'Content-Type: application/json' \ 
--header 'languageCode: en' \ 
--data-raw '{ 
    "merchantId" : "2f6823d4-8dfb-5", 
    "mergeOrigin" : "B291-E8A4E4F8C7D0E283", 
    "channelId": "PARCEL_NINJA", 
    "groupId" : "a8740efa-fa7a-4768-af0d-aeade5451804", 
    "inventoryInfoList" : [ 
        { 
            "inventoryId" : "B291-F55D039CE4EF4EEE", 
            "quantity" : 10 
        } 
    ] 
}'
```

### Delete Bundle
- **Description**: Deletes a bundle and reverts the parent product back to normal product.
- **URL**: /api/ims/v1/bundle
- **Verb**: DELETE

#### Request Headers
|Key|Value|
| :- | :- |
|languageCode|en/fr|

#### Request Params
|Field|Description|Datatype|Mandatory|Example|
| :- | :- | :- | :- | :- |
|merchantId|sellerId|String|Y|2f6823d4-8dfb-5|
|groupId|Unique groupId of bundled product|String|Y|a8740efa-fa7a-4768-af0d-aeade5451804|

#### Response
```json
{
  "status": true
}
```

#### Response Params
|Field|Description|Datatype|Example|
| :- | :- | :- | :- |
|status|Success status|boolean|true/false|

Curl
```bash
curl --location --request DELETE ‘{{HOST}}/api/ims/v1/bundle?merchantId=2f6823d4-8dfb-5&groupId=a8740efa-fa7a-4768-af0d-aeade5451804' \
--header 'languageCode: en’
```

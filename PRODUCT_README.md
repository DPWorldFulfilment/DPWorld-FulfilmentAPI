**Bundle Create API**

Description: Converts a product into bundled product.

URL: {DNS}/ api/ims/v1/bundle

Verb: POST

RequestHeaders:

  -----------------------------------------------------------------------
  Key                                 Value
  ----------------------------------- -----------------------------------
  languageCode                        en/fr

  -----------------------------------------------------------------------

**Request Body:**

{

> \"merchantId\": \"2f6823d4-8dfb-5\",
>
> \"mergeOrigin\": \"B291-E8A4E4F8C7D0E283\",
>
> \"channelId\":\"PARCEL_NINJA\",
>
> \"inventoryInfoList\": \[
>
> {
>
> \"inventoryId\": \"B291-F55D039CE4EF4EEE\",
>
> \"quantity\": 5
>
> },\
> {
>
> \"inventoryId\": \"B291-G85D039CE4EF4ADF\",
>
> \"quantity\": 2
>
> }
>
> \]
>
> }
>
> Request Params:

  ----------------------------------------------------------------------------------------------------------
  Field                                 Description           Datatype   Mandatory   Example
  ------------------------------------- --------------------- ---------- ----------- -----------------------
  merchantId                            sellerId              String     Y           2f6823d4-8dfb-5

  mergeOrigin                           Parent inventory to   String     Y           B291-E8A4E4F8C7D0E283
                                        be made into bundle                          
                                        product                                      

  channelId                             channel               String     Y           PARCEL_NINJA

  inventoryInfoList                     List of child         List       Y           \-
                                        inventory id configs                         
                                        per bundle                                   

  InventoryInfoList\[\*\].inventoryId   Child inventory Id    String     Y           B291-F55D039CE4EF4EEE

  InventoryInfoList\[\*\].quantity      Inventory of child    Integer    Y           5
                                        InventoryId per                              
                                        bundle                                       
  ----------------------------------------------------------------------------------------------------------

Response Body:

{

> \"groupId\": \"a8740efa-fa7a-4768-af0d-aeade5451804\",
>
> \"status\": true
>
> }
>
> Response Params:

  ------------------------------------------------------------------------------------------
  Field       Description                 Datatype    Example
  ----------- --------------------------- ----------- --------------------------------------
  groupId     Unique groupId for the      String      a8740efa-fa7a-4768-af0d-aeade5451804
              created bundle                          

  status      Success status              boolean     true/false
  ------------------------------------------------------------------------------------------

> Sample Curl :\
> curl \--location \--request POST '{{HOST}}api/ims/v1/bundle\' \\
>
> \--header \'Content-Type: application/json\' \\
>
> \--header \'languageCode: en\' \\
>
> \--data-raw \'{
>
> \"merchantId\" : \"2f6823d4-8dfb-5\",
>
> \"mergeOrigin\" : \"B291-E8A4E4F8C7D0E283\",
>
> \"channelId\": \"PARCEL_NINJA\",
>
> \"inventoryInfoList\" : \[
>
> {
>
> \"inventoryId\" : \"B291-F55D039CE4EF4EEE\",
>
> \"quantity\" : 5
>
> }
>
> \]
>
> }\'

1.  **Bundle Update API:**

API Description: Updates the child configuration of a bundled product

Rest URL: {DNS}/ api/ims/v1/bundle

RequestType: PUT

RequestHeaders:

  -----------------------------------------------------------------------
  Key                                 Value
  ----------------------------------- -----------------------------------
  languageCode                        en/fr

  -----------------------------------------------------------------------

**Request Body:**

{

> \"merchantId\": \"2f6823d4-8dfb-5\",
>
> \"mergeOrigin\": \"B291-E8A4E4F8C7D0E283\",
>
> \"channelId\": \"PARCEL_NINJA\",
>
> \"groupId\": \"a8740efa-fa7a-4768-af0d-aeade5451804\",
>
> \"inventoryInfoList\": \[
>
> {
>
> \"inventoryId\": \"B291-F55D039CE4EF4EEE\",
>
> \"quantity\": 10
>
> }
>
> \]
>
> }
>
> Request Params:

  -------------------------------------------------------------------------------------------------------------------------
  Field                                 Description           Datatype   Mandatory   Example
  ------------------------------------- --------------------- ---------- ----------- --------------------------------------
  merchantId                            sellerId              String     Y           2f6823d4-8dfb-5

  mergeOrigin                           Bundled inventory Id  String     Y           B291-E8A4E4F8C7D0E283
                                        to be updated                                

  channelId                             channel               String     Y           PARCEL_NINJA

  groupId                               Unique groupId of     String     Y           a8740efa-fa7a-4768-af0d-aeade5451804
                                        bundled product                              

  inventoryInfoList                     List of updated child List       Y           \-
                                        inventory id configs                         
                                        per bundle                                   

  InventoryInfoList\[\*\].inventoryId   Child inventory Id    String     Y           B291-F55D039CE4EF4EEE

  InventoryInfoList\[\*\].quantity      Inventory of child    Integer    Y           10
                                        InventoryId per                              
                                        bundle                                       
  -------------------------------------------------------------------------------------------------------------------------

Response Body:

{

> \"groupId\": \"a8740efa-fa7a-4768-af0d-aeade5451804\",
>
> \"status\": true
>
> }
>
> Response Params:

  ------------------------------------------------------------------------------------------
  Field       Description                 Datatype    Example
  ----------- --------------------------- ----------- --------------------------------------
  groupId     New Unique groupId for the  String      a8740efa-fa7a-4768-af0d-aeade5451804
              updated bundle                          

  status      Success status              boolean     true/false
  ------------------------------------------------------------------------------------------

> Sample Curl :\
> curl \--location \--request PUT '{{HOST}}/api/ims/v1/bundle\' \\
>
> \--header \'Content-Type: application/json\' \\
>
> \--header \'languageCode: en\' \\
>
> \--data-raw \'{
>
> \"merchantId\" : \"2f6823d4-8dfb-5\",
>
> \"mergeOrigin\" : \"B291-E8A4E4F8C7D0E283\",
>
> \"channelId\": \"PARCEL_NINJA\",
>
> \"groupId\" : \"a8740efa-fa7a-4768-af0d-aeade5451804\",
>
> \"inventoryInfoList\" : \[
>
> {
>
> \"inventoryId\" : \"B291-F55D039CE4EF4EEE\",
>
> \"quantity\" : 10
>
> }
>
> \]
>
> }\'

2.  **Bundle Delete API:**

API Description: Deletes a bundle and reverts the parent product back to
normal product.

Rest URL: {DNS}/ api/ims/v1/bundle

RequestType: DELETE

RequestHeaders:

  -----------------------------------------------------------------------
  Key                                 Value
  ----------------------------------- -----------------------------------
  languageCode                        en/fr

  -----------------------------------------------------------------------

> Request Params:

  ------------------------------------------------------------------------------------------------
  Field        Description           Datatype   Mandatory   Example
  ------------ --------------------- ---------- ----------- --------------------------------------
  merchantId   sellerId              String     Y           2f6823d4-8dfb-5

  groupId      Unique groupId of     String     Y           a8740efa-fa7a-4768-af0d-aeade5451804
               bundled product                              
  ------------------------------------------------------------------------------------------------

Response Body:

{

> \"status\": true
>
> }
>
> Response Params:

  ------------------------------------------------------------------------
  Field       Description                 Datatype    Example
  ----------- --------------------------- ----------- --------------------
  status      Success status              boolean     true/false

  ------------------------------------------------------------------------

> Sample Curl :\
> curl \--location \--request DELETE
> '{{HOST}}/api/ims/v1/bundle?merchantId=2f6823d4-8dfb-5&groupId=a8740efa-fa7a-4768-af0d-aeade5451804\'
> \\
>
> \--header \'languageCode: en'


<a name="getproductsbyname"></a>
### Returns details of single product based on productName parameter
```
GET /data/privacy/gdpr/products/{productName}
```


#### Description
Returns details of a product.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Bearer XXXXX|string|
|**Header**|**Content-Type**  <br>*required*|application/json|string|
|**Header**|**x-api-key**  <br>*required*|acp_XXX_XXXX, IMS Client id which is whitelisted and subscribed to consume services on adobe.io|string|
|**Header**|**x-gw-ims-org-id**  <br>*required*|XXXXX47E56F59C747FXXXXX@AdobeOrg|string|
|**Path**|**productName**  <br>*required*|Product Name for details|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Successful retrieval of product details|[Product](../definitions/Product.md#product)|
|**404**|No Products found in the system|No Content|
|**417**|Expectation Failed!! Validation failed|No Content|
|**500**|Internal server error|No Content|
|**503**|Exception Occurred!!|No Content|


#### Tags

* GDPR Product Management CRUD API


#### Example HTTP request

##### Request path
```
/data/privacy/gdpr/products/string
```


##### Request header
```
json :
"string"
```


#### Example HTTP response

##### Response 200
```
json :
{
  "productId" : 0,
  "productName" : "string",
  "inUse" : true,
  "createdOn" : "string",
  "createdBy" : "string",
  "comments" : "string",
  "responseThreshold" : 0,
  "statusCode" : "string",
  "statusMessage" : "string"
}
```




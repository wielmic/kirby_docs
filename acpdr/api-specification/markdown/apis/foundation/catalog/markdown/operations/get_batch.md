
<a name="get_batch"></a>
### Fetches a list of Batches.
```
GET /batches
```


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-api-key**  <br>*required*|The API key belonging to the calling client.|string|
|**Header**|**x-gw-ims-org-id**  <br>*required*|The owning IMS organization identifier.|string|
|**Query**|**batch**  <br>*optional*|Used to filter on the related object: &batch=batchId.|string|
|**Query**|**completed**  <br>*optional*|Filter by the Unix timestamp (in milliseconds) when the Batch processing action was completed. Completed - Started should yield the total processing time.|integer (int64)|
|**Query**|**connection**  <br>*optional*|Used to filter on the related object: &connection=connectionId.|string|
|**Query**|**connector**  <br>*optional*|Used to filter on the related object: &connector=connectorId.|string|
|**Query**|**created**  <br>*optional*|Filter by the Unix timestamp (in milliseconds) when this object was persisted.|integer (int64)|
|**Query**|**createdAfter**  <br>*optional*|Exclusively filter records created after this timestamp.|integer (int64)|
|**Query**|**createdBefore**  <br>*optional*|Exclusively filter records created before this timestamp.|integer (int64)|
|**Query**|**createdClient**  <br>*optional*|Filter by the ID of the IMS client that created this object.|string|
|**Query**|**createdUser**  <br>*optional*|Filter by the  ID of the user who created this object.|string|
|**Query**|**dataSet**  <br>*optional*|Used to filter on the related object: &dataSet=dataSetId.|string|
|**Query**|**dataSetFile**  <br>*optional*|Used to filter on the related object: &dataSetFile=dataSetFileId.|string|
|**Query**|**dataSetView**  <br>*optional*|Used to filter on the related object: &dataSetView=dataSetViewId.|string|
|**Query**|**endAfter**  <br>*optional*|Query only batches with availability dates that end after the specified timestamp.|integer (int64)|
|**Query**|**endBefore**  <br>*optional*|Query only batches with availability dates that end before the specified timestamp.|integer (int64)|
|**Query**|**failedRecordCount**  <br>*optional*|Filter by the number of records that could not be processed in this Batch.|integer (int64)|
|**Query**|**limit**  <br>*optional*|Limit response to a specified number of objects. Ex. limit=10|integer|
|**Query**|**orderBy**  <br>*optional*|Sort parameter and direction for sorting the response. Ex. orderBy=asc:created,updated. This was previously called sort.|string|
|**Query**|**properties**  <br>*optional*|A comma separated whitelist of top-level object properties to be returned in the response. Used to cut down the number of properties and amount of data returned in the response bodies.|string|
|**Query**|**properties**  <br>*optional*|A comma separated whitelist of top-level object properties to be returned in the response. Used to cut down the number of properties and amount of data returned in the response bodies.|string|
|**Query**|**property**  <br>*optional*|Regex used to filter objects in the response. Ex. property=name~^test.|string|
|**Query**|**recordCount**  <br>*optional*|Filter by the total number of data records (rows/documents) processed in this Batch.|integer (int64)|
|**Query**|**size**  <br>*optional*|Number of bytes processed in this Batch.|integer (int64)|
|**Query**|**start**  <br>*optional*|Returns results from a specific offset of objects. This was previously called offset. Ex. start=3.|integer|
|**Query**|**startAfter**  <br>*optional*|Query only batches with availability dates that start after the specified timestamp.|integer (int64)|
|**Query**|**startBefore**  <br>*optional*|Query only batches with availability dates that start before the specified timestamp.|integer (int64)|
|**Query**|**started**  <br>*optional*|Filter by the Unix timestamp (in milliseconds) when the Batch processing action was started.|integer (int64)|
|**Query**|**status**  <br>*optional*|Filter by the current (mutable) status of this Batch.|string|
|**Query**|**transform**  <br>*optional*|Used to filter on the related object: &transform=transformId.|string|
|**Query**|**updated**  <br>*optional*|Filter by the Unix timestamp (in milliseconds) for the time of last modification.|integer (int64)|
|**Query**|**updatedUser**  <br>*optional*|Filter by the  ID of the user who changed this object.|string|
|**Query**|**version**  <br>*optional*|Filter by Semantic version of the account. Updated when the object is modified.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|batch response|< string, [batchResponse](../definitions/batchResponse.md#batchresponse) > map|
|**400**|Bad request|No Content|
|**403**|Forbidden|No Content|
|**404**|Not found|No Content|
|**500**|Internal server error|No Content|
|**default**|Unexpected error|No Content|


#### Produces

* `application/json`


#### Security

|Type|Name|
|---|---|
|**apiKey**|**[Bearer](security.md#bearer)**|


#### Example HTTP request

##### Request path
```
/batches
```


##### Request header
```
json :
"string"
```


##### Request query
```
json :
{
  "batch" : "string",
  "completed" : 0,
  "connection" : "string",
  "connector" : "string",
  "created" : 0,
  "createdAfter" : 0,
  "createdBefore" : 0,
  "createdClient" : "string",
  "createdUser" : "string",
  "dataSet" : "string",
  "dataSetFile" : "string",
  "dataSetView" : "string",
  "endAfter" : 0,
  "endBefore" : 0,
  "failedRecordCount" : 0,
  "limit" : 0,
  "orderBy" : "string",
  "properties" : "string",
  "property" : "string",
  "recordCount" : 0,
  "size" : 0,
  "start" : 0,
  "startAfter" : 0,
  "startBefore" : 0,
  "started" : 0,
  "status" : "string",
  "transform" : "string",
  "updated" : 0,
  "updatedUser" : "string",
  "version" : "string"
}
```


#### Example HTTP response

##### Response 200
```
json :
{
  "5911f88ae2f4bf657c5a8cb5" : {
    "imsOrg" : "4F3BB22C5631222A7F000101@AdobeOrg",
    "created" : 1494349962314,
    "createdClient" : "MCDPCatalogServiceStage",
    "createdUser" : "MCDPCatalogServiceStage@AdobeID",
    "updatedUser" : "MCDPCatalogServiceStage@AdobeID",
    "updated" : 1494349963467,
    "status" : "success",
    "errors" : [ {
      "code" : "err-1494349963436"
    } ],
    "version" : "1.0.3",
    "availableDates" : {
      "startDate" : 1337,
      "endDate" : 4000
    },
    "relatedObjects" : [ {
      "type" : "batch",
      "id" : "foo_batch"
    }, {
      "type" : "connection",
      "id" : "foo_connection"
    }, {
      "type" : "connector",
      "id" : "foo_connector"
    }, {
      "type" : "dataSet",
      "id" : "foo_dataSet"
    }, {
      "type" : "dataSetView",
      "id" : "foo_dataSetView"
    }, {
      "type" : "dataSetFile",
      "id" : "foo_dataSetFile"
    }, {
      "type" : "expressionBlock",
      "id" : "foo_expressionBlock"
    }, {
      "type" : "service",
      "id" : "foo_service"
    }, {
      "type" : "serviceDefinition",
      "id" : "foo_serviceDefinition"
    } ],
    "metrics" : {
      "foo" : 1337
    },
    "tags" : {
      "foo_bar" : [ "stuff" ],
      "bar_foo" : [ "woo", "baz" ],
      "foo/bar/foo-bar" : [ "weehaw", "wee:haw" ]
    }
  }
}
```




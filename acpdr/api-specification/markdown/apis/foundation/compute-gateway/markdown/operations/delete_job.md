
<a name="delete_job"></a>
### Deletes the specified Spark job
```
DELETE /data/foundation/compute/jobs/{jobID}
```


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-api-key**  <br>*required*|The API key belonging to the calling client.|string|
|**Header**|**x-request-id**  <br>*optional*|A unique id generated by Adobe.io.|string|
|**Path**|**jobID**  <br>*required*|Job ID|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**202**|Spark job kill request submitted successfully|[Message](../definitions/Message.md#message)|
|**401**|Unauthorized access|[Message](../definitions/Message.md#message)|
|**404**|Job Not Found|[Message](../definitions/Message.md#message)|
|**409**|Job kill requested failed as the job might already have terminated or it was not found on the cluster.|[Message](../definitions/Message.md#message)|
|**414**|Request URI is longer than allowed 2000 chars|[Message](../definitions/Message.md#message)|
|**422**|Input validation failure|[Message](../definitions/Message.md#message)|
|**503**|Kill request submission failed|[Message](../definitions/Message.md#message)|


#### Produces

* `application/json`


#### Tags

* ComputeJobs


#### Example HTTP request

##### Request path
```
/data/foundation/compute/jobs/4b3c4fae-212c-404f-9565-9b3fa0a9cb4f
```


##### Request header
```
json :
"string"
```


#### Example HTTP response

##### Response 202
```
json :
{
  "message" : "string",
  "error_code" : "string"
}
```


##### Response 401
```
json :
{
  "message" : "string",
  "error_code" : "string"
}
```


##### Response 404
```
json :
{
  "message" : "string",
  "error_code" : "string"
}
```


##### Response 409
```
json :
{
  "message" : "string",
  "error_code" : "string"
}
```


##### Response 414
```
json :
{
  "message" : "string",
  "error_code" : "string"
}
```


##### Response 422
```
json :
{
  "message" : "string",
  "error_code" : "string"
}
```


##### Response 503
```
json :
{
  "message" : "string",
  "error_code" : "string"
}
```




<a name="retrieveexperiments"></a>
### Get All Experiments for an ML Instance
```
GET /experiments
```


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**x-gw-ims-org-id**  <br>*required*|IMS org id of the caller|string||
|**Query**|**limit**  <br>*optional*|Limit value for pagination. Indicates the requested number of items to return. The service may return a different number of items than requested.|integer (int32)|`25`|
|**Query**|**orderby**  <br>*optional*|Sort order for pagination. Indicates the fields and direction to use for sorting in priority order.|< string > array(csv)||
|**Query**|**property**  <br>*optional*|Property matching expression for filtering paginated results. Indicates the comparision expression that items must match in order to be returned.|< string > array(csv)||
|**Query**|**start**  <br>*optional*|Start value for pagination. Indicates the starting index for the items to return.|string||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|List of Experiments|[ExperimentListing](../definitions/ExperimentListing.md#experimentlisting)|
|**400**|Bad request|[SenseiApiResponse](../definitions/SenseiApiResponse.md#senseiapiresponse)|
|**401**|Unauthorized|[SenseiApiResponse](../definitions/SenseiApiResponse.md#senseiapiresponse)|
|**403**|Forbidden|[SenseiApiResponse](../definitions/SenseiApiResponse.md#senseiapiresponse)|
|**406**|Unacceptable|[SenseiApiResponse](../definitions/SenseiApiResponse.md#senseiapiresponse)|
|**500**|Internal Server Error|[SenseiApiResponse](../definitions/SenseiApiResponse.md#senseiapiresponse)|
|**502**|Bad Gateway|[SenseiApiResponse](../definitions/SenseiApiResponse.md#senseiapiresponse)|
|**503**|Service Unavailable|[SenseiApiResponse](../definitions/SenseiApiResponse.md#senseiapiresponse)|
|**504**|Gateway Timeout|[SenseiApiResponse](../definitions/SenseiApiResponse.md#senseiapiresponse)|


#### Produces

* `application/vnd.adobe.platform.sensei+json;profile=experimentListing.v1.json`


#### Tags

* Experiment


#### Example HTTP request

##### Request path
```
/experiments
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
  "limit" : 0,
  "orderby" : "string",
  "property" : "string",
  "start" : "string"
}
```


#### Example HTTP response

##### Response 200
```
json :
{
  "children" : [ {
    "id" : "string",
    "name" : "string",
    "mlInstanceId" : "string",
    "mlInstanceQuery" : "string",
    "description" : "string",
    "created" : "string",
    "createdBy" : "object",
    "updated" : "string",
    "deleted" : true,
    "workflowId" : "string",
    "_links" : "object"
  } ],
  "_page" : {
    "orderby" : "string",
    "property" : "string",
    "start" : "string",
    "count" : 0,
    "next" : "string"
  },
  "_links" : {
    "next" : {
      "href" : "string",
      "templated" : true,
      "type" : "string",
      "method" : "string",
      "title" : "string",
      "hrefLang" : "string"
    },
    "page" : {
      "href" : "string",
      "templated" : true,
      "type" : "string",
      "method" : "string",
      "title" : "string",
      "hrefLang" : "string"
    },
    "self" : {
      "href" : "string",
      "templated" : true,
      "type" : "string",
      "method" : "string",
      "title" : "string",
      "hrefLang" : "string"
    },
    "createExperiment" : {
      "href" : "string",
      "templated" : true,
      "type" : "string",
      "method" : "string",
      "title" : "string",
      "hrefLang" : "string"
    }
  }
}
```


##### Response 400
```
json :
{
  "type" : "https://platform.adobe.io/data/foundation/ml/problems/illegal-argument",
  "title" : "Illegal Argument",
  "status" : 400,
  "detail" : "Model specification name must not be empty",
  "additionalDetails" : {
    "string" : "string"
  }
}
```


##### Response 401
```
json :
{
  "type" : "https://platform.adobe.io/data/foundation/ml/problems/illegal-argument",
  "title" : "Illegal Argument",
  "status" : 400,
  "detail" : "Model specification name must not be empty",
  "additionalDetails" : {
    "string" : "string"
  }
}
```


##### Response 403
```
json :
{
  "type" : "https://platform.adobe.io/data/foundation/ml/problems/illegal-argument",
  "title" : "Illegal Argument",
  "status" : 400,
  "detail" : "Model specification name must not be empty",
  "additionalDetails" : {
    "string" : "string"
  }
}
```


##### Response 406
```
json :
{
  "type" : "https://platform.adobe.io/data/foundation/ml/problems/illegal-argument",
  "title" : "Illegal Argument",
  "status" : 400,
  "detail" : "Model specification name must not be empty",
  "additionalDetails" : {
    "string" : "string"
  }
}
```


##### Response 500
```
json :
{
  "type" : "https://platform.adobe.io/data/foundation/ml/problems/illegal-argument",
  "title" : "Illegal Argument",
  "status" : 400,
  "detail" : "Model specification name must not be empty",
  "additionalDetails" : {
    "string" : "string"
  }
}
```


##### Response 502
```
json :
{
  "type" : "https://platform.adobe.io/data/foundation/ml/problems/illegal-argument",
  "title" : "Illegal Argument",
  "status" : 400,
  "detail" : "Model specification name must not be empty",
  "additionalDetails" : {
    "string" : "string"
  }
}
```


##### Response 503
```
json :
{
  "type" : "https://platform.adobe.io/data/foundation/ml/problems/illegal-argument",
  "title" : "Illegal Argument",
  "status" : 400,
  "detail" : "Model specification name must not be empty",
  "additionalDetails" : {
    "string" : "string"
  }
}
```


##### Response 504
```
json :
{
  "type" : "https://platform.adobe.io/data/foundation/ml/problems/illegal-argument",
  "title" : "Illegal Argument",
  "status" : 400,
  "detail" : "Model specification name must not be empty",
  "additionalDetails" : {
    "string" : "string"
  }
}
```




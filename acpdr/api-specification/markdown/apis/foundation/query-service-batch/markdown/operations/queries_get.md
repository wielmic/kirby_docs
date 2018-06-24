
<a name="queries-get"></a>
### Fetches a list of queries for this IMS organization.
```
GET /queries
```


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-api-key**  <br>*required*|API key|string|
|**Header**|**x-gw-ims-org-id**  <br>*required*|The owning IMS organization identifier.|string|
|**Header**|**x-request-id**  <br>*optional*|A unique id generated by Adobe.io|string|
|**Query**|**limit**  <br>*optional*|Hint on number of records to fetch per page.|integer|
|**Query**|**orderby**  <br>*optional*|Field to order results by. Supported fields: created, updated. Prepend property name with + for ASC,- for DESC order.|string|
|**Query**|**property**  <br>*optional*|Comma separated property filters. Supported filters are on created, updated, state and id. e.g created>=2017-04-05T13:30:00Z,state==TASK_RUNNING|string|
|**Query**|**start**  <br>*optional*|Start value of property specified using orderby.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Query response|[Response 200](#queries-get-response-200)|
|**401**|Unauthorized|No Content|
|**404**|Not Found|No Content|
|**500**|Internal Server Error|No Content|

<a name="queries-get-response-200"></a>
**Response 200**

|Name|Description|Schema|
|---|---|---|
|**_links**  <br>*optional*|**Example** : `"object"`|[_links](#queries-get-links)|
|**_page**  <br>*optional*|**Example** : `"[page](#page)"`|[_page](../definitions/page.md#page)|
|**queries**  <br>*optional*|**Example** : `[ "[query_status](#query_status)" ]`|< [query_status](../definitions/query_status.md#query_status) > array|
|**version**  <br>*optional*|REST API version of this resource  <br>**Example** : `0`|integer|

<a name="queries-get-links"></a>
**_links**

|Name|Description|Schema|
|---|---|---|
|**next**  <br>*optional*|**Example** : `"[next](#next)"`|[next](../definitions/next.md#next)|


#### Produces

* `application/json`


#### Security

|Type|Name|
|---|---|
|**apiKey**|**[Bearer](security.md#bearer)**|


#### Example HTTP request

##### Request path
```
/queries
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
"object"
```



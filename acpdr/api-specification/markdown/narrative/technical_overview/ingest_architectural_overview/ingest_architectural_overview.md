# Batch Ingestion Overview


The Batch Ingestion API allows you to ingest data into Adobe Experience Platform as batch files. Data being ingested can be the profile data from a flat file in a CRM system (such as a parquet file), or data that conforms to a known schema in the Experience Data Model (XDM) registry.

![](batch_ingestion.png)

See the [Batch Ingestion API](../../../../../../acpdr/swagger-specs/bulk-ingest-api.yaml) reference for additional information.

## Using the API

The Data Ingestion API allows you to ingest data as batches (a unit of data that consists of one or more files to be ingested as a single unit) into Experience Platform in three basic steps:

1. Create a new batch. 
2. Upload files to a specified dataset that matches the XDM schema of the data. 
3. Signal the end of the batch. 


### Data Ingestion Prerequisites
- Data to upload must be either in [parquet](http://parquet.apache.org/documentation/latest/) or [JSON format][xdm-json].
- A dataset created in the [Catalog services](../catalog_architectural_overview/catalog_architectural_overview.md).
- Contents of the parquet file must match a subset of the schema of the dataset being uploaded into.
- Have your unique Access Token after authentication.

### Batch Ingestion Best Practices

- The recommended batch size is between 256 MB and 100 GB.
- Each batch should contain at most 1500 files.

To upload a file larger than 512MB, the file will need to be divided into smaller chunks. Instructions to upload a large file can be found [here](#large-file-upload---create-file).


### Creating a Batch

Before data can be added to a dataset, it must be linked to a batch, which will later be uploaded into a specified dataset.

```http
POST /batches
```

#### Request

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

`{IMS_ORG}`: Your IMS organization credentials found in your unique Adobe Experience Platform integration.  
`{ACCESS_TOKEN}`: Token provided after authentication.  
`{API_KEY}`: Your specific API key value found in your unique Adobe Experience Platform integration.  
`{DATASET_ID}`: The ID of the dataset to upload the files into.

#### Response

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```
`{BATCH_ID}`: The ID of the batch that was just created (used in subsequent requests).  
`{IMS_ORG}`: Your IMS organization specified in the request.  
`{DATASET_ID}`: The ID of the dataset to upload the files into.


## File Upload
After successfully creating a new batch for uploading, files can then be uploaded to a specific dataset.

You can upload files using the **Small File Upload API**. However, if your files are too large and the gateway limit is exceeded (such as extended timeouts, requests for body size exceeded, and other constrictions), you can switch over to the **Large File Upload API**. This API uploads the file in chunks, and stitches data together using the **Large File Upload Complete API** call.

### Small File Upload
Once a batch is created, data can be uploaded to a preexisting dataset.  The file being uploaded must match its referenced XDM schema.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

#### Request

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

`{BATCH_ID}`: The ID of the batch.  
`{DATASET_ID}`: The ID of the dataset to upload files.  
`{FILE_NAME}`: Name of file as it will be seen in the dataset.  
`{IMS_ORG}`: Your IMS organization credentials for your unique Adobe Experience Platform integration.  
`{ACCESS_TOKEN}`: Token provided after authentication.  
`{FILE_PATH_AND_NAME}`: The path and filename of the file to be uploaded into the dataset.  

#### Response
```JSON
#Status 200 OK, with empty response body
```

### Large File Upload - Create File
To upload a large file, the file must be split into smaller chunks and uploaded one at a time.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

#### Request

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```
`{BATCH_ID}`: The ID of the batch.  
`{DATASET_ID}`: The ID of the dataset ingesting the files.  
`{IMS_ORG}`: Your IMS organization credentials found in your unique Adobe Experience Platform integration.  
`{ACCESS_TOKEN}`: Token provided after authentication.  
`{API_KEY}`: Your specific API key value found in your unique Adobe Experience Platform integration.  

#### Response
```JSON
#Status 201 CREATED, with empty response body
```

### Large File Upload - Upload Subsequent Parts
After the file has been created, all subsequent chunks can be uploaded by making repeated PATCH requests, one for each section of the file.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

#### Request

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

`{BATCH_ID}`: The ID of the batch.  
`{DATASET_ID}`: The ID of the dataset to upload the files into.  
`{FILE_NAME}`:Name of file as it will be seen in the dataset.  
`{IMS_ORG}`: Your IMS organization credentials found in your unique Adobe Experience Platform integration.  
`{ACCESS_TOKEN}`: Token provided after authentication.  
`{FILE_PATH_AND_NAME}`: The path and filename of the file to be uploaded into the dataset.  
`{CONTENT_RANGE}`: The range of bytes of the file being uploaded with this request. (for example: 0-82/164)  

#### Response
```JSON
#Status 200 OK, with empty response
```

### Signal Batch Completion
After all files have been uploaded to the batch, the batch can be signaled for completion. By doing this, the Catalog **DataSetFile** entries are created for the completed files and associated with the batch generated above. The Catalog batch is then marked as successful, which triggers downstream flows to ingest the available data.

#### Request
```http
POST /batches/{BATCH_ID}?actions=COMPLETE
```

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

`{BATCH_ID}`: The ID of the batch to be uploaded into the dataset.  
`{IMS_ORG}`: Your IMS organization credentials found in your unique Adobe Experience Platform integration.  
`{ACCESS_TOKEN}`: Token provided after authentication.  
`{API_KEY}`: Your specific API key value found in your unique Adobe Experience Platform integration.  

#### Response
```JSON
#Status 200 OK, with empty response
```

### Check Batch Status
While waiting for the files to uploaded to the batch, the batch's status can be checked to see its progress.

```http
GET /batch/{BATCH_ID}
```

#### Request

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key: {API_KEY}"
```

#### Response

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}

```

`{BATCH_ID}`: The ID of the batch to be uploaded into the dataset.  
`{IMS_ORG}`: Your IMS organization credentials found in your unique Adobe Experience Platform integration.  
`{USER_ID}`: The ID of the user who created or updated the batch.  

The `"status"` field is what shows the current status of the batch requested. The batches can have one of the following states:

## Batch Ingestion Statuses

Status | Description 
------ | -----------
Abandoned | The batch has not completed in the expected timeframe.
Aborted | An abort operation has **explicitly** been called (via Batch Ingest API) for the specified batch. Once the batch is in a **Loaded** state, it cannot be aborted.
Active |  The batch has been successfully promoted and is available for downstream consumption. This status can be used interchangeably with **Success**.
Deleted | Data for the batch has been completely removed. 
Failed | A terminal state that results from either bad configuration and/or bad data. Data for a failed batch will **not** show up. This status can be used interchangeably with **Failure**.
Inactive | The batch was successfully promoted, but has been reverted or has expired. The batch is no longer available for downstream consumption.
Loaded | Data for the batch is complete and the batch is ready for promotion.
Loading | Data for this batch is being uploaded and the batch is currently **not** ready to be promoted.
Retrying | The data for this batch is being processed. However, due to a system or transient error, the batch failed - as a result, this batch is being retried.
Staged | The staging phase of the promotion process for a batch is complete and the ingestion job has been run.
Staging | Data for the batch is being processed.
Stalled | The data for the batch is being processed. However, the batch promotion has stalled after a number of retries.

[xdm-json]: ../schema_registry/acp_schema_registry.md
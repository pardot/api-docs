# Import API Overview

The Import API provides a programmatic way to insert or update large amounts of data into Pardot. It makes use of Pardot's existing API structures, patterns, and terminology. It aims to automate the existing [Import feature set](https://help.salesforce.com/articleView?id=pardot_prospects_import.htm&type=0). Currently only Prospect import is supported.

The functionality described is available only if your Pardot org has the API Import feature enabled. This feature is **disabled** by default for all accounts & editions.

## When to Use the Import API

The Import API is intended for use when inserting or updating large sets of data and when synchronous responses indicating completion are not required. Currently, only Prospect upsert is supported. The Import API should be used if the limitations of [batch upsert](http://developer.pardot.com/kb/api-version-4/prospects/#upserting-prospects) are too restrictive to meet your use case. 

The Import API is intended to process many records asynchronously in batches. Generally, the larger the batch, the more efficiency can be gained. Each batch requires a minimum amount of system resources in order to process. Thus, small batches are discouraged and may result in slower performance. 

## What You Can Do with the Import API

The Import API allows users to send a CSV file with Prospects to be imported. Columns in the CSV correspond to Pardot Field IDs. Rows correspond to prospects to be upserted. Validation ensures that each column in the CSV **must** match a valid Field ID. Any extraneous columns will cause the CSV to be rejected. 

### Matching & Upsert behavior

If a row in the CSV file can be matched to an existing prospect, all fields specified will be updated. If a matching prospect cannot be found, a new prospect will be created. Any field that is left blank will be overwritten with NULL. All standard and custom fields are supported.

In API Version 3, prospects will be matched by email address. If the prospect that is matched is in the recycle bin, that record will fail to upsert unless the restoreDeleted option was specified during import creation. The rest of the import will continue processing.

## How the Import API Works

A set of records is processed by creating an import that contains one or more batches of data. The import specifies which object is being processed and what type of operation is being used. As stated previously, the only currently supported object is Prospect and the only currently supported operation is Upsert. A batch is a set of records sent to the server in an HTTP POST request.

Processing of import batches is done in parallel and batches are subdivided into smaller groups of objects for processing. Order of processing for individual records, batches, and entire imports is not guaranteed. In particular, if one import is submitted before a subsequent import is completed, processing timeframes for these may overlap.

The import is represented in the API with the Import resource. This resource is used to create a new import, get status for an existing import, upload data as a batch, and change status for an import. A batch is created by submitting a CSV representation of a set of records in an HTTP POST request. When created, the status of the batch is represented on the Import resource. When complete, the result for failed records is available in a result set resource. All other records are assumed to be successful.

Processing data typically consists of the following steps.

1. Create a new import that specifies the object and action
2. Send data to the server as a batch.
3. Once data has been submitted, set the state of the import to be ready for processing. Once set, no more data can be submitted as part of the import.
4. Check the status of the import at a reasonable interval. Each status check returns the state of the import.
5. When the import is complete, statistics will be made available for creates, updates, and failures. If there are failures, a URI will be made available to download them.
    1. This URI is another API endpoint, which follows the same authentication rules as other Pardot API endpoints.
    2. Failure results will include only the records which failed to be inserted or updated.

Once the import is set to be ready for processing, it cannot be aborted. Any imports left open will be expired after 24 hours.

## Limitations

* An account is limited to 10,000 batches per day
* Each batch may be no more than 10MB
* The above two limits result in a daily limit of 100GB
* Each import may contain no more than 10 batches.

## Expiration

When an import has been in the system for a specific amount of time, it will expire. When expired, imports will not be able to be changed and data about the import will be removed.

An import will expire under these conditions:

1. An import is Complete and the last update was 7 days prior. This allows for data to be retrieved 7 days after the completion of an import.
2. An import is Open and is older than 24 hours. This expiration happens regardless of if a batch has been added to the import or not. An import is considered “Open” after it is created but before the state has been updated to “Ready”.

# Getting Started

This document assumes the end user is already familiar with connecting to the Pardot API, managing Prospects, and creating CSV files. Given those assumptions, a user can begin importing data by using the following endpoints.

---

# Create

/api/import/version/3/do/create

Used to create a new asynchronous import. If a batch of import data is included in this request, the import may be submitted for processing as part of this operation. Otherwise one or more batches may created and associated with this import using the do/batch endpoint and the import may be submitted for processing with the do/update endpoint.

## POST

### Params

### Request Body

ContentType: application/json or multipart/form-data

Use multipart/form-data if sending prospect data in the create request. Use application/json if subsequent do/batch requests will be made with prospect data.

* Input Representation (sent as "**importInput**" if ContentType is multipart/form-data):
    * **operation**: The operation to be executed. Currently only “Upsert” is available. See Import Operation enum for more information.
    * **object**: The current object to be run the import against. Currently only “Prospect” is available. See Import Object enum for more information.
    * **restoreDeleted**: (Optional) If a record within the CSV file matches a record that is has been moved to the Recycle Bin (usually through a Delete), the record can be restored and updated. If the property is true, then the record will be restored and updated. If false, the record is ignored and an error occurs (which appears in the error document after the import has completed). Default if not specified is false.
    * **state**: (Optional) Specify "Ready" to indicate that the CSV file included in the request contains all prospects for this import. In this case, do/batch and do/update requests are not required and should be omitted.

```json
{
    "operation": "Upsert",
    "object": "Prospect",
    "restoreDeleted": boolean,
    "state": "Ready"
}
```

A single part with the name "**importFile**" should contain the CSV file for the batch. The file should contain a header row.

### Success

* Status Code: 200
* Output Representation
    * **id**: The id of the import.
    * **state**: The state of the import, which should always be returned as “Open” or "Waiting". "Waiting" will only be returned if the "Ready" state was specified in the input. See Import State enum.
    * **isExpired**: indicates whether results & errors will be available. 
    * **batchesRef**: (Optional) The full URL path to add batches of data to the import. This will only be included in the response if the import remains in the "Open" state.

```json
{
    "id": int,
    "state": string,
    "isExpired": bool,
    "batchesRef": string : "https://pi.pardot.com/api/import/version/{version}/do/batch/id/{id}"
}
```

### Errors
* Status code: 4xx
* Error codes: See [Error Codes](/kb/error-codes-messages)

---

# Add Batch

/api/import/version/3/do/batch/id/{id}

Allows adding batches of data to an existing import when in the Open state.

## POST

### Params

**{id}**: Id of the import

### Body

ContentType: multipart/form-data

A single part with the name "**importFile**" should contain the CSV file for the batch. The file should contain a header row.

Column names must match [Field Names](http://developer.pardot.com/kb/object-field-references/) in Pardot. For example, to set campaign, pass “campaign_id”. Any extraneous columns or columns that do not match existing field names will cause validation to fail on this step. Each batch must contain an identical header (with the same fields in the same order).

### Limits

* Request size: 10MB is the maximum size we'll accept per batch
* Number of batches per import: 10 batch per import
* Number of batches per day: 10000

### Success

* Status Code: 204
* Output Representation: Empty Body

### Errors
* Status code: 4xx
* Error codes: See [Error Codes](/kb/error-codes-messages)

---

# Update

/api/import/version/3/do/update/id/{id}

 Used to signal that all batches have been added for this import and processing can begin. Moves state from Open to Ready.

## PATCH

Params

**{id}**: Id of the import

### Body

ContentType: application/json

```json
{
    "state": "Ready" // see State enum
}
```

### Success

* Status Code: 200

```json
{
    "id": {id},
    "state": "Waiting",
    "isExpired": bool
}
```

### Errors

* Status code: 4xx
* Error codes: See [Error Codes](/kb/error-codes-messages)

---

# Read

/api/import/version/3/do/read/id/{id}

Returns the current state of the import. If processing has been completed, will provide path to the results of the operation along with any statistics about the operation.

## GET

### Params

**{id}**: Id of the import

### Success

* Status Code: 200
* Output Representation
    * **id**: the id of the import
    * **state**: the current state of the import. See Import State enum.
    * **isExpired**: indicates whether results & errors will be available. 
    * When import state is “Open”:
        * **batchesRef**: the full url path to add batches of data to the import
    * When processing is complete:
        * **createdCount**: count of prospects created
        * **updatedCount**: count of prospects updated
        * If **isExpired** is false:
            * If there are errors:
                * **errorsRef**: full URL path to retrieve errors CSV
                * **errorCount**: count of error operations

```json
{
    "id": int,
    "state": string,
    "isExpired": int
    // if state is "Complete"
    "createdCount": int,
    "updatedCount": int,
    "errorsRef": string : "https://pi.pardot.com/api/import/version/{version}/do/downloadErrors/id/{id}",
    "errorCount": int
}
```

### Errors

* Status code: 4xx
* Error codes: See [Error Codes](/kb/error-codes-messages)

---

# Download Errors

/api/import/version/3/do/downloadErrors/id/{id}

Download errors associated with the specified import (after it has completed).

## GET

### Params

**{id}**: Id of the import

### Success

CSV data with error info for any rows that failed to result in inserts or updates.

### Errors

* Status code: 4xx
* Error codes: See [Error Codes](/kb/error-codes-messages)

---

# Enums

## Import State

* "Open"              : The import has been created and can have batches added
* "Ready"             : All import have been added and is ready to be processed
* "Waiting"           : The import has been signaled ready for processing and is waiting to be picked up by a processing agent.
* "Processing"        : The import batches are being processed
* "Complete"          : All batches completed and results are ready to be consumed

## Import Operation

* "Upsert"    : Upsert objects

## Object

* "Prospect" : Operate on Prospect


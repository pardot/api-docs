# Import API Overview

The Import API provides a programmatic way to insert or update large amounts of data in Pardot. It uses Pardot's existing API structures, patterns, and terminology. The Import API automates the existing prospect [import feature set](https://help.salesforce.com/articleView?id=pardot_prospects_import.htm&type=0). Only prospect import is supported currently.

The functionality described is available only if your Pardot org has the API Import feature enabled. This feature is **disabled** by default for all accounts & editions.

## When to Use the Import API

Use the Import API to insert or update large sets of data, when you don't require synchronous completion responses, or when [batch upsert limitations](http://developer.pardot.com/kb/api-version-4/prospects/#upserting-prospects) are too restrictive. Currently, only Prospect upsert is supported.

The Import API processes many records asynchronously in batches. Each batch requires a minimum amount of system resources to run, so larger batches are generally more efficient. Small batches may result in slower performance.

## What You Can Do with the Import API

The Import API lets you import a CSV file of prospects. Columns in the CSV correspond to Pardot field names. Rows correspond to prospects to be upserted. Each column must match a valid field name, or validation fails and the CSV is rejected.

### Matching & Upsert behavior

If a row in the CSV file matches an existing prospect, all fields specified are updated. A new prospect is created when a matching prospect isn't found. Any blank field is overwritten with NULL. All standard and custom fields are supported.

In API Version 3, prospects are matched by email address. If the matched prospect is in the recycle bin, that record won't upsert unless the `restoreDeleted` option was specified during import creation. The rest of the import isn't affected when a record is skipped.

## How the Import API Works

An import contains a set of records divided into one or more batches of data. A batch is a set of records sent to the server in an HTTP POST request. The import specifies which object is processed and what type of operation is used. The Import API currently supports only the Prospect object and the Upsert operation.

Batches are processed in parallel, and batches are subdivided into smaller groups of objects for processing.

The order in which individual records, batches, and entire imports are processed is not guaranteed.

The Import resource is used to create an import, get status for an import, upload data as a batch, and change status for an import. When a batch has completed processing, the result for failed records is available in a result set resource. All other records are assumed to be successful.

Processing data typically consists of the following steps.

1. Create an import that specifies object and action.
2. Send data to the server as a batch.
3. After you finish submitting data, set the state of the import to "Ready". When the import state is set to ready for processing, no more data can be added.
4. Check the status of the import at a reasonable interval. Each status check returns the state of the import.
5. When the import is complete, statistics become available for creates, updates, and failures. If there are failures, a URI to download them is available.
    1. The URI is an API endpoint, and follows the same authentication rules as other Pardot API endpoints.
    2. The failure results include only the records that weren't inserted or updated.

Once the import is set to be ready for processing, it cannot be aborted. Any imports left open will be expired after 24 hours.

## Limitations

* Each account can process 1000 batches per day.
* Each batch must be smaller than 10MB.
* The daily data limit is 10GB.
* Each import can contain up to 10 batches.

## Expiration

When an import expires, it can't be changed and data about the import is removed.

Imports expire in these situations:

* An import is Complete and the last update was 7 days prior. This allows for data to be retrieved 7 days after the completion of an import.
* The import is has been in the Open state for 24 hours, regardless of whether a batch has been added. An import is open until its state has been updated to “Ready”.

# Getting Started

This document assumes that you're already familiar with connecting to the Pardot API, managing prospects, and creating CSV files. You can import data by using these endpoints.

---

# Create

/api/import/version/3/do/create

Used to create a new asynchronous import. If a batch of import data is included in this request, the import can be submitted for processing as part of this operation. Otherwise one or more batches can be created and associated with this import using the do/batch endpoint and the import can be submitted for processing with the do/update endpoint.

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
    * **id**: The ID of the import.
    * **state**: The state of the import, which should always be returned as “Open” or "Waiting". "Waiting" will only be returned if the "Ready" state was specified in the input. See Import State enum.
    * **isExpired**: Indicates whether results & errors will be available. 
    * **batchesRef**: (Optional) The full URL path to add batches of data to the import. This will only be included in the response if the import remains in the "Open" state.

```json
{
    "id": int,
    "state": string,
    "isExpired": boolean,
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

**{id}**: The ID of the import.

### Body

ContentType: multipart/form-data

A single part with the name "**importFile**" should contain the CSV file for the batch. The file should contain a header row.

Column names must match [Field Names](http://developer.pardot.com/kb/object-field-references/) in Pardot. For example, to set campaign, pass “campaign_id”. Columns that do not match existing field names cause validation to fail on this step. Each batch must contain an identical header (with the same fields in the same order).

### Limits

* Each account can process 1000 batches per day.
* Each batch must be smaller than 10MB.
* The daily data limit is 10GB.
* Each import can contain up to 10 batches.

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

**{id}**: The ID of the import.

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
    "isExpired": boolean
}
```

### Errors

* Status code: 4xx
* Error codes: See [Error Codes](/kb/error-codes-messages)

---

# Read

/api/import/version/3/do/read/id/{id}

Returns the current state of the import. If processing is complete, the output provides path to the results of the operation along with any statistics about the operation.

## GET

### Params

**{id}**: The ID of the import.

### Success

* Status Code: 200
* Output Representation
    * **id**: The ID of the import.
    * **state**: The current state of the import. See Import State enum.
    * **isExpired**: Indicates whether results & errors will be available. 
    * When import state is “Open”:
        * **batchesRef**: The full url path to add batches of data to the import.
    * When processing is complete:
        * **createdCount**: Count of prospects created.
        * **updatedCount**: Count of prospects updated.
        * If **isExpired** is false:
            * If there are errors:
                * **errorsRef**: The full URL path to retrieve errors CSV.
                * **errorCount**: Count of error operations.

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

Download errors associated with the specified import (after it is complete).

## GET

### Params

**{id}**: The ID of the import.

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


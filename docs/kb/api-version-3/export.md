# Export API Overview

The Export API provides a way to retrieve large volumes of data from Pardot. It uses Pardot's existing API
structures, patterns, and terminology. Only visitor activity is supported currently.

# When to Use the Export API

Use the Export API to retrieve large sets of data, when you don't need synchronous completion responses or when query limitations are too restrictive. Currently only visitor activity can be queried.

# How the Export API Works

An export is associated to a query and data set within Pardot. When an export is created, the query is split into many queries for smaller sets of data. These smaller queries are then processed in parallel and the retrieved data is saved as CSV files. When the export is complete, the CSV files will be available to download.

The order of the records returned in the CSV files is not guaranteed. The number of records varies within each CSV file however all files associated to an export will comprise the full data set of the query.

The Export resource is used to create an export and get the status of an export. When the export is complete, the links to the CSV files containing the data will be available in the resource.

Users create and retrieve results of exports with the following steps.

1. Create an export that specifies the object, procedure and arguments.
2. Check the status of the export at a reasonable interval. We recommend that you wait a few minutes between calls. Calls to check export status will count against API call limits. When the results of the status checks indicate a complete export, the results will also contain links to download the records as CSV files.

Data associated to an export will expire after 7 days.

# Limitations

* The daily Pardot API call limit and the concurrent Pardot API call limit apply to Export API calls just as they would with any other Pardot API calls.
* Export API calls are executed sequentially for each account, with older exports being processed before newer exports.

# Expiration

The data associated to an export will expire after 7 days. The Export resource will show that the export has expired and all links to the CSV files will be removed. Attempts to retrieve the data after an expiration occurs will result in a failure.

# CSV File Formatting

* The first row contains the name of the field.
* The second row to the end of the file contains the record data.
* Dates are returned in the timezone of the user at the time the user created the export.
    * For example, if a user is in “PST” timezone and creates an export, the dates in the export will be in “PST”. If the a second user is in “EST” timezone and downloads the exported files, the dates in the export will be in “PST
    * If the timezone of a user changes, any previous exports created by the user will have dates formatted in the previous timezone and any new exports will be in the new timezone.
* Dates are returned in the standard Pardot API date format of `YYYY-MM-DD HH:mm:SS`.
* Fields with null values will be represented as an empty value in CSV.

# Procedures

A procedure is a query and execution plan used to effeciently retrieve the associated data. Each object has a different set of procedures.

## Visitor Activity

## filter_by_created_at

Retrieves all of the Visitor Activity records where the `created_at` value is equal or greater than the `created_after` argument and less or equal to the `created_before` argument.

**Abilities**

To create an export with this procedure, the user must have the following:

* “Prospects > Visitors > View“ ability

To view an export with this procedure, the user must have the following:

* “Prospects > Visitors > View“ ability AND
* The user must be the same as the user that created the export

OR

* “Admin > Exports > View”

**Arguments**

* **created_after**: Selects visitor activities that were created after the specified time. The value can be `today`, `yesterday`, `last_7_days`, `this_month`, `last_month`, or a custom time specified in [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) format.
* **created_before**: (Optional) Selects visitor activities that were created before the specified time. This value must be after the value in `created_after`. If this argument is not specified, then no upper boundary is used in the query (and all data after the `created_after` will be returned). The value can be `today`, `yesterday`, `last_7_days`, `this_month`, `last_month`, or a custom time specified in [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) format.

# Getting Started

This document assumes that you're already familiar with connecting to the Pardot API, managing visitor activities, and reading from CSV files.

---

# Create 

```
/api/export/version/3/do/create
```

Used to create an export of an object and procedure.

## POST

### Request Body

Content-Type must be `application/json`.

Input Representation

* **object**: Specifies which object to export. Currently on "visitorActivity" is available.
* **procedure**: The procedure to execute. A procedure is a query and execution plan used to effeciently retrieve the associated data. Each object has a different set of procedures. See the [Procedures](#procedures) section for the list of available procedures.
    * **name**: The name of the procedure to execute.
    * **arguments**: Arguments used to manipulate the behavior of the procedure. These arguments are specific to the procedure. See the documentation for the procedure to see which arguments apply.

```json
{
	"object": string,
	"procedure": {
		"name": string,
		"arguments": {
			"argument name": argument value,
			// additional arguments...
		}
	}
}
}
```

### Success

* Status Code: 200

Output Representation

* **id**: The ID of the export. This ID will be used to check the status of the export.
* **state**: The state of the export. This will display "Waiting" when the export has been queued for processing, "Processing" when the server is working on the export and "Complete" when the export has completed. See [Export State](#export-state) enum.
* **isExpired**: Indicates that the export has expired. After an export has expired, this will return `false` and no data associated to the export can be downloaded.
* **resultsRef**: (Optional) This property will appear only when the export has completed and contains a list of URLS to CSV files available for download. If there is no data associated to the export, this property will be absent. If there is only a single CSV file available for download, this will be a `string` containing the URL to download the file. If there are multiple CSV files, this will be an array of URLs.
* **createdAt**: The date and time the export was created in the timezone of the user making the request.
* **updatedAt**: The date and time the export was updated in the timezone of the user making the request.

```json
{
    "export": {
        "id": int,
        "state": string,
        "isExpired": boolean,
        "resultsRef": string OR string[],
        "createdAt": datetime,
        "updatedAt": datetime
    }
}
```

### Errors

* Status Code: 4xx
* Error codes: See [Error Codes](/kb/error-codes-messages)

### Example

Below is a request to execute the Visitor Activity procedure named `filter_by_created_at`, which retrieves all Visitor Activity data where the `created_at` value is between two dates. In this example, the data will be retrieved
from December 25th, 2019 to December 25th, 2020.

```
POST /api/export/version/3/do/create
HOST: pi.pardot.com
Content-Type: application/json
Authorization: Pardot user_key=U,api_key=A
```

```json
{
    "object": "visitorActivity",
    "procedure": {
        "name": "filter_by_created_at",
        "arguments": {
            "created_after": "2019-12-25 10:00:00",
            "created_before": "2020-12-25 24:59:59"
        }
    }
}
```

After sending the request as a `POST`, the response will be the following. From this response, the export has been queued for execution but has not started nor completed. We suggest waiting a few minutes before checking the Read endpoint for the new status.

```json
{
    "id": 201917,
    "state": "Waiting",
    "isExpired": false
}
```

---

# Read

```
/api/export/version/3/do/read/id/{id}
```

Used to retrieve the status of the export. Once an export is complete, the links to download the results will also be present in the result body.

## GET

### Params

**{id}**: The ID of the export.

### Success

* Status Code: 200

Output Representation

* **id**: The ID of the export. This ID will be used to check the status of the export.
* **state**: The state of the export. This will display "Waiting" when the export has been queued for processing, "Processing" when the server is working on the export and "Complete" when the export has completed. See [Export State](#export-state) enum.
* **isExpired**: Indicates that the export has expired. After an export has expired, this will return `true` and no data associated to the export can be downloaded.
* **resultsRef**: (Optional) This property will appear only when the export has completed and contains a list of URLS to CSV files available for download. If there is no data associated to the export, this property will be absent. If there is only a single CSV file available for download, this will be a `string` containing the URL to download the file. If there are multiple CSV files, this will be an array of URLs. The order of the URLs in the array is not significant.
* **createdAt**: The date and time the export was created in the timezone of the user making the request.
* **updatedAt**: The date and time the export was updated in the timezone of the user making the request.

```json
{
    "export": {
        "id": int,
        "state": string,
        "isExpired": boolean,
        "resultsRef": string OR string[],
        "createdAt": datetime,
        "updatedAt": datetime
    }
}
```

### Errors

* Status Code: 4xx
* Error codes: See [Error Codes](/kb/error-codes-messages)


### Example

After calling the Create endpoint, the ID of the export will be given in the response. This ID will be used
in the URL to call the Read endpoint.

```
GET /api/export/version/3/do/read/id/201917
HOST: pi.pardot.com
Content-Type: application/json
Authorization: Pardot user_key=U,api_key=A
```

If the export is waiting to be processed, the `state` property will be "Processing", like the following example.

```json
{
    "id": 201917,
    "state": "Waiting",
    "isExpired": false
}
```

If the export has completed, the `state` property will be "Complete" and contain URLs to download the CSV files.

```json
{
    "id": 201917,
    "state": "Complete",
    "isExpired": false,
    "resultRefs": [
        "https://www.pardot.com/api/export/version/3/do/downloadResults/id/201917/file/23191",
        "https://www.pardot.com/api/export/version/3/do/downloadResults/id/201917/file/20201",
        "https://www.pardot.com/api/export/version/3/do/downloadResults/id/201917/file/20102"
    ]
}
```

---

# Query

```
/api/export/version/3/do/query
```

Used by administrators to retrieve a list of exports and their status. A user must have the “Admin > Exports > View” ability in order to execute this endpoint.

## GET

### Params

* **created_after**: (Optional) Filters the results to return only exports that were created after the specified time.
* **created_before**: (Optional) Filters the results to return only exports that were created before the specified time.
* **updated_after**: (Optional) Filters the results to return only exports that were updated after the specified time.
* **updated_before**: (Optional) Filters the results to return only exports that were updated before the specified time.
* **status**: (Optional) Filters the results to return exports in the given state. Allowed values are "Complete", "Failed", "Processing", or "Waiting".
* **object**: (Optional) Filters the results to return exports for the specified object.
* **sort_by**: (Optional) Sorts the results by the specified property value. Allowed values are "id", "created_at", or "updated_at". If not specified, the results are returned by "id" in "descending" order.
* **sort_order**: (Optional) Used in conjuntion with **sort_by** and adjusts the direction of the sort. Allowed values are "ascending" or "descending". If not specified, the results are in "descending" order.

### Success

* Status Code: 200

Output Representation

* **result**: A collection of exports
    * **total_results**: The total number of results matching the filter.
    * **export**: A collection of exports. If there are not results, this property is omitted. If there is a single result, this is an object. If there are multiple results, this is an array of results.
        * **id**: The ID of the export. This ID will be used to check the status of the export.
        * **state**: The state of the export. This will display "Waiting" when the export has been queued for processing, "Processing" when the server is working on the export and "Complete" when the export has completed. See [Export State](#export-state) enum.
        * **isExpired**: Indicates that the export has expired. After an export has expired, this will return `false` and no data associated to the export can be downloaded.
        * **createdAt**: The date and time the export was created in the timezone of the user making the request.
        * **updatedAt**: The date and time the export was updated in the timezone of the user making the request.

Note that the export representation returned in query will not contain a **resultRefs** property. Use the read endpoint for the export to get the full export representation.

```json
{
    "result": {
        "total_results": int,
        "export": [
            {
                "id": int,
                "state": string,
                "isExpired": boolean,
                "resultsRef": string OR string[],
                "createdAt": datetime,
                "updatedAt": datetime
            }
        ]
    }
}
```

### Errors

* Status Code: 4xx
* Error codes: See [Error Codes](/kb/error-codes-messages)

---

# Download Results

The URLs retrieved from the Read endpoint can be used to download the results of the export. A failure will occur when attempting to download any results from an expired export. See [Expiration](#expiration) for more information.

## GET

### Success

The data represented in CSV format. See the [CSV Format](#csv-file-formatting) section for more information.

### Errors

* Status code: 4xx
* Error codes: See [Error Codes](/kb/error-codes-messages)

---

# Enums

## Export State

* "Waiting": The export is waiting to be processed.
* "Processing": A server has started processing the export.
* "Complete": The export is complete and the results are ready to be downloaded.
* "Failed": A fatal error has occurred and cannot the data cannot be retrieved. Try executing the export again. If the error occurs again, contact your support representative.
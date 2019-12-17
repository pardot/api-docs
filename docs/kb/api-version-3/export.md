# Export API Overview

The Export API provides a way to retrieve large volumes of data from Pardot. It uses Pardot's existing API structures, patterns, and terminology.

# When to Use the Export API

Use the Export API to retrieve large sets of data when you don't need synchronous completion responses or when query limitations are too restrictive. Currently, only visitor activity is supported.

# How the Export API Works

An export is associated with a query and a data set in Pardot. When you create an export, the query is split into smaller queries, which return smaller sets of data. These smaller queries are processed in parallel, and the retrieved data is saved in CSV files. When the export is complete, the CSV files are available to download.

The order of the records returned in the CSV files is not guaranteed. The number of records in each CSV file varies, and all of the files associated with an export make up the full data set for the query.

The Export resource is used to create an export and get the status of an export. When the export is complete, the links to the CSV files containing the data are available in the resource.

# Limitations

* The Export API is subject to the daily Pardot API call limit and the concurrent Pardot API call limit for your account.
* Export API calls are executed sequentially for each account, with older exports being processed before newer exports.

# Expiration

The data associated with an export expires after 7 days. When data expires, the Export resource removes links to the CSV files and shows that the export has expired. Attempts to retrieve the data after an export expires fail.

# CSV File Formatting

* The first row contains the name of the field.
* The second row and beyond contain the record data.
* Dates are returned in the user’s timezone at the time they created the export.
    * For example, if a user is in “PST” timezone and creates an export, the dates in the export are in “PST”. If a second user is in “EST” timezone and downloads the exported files, the dates in the export are in “PST”.
    * If a user’s timezone changes, previous exports created by the user have dates formatted in the previous timezone. Dates in new exports use the new timezone.
* Dates are returned in the standard Pardot API date format of `YYYY-MM-DD HH:mm:SS`.
* Fields with null values are represented as an empty value in CSV.

# Procedures

A procedure is a query and execution plan used to retrieve the data. Each object has a different set of procedures.

## Visitor Activity

## filter_by_created_at

Retrieves all visitor activity records with a `created_at` value that is equal or greater than the `created_after` argument and less than or equal to the `created_before` argument.

**Abilities**

| Action           | Requirements  |
| ---------------- | ------------- |
| Create export    | Prospects > Visitors > View ability |
| View export      | Prospects > Visitors > View ability and be the same user that created the export |
| View all exports | Admin > Exports > View ability |
| Query exports    | Admin > Exports > View ability |


To create an export with this procedure, the user must have the following:

* “Prospects > Visitors > View“ ability

To view an export with this procedure, the user must have the following:

* “Prospects > Visitors > View“ ability AND
* The user must be the same as the user that created the export

OR

* “Admin > Exports > View”

**Arguments**

* **created_after**: Selects visitor activities that were created after the specified time. The value can be `today`, `yesterday`, `last_7_days`, `this_month`, `last_month`, or a custom time specified in [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) format.
* **created_before**: (Optional) Selects visitor activities that were created before the specified time. This value must be after the value in `created_after`. If this argument is not specified, then no upper boundary is used in the query, and all data after the `created_after` is returned. The value can be `today`, `yesterday`, `last_7_days`, `this_month`, `last_month`, or a custom time specified in [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) format.

__NOTE:__ The span between created_after and created_before cannot exceed 1 year. This is valid even when created_before is not specified, in which case the current date is used to measure the requested interval.

# Using the Export API

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

* **object**: Specifies which object to export. Currently only "visitorActivity" is supported.
* **procedure**: The procedure to execute. A procedure is a query and execution plan used to retrieve data. Each object has a different set of procedures. See the [Procedures](#procedures) section for available procedures.
    * **name**: The name of the procedure.
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

Status Code: 200

Output Representation

* **id**: The ID of the export. ID is used to check the status of the export.
* **state**: The state of the export. Displays "Waiting" when the export has been queued for processing, "Processing" when the server is working on the export and "Complete" when the export has completed. See [Export State](#export-state) enum.
* **isExpired**: Indicates that the export has expired. When an export has expired, this will return `true` and no data associated to the export can be downloaded.
* **resultsRef**: (Optional) This property appears when an export is complete, and it contains a list of URLS to CSV files available for download. If there is no data associated with the export, this property is absent. If there is only a single CSV file available for download, this property is a string containing the URL to download the file. If there are multiple CSV files, resultRef is an array of URLs.
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

This is a request to execute the visitor activity procedure named `filter_by_created_at`, which retrieves all visitor activity data where the `created_at` value is between two dates. In this example, the data will be retrieved from December 25, 2019 to December 25, 2020.

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

Used to retrieve the status of the export. Once an export is complete, the links to download the results are available in the result body.

## GET

### Params

**{id}**: The ID of the export.

### Success

Status Code: 200

Output Representation

* **id**: The ID of the export. This ID is used to check the status of the export.
* **state**: The state of the export. Displays "Waiting" when the export has been queued for processing, "Processing" when the server is working on the export and "Complete" when the export is completed. See [Export State](#export-state) enum.
* **isExpired**: Indicates that the export has expired. After an export has expired, this will return true and no data associated with the export can be downloaded.
* **resultsRef**: (Optional) This property appears only when the export has completed and contains a list of URLS to CSV files available for download. If there is no data associated with the export, this property is absent. If there is only a single CSV file available for download, resultsRef is a string containing the URL to download the file. If there are multiple CSV files, resultsRef is an array of URLs. The order of the URLs in the array is not significant.
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

After calling the Create endpoint, the ID of the export will be given in the response. This ID is used in the URL to call the Read endpoint.

```
GET /api/export/version/3/do/read/id/201917
HOST: pi.pardot.com
Content-Type: application/json
Authorization: Pardot user_key=U,api_key=A
```

If the export is waiting to be processed, `state` is "Waiting", like the following example.

```json
{
    "id": 201917,
    "state": "Waiting",
    "isExpired": false
}
```

If the export is finished, `state` is "Complete" and `resultRefs` contains URLs to download the CSV files.

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

Used by administrators to retrieve a list of exports and their status. A user must have the “Admin > Exports > View” ability to execute this endpoint.

## GET

### Params

* **created_after**: (Optional) Filters the results to return only exports that were created after the specified time.
* **created_before**: (Optional) Filters the results to return only exports that were created before the specified time.
* **updated_after**: (Optional) Filters the results to return only exports that were updated after the specified time.
* **updated_before**: (Optional) Filters the results to return only exports that were updated before the specified time.
* **status**: (Optional) Filters the results to return exports in the given state. Allowed values are "Complete", "Failed", "Processing", or "Waiting".
* **object**: (Optional) Filters the results to return exports for the specified object.
* **sort_by**: (Optional) Sorts the results by the specified property value. Allowed values are "id", "created_at", or "updated_at". If not specified, the results are returned by "id" in "descending" order.
* **sort_order**: (Optional) Used with `sort_by`. Adjusts the direction of the sort using the values "ascending" or "descending". If not specified, the results are in "descending" order.

### Success

Status Code: 200

Output Representation

* **result**: A collection of exports
    * **total_results**: The total number of results matching the filter.
    * **export**: A collection of exports. If there are no results, this property is omitted. If there is a single result, this is an object. If there are multiple results, this is an array of results.
        * **id**: The ID of the export. This ID is used to check the status of the export.
        * **state**: The state of the export. Displays "Waiting" when the export has been queued for processing, "Processing" when the server is working on the export and "Complete" when the export has completed. See [Export State](#export-state) enum.
        * **isExpired**: Indicates that the export has expired. After an export has expired, this will return `true` and no data associated with the export can be downloaded.
        * **createdAt**: The date and time the export was created in the timezone of the user making the request.
        * **updatedAt**: The date and time the export was updated in the timezone of the user making the request.

Note that the export representation returned in query doesn’t contain `resultRefs`. Use the read endpoint for the export to get the full export representation.

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

The URLs retrieved from the Read endpoint can be used to download the results of the export. A failure occurs when attempting to download any results from an expired export. See [Expiration](#expiration) for more information.

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
* "Complete": The export is complete and the results are available for download.
* "Failed": A fatal error has occurred and the data can’t be retrieved. Try executing the export again. If the error occurs again, contact support.

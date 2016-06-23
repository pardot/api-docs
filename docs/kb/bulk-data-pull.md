# Bulk Data Pull via the Pardot API

This document outlines the approach and best practices around pulling a large amount of data out of Pardot via the API, typically for ingestion into a third-party system or internal data warehouse.

Pulling data from Pardot is a straightforward, two-step process. First, log in with your Pardot user email, password, and user key to acquire an API key. Then, use the query endpoint for each data set to pull the data.

## Query the Pardot API

Before getting started, review the documentation at http://developer.pardot.com and determine which data set you are going to pull. For a data set to be eligible for a bulk data pull, it must have a query operation that supports at least one of the following three sets of search filter criteria parameters:

* `created_before` and `created_after`
* `updated_before` and `updated_after`
* `id_greater_than` and `id_less_than`

Issue an HTTP GET to the appropriate query endpoint to pull the data back. Include your `user_key` and `api_key` as URL parameters. The query response will contain up to 200 rows from the data set you have requested.

### Best Practice #1 ‐ Use the Bulk Output Format

For bulk data pulls, we strongly recommended that you use the `bulk` output format, which is highly optimized for performance. The `bulk` output format disables functionality which displays additional data in the API response such as nested object relationships (e.g. campaign name for activities, etc.). Additionally, the bulk output format omits information about the total number of rows that matched your query, which enables the API to return a response more quickly.

### Best Practice #2 ‐ Avoid Offset

For bulk data pulls, we strongly discourage use of the `offset` parameter. Instead, iterate through the data set using one of the supported search filter criteria parameters.

To accomplish this, as you process the query results in your code, store a high water mark value - the largest `id` or most recent `created_at` or `updated_at` value. Then, on your next query, send that high water mark value as the `id_greater_than`, `created_after`, or `updated_after` search filter parameter value.

### Bulk API Request & Response Samples

Example Request & Response (XML)

```bash
curl https://pi.pardot.com/api/visitorActivity/version/3/do/query?user_key=1234567890abcdef1234567890abcdef&api_key=fedcba0987654321fedcba0987654321&output=bulk
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<rsp stat="ok" version="1.0">
	<result>
		<visitor_activity>
			<id>23807</id>
			<visitor_id>14692</visitor_id>
			<prospect_id>621</prospect_id>
			<type>1</type>
			<type_name>Email Tracker</type_name> <details>http://www.pardot.com/products/demos/flash-demo.html</details> <email_id>764</email_id>
			<campaign_id>1</campaign_id>
			<created_at>2007-08-09 19:29:07</created_at>
			</visitor_activity> <visitor_activity>
			<id>23815</id>
			<visitor_id>14692</visitor_id>
			<prospect_id>621</prospect_id>
			<type>1</type>
			<type_name>Email Tracker</type_name> <details>http://www.pardot.com/products/demos/flash-demo.html</details> <email_id>764</email_id>
			<campaign_id>1</campaign_id>
			<created_at>2007-08-09 20:13:40</created_at>
		</visitor_activity>
	</result>
</rsp>
```

Example Request & Response (JSON)

```bash
curl https://pi.pardot.com/api/visitorActivity/version/3/do/query?user_key=1234567890abcdef1234567890abcdef&api_key=fedcba0987654321fedcba0987654321&output=bulk&format=json
```

```json
{
	"@attributes": {
		"stat": "ok",
		"version": 1
	},
	"result": {
		"visitor_activity": [
		{
			"id": 23807,
			"visitor_id": 14692,
			"prospect_id": 621,
			"type": 1,
			"type_name": "Email Tracker",
			"details": "http:\/\/www.pardot.com\/products\/demos\/flash-demo.html", "email_id": 764,
			"campaign_id": 1,
			"created_at": "2007-08-09 19:29:07"
		}, {
			"id": 23815,
			"visitor_id": 14692,
			"prospect_id": 621,
			"type": 1,
			"type_name": "Email Tracker",
			"details": "http:\/\/www.pardot.com\/products\/demos\/flash-demo.html", "email_id": 764,
			"campaign_id": 1,
			"created_at": "2007-08-09 20:13:40"
		}]
	}
}
```

## Example of Paging through a Large Set of Results

Because using the offset parameter is strongly discouraged, let’s see how you can use a high water mark value to iterate through multiple pages of results instead. In this example, you will query for all visitor activities that occurred yesterday. This is a perfect match for the `created_after` and `created_before` search filter criteria parameters.

To keep things simple, assume there were a total of 5 activities created yesterday (at time of writing, 2016-03-29) at times 02:00, 06:00, 10:00, 14:00, and 18:00. Also assume the API page size limit is 2 rather than 200.

To iterate over the results in the suggested approach, your API integration process would proceed as follows:
1. Log in to the Pardot API
2. Pull all visitor activity created after yesterday at midnight (`2016-03-29T00:00:00`) and before tonight at midnight (`2016-03-30T00:00:00`):

Example Request & Response (JSON)

```bash
curl https://pi.pardot.com/api/visitorActivity/version/3/do/query?user_key=X&api_key=Y&output=bulk&format=json&created_after=2016-03-29T00:00:00&created_before=2016-03-30T00:00:00&sort_by=created_at&sort_order=ascending
```

```json
{
	"@attributes": {
		"stat": "ok",
		"version": 1
	},
	"result": {
		"visitor_activity": [
		{
			"id": 23807,
			"created_at": "2016-03-29 02:00:00"
		}, {
			"id": 24531,
			"created_at": "2016-03-29 06:00:00"
		}]
	}
}
```
*Note*: the above example was edited for brevity

3. The API has returned two results - the activities from 02:00 and 06:00. Since you are paging by `created_at`, set your high water mark value to the `created_at` value of the last record you pull back, `2016-03-30T06:00:00`. You have now retrieved all activities up to that time.
4. Pull all visitor activity created after your high water mark (`2016-03-29T06:00:00`) and before tonight at midnight (`2016-03-30T00:00:00`):

Example Request & Response (JSON)

```bash
curl https://pi.pardot.com/api/visitorActivity/version/3/do/query?user_key=X&api_key=Y&output=bulk&format=json&created_after=2016-03-29T06:00:00&created_before=2016-03-30T00:00:00&sort_by=created_at&sort_order=ascending
```

```json
{
    "@attributes": {
    	"stat": "ok",
    	"version": 1
	},
	"result": {
		"visitor_activity": [
		{
			"id": 27093,
			"created_at": "2016-03-29 10:00:00"
		},
		{
			"id": 27588,
			"created_at": "2016-03-29 14:00:00"
		}]
	}
}
```
*Note*: the above example was edited for brevity


5. The API returns two more results back - the activities from 10:00 and 14:00. Since you are paging by `created_at`, update your high water mark value to the `created_at` value of the last record you pull back, `2016-03-29T14:00:00`. You have now retrieved all activities up to that time.
6. Pull all visitor activity created after your high water mark (`2016-03-29T14:00:00`) and before tonight at midnight (`2016-03-30T00:00:00`):

Example Request & Response (JSON)

```bash
curl https://pi.pardot.com/api/visitorActivity/version/3/do/query?user_key=X&api_key=Y&output=bulk&format=json&created_after=2016-03-29T14:00:00&created_before=2016-03-30T00:00:00&sort_by=created_at&sort_order=ascending
```

```json
{
	"@attributes": {
		"stat": "ok",
		"version": 1
	},
	"result": {
		"visitor_activity": [
		{
			"id": 30017,
			"created_at": "2016-03-29 18:00:00"
		}]
	}
}
```
*Note*: the above example was edited for brevity

7. The API returns one result back, the activity from 18:00. As the max page size is 2 and the API returned one record, you know you are at the end of the list of records and do not need to query any further. If the API had returned 2 records you would repeat the query process again with a new high water mark. You know it’s safe to stop when the number of records returned by the API is less than the max page size.

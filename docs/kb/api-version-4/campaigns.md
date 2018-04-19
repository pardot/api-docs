# Querying Campaigns


## Supported Operations<a name="62781-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/campaign/version/4/do/query?...` | `user_key, api_key` | Returns the campaigns matching the specified criteria parameters. See the [Using Campaigns](#using-campaigns) section for a complete description of the campaign [XML Response Format](#xml-response-format). Also see [Campaign](../object-field-references#campaign) in [Object Field References](../object-field-references) |

<a name="62781-supported-search-criteria" id="supported-search-criteria"></a>

## Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 campaigns will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.


| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for campaigns that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for campaigns that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `id_greater_than` | `integer` | `<any_positive_integer>` | Searches for campaigns with IDs greater than the specified integer |
| `id_less_than` | `integer` | `<any_positive_integer>` | Searches for campaigns with IDs less than the specified integer |
| `name` | `string` | `<any string>` | Searches for campaigns a name exactly matching the given name |
| `updated_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for campaigns that were updated before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `updated_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for campaigns that were updated after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |


## Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the campaigns matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. If a number larger than 200 is specified, 200 will be used |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching campaign (according to the specified sorting order) to be returned in the `query` response. The first `offset` matching campaigns will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th campaign matched by the provided criteria |
| `sort_by` | `string` | `created_at, id` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supported Sorting Options](#supported-sorting-options) for more details |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in campaign queries, see Campaign in Object Field References.

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the campaigns' `created_at` timestamps |
| `id` | `ascending` | Specifies that the query results should be sorted by the campaigns' `id` fields |
| `name` | `ascending` | Specifies that the query results should be sorted by the campaigns' `name` fields |
| `updated_at` | `descending` | Specifies that the query results should be sorted by the campaigns' `updated_at` timestamps |
| `cost` | `descending` | Specifies that the query results should be sorted by the campaigns' `cost` fields |



## XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <campaign>...</campaign>
        <campaign>...</campaign>
        <campaign>...</campaign>
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting campaigns for the specified query |
| `<total_results>` | Contains the number of campaigns selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched campaigns |
| `<campaign>` | The data for an individual campaign. See [Using Campaigns](#using-campaigns) for a complete description of the campaign [XML Response Format](#xml-response-format). Also see [Campaign](../object-field-references#campaign) in [Object Field References](../object-field-references) |

# Using Campaigns


## Supported Operations<a name="62780-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [Campaign](../object-field-references#campaign) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/campaign/version/4/do/read/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the campaign specified by `<id>`. `<id>` is the Pardot ID of the target campaign. |
| `read` | `/api/campaign/version/4/do/read/fid/`**_`<fid>`_**`?...` | `user_key, api_key, fid` | Returns the data for the campaign specified by `<fid>`. `<fid>` is the Salesforce ID of the target campaign. |
| `update` | `/api/campaign/version/4/do/update/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Updates the provided data for the campaign specified by `<id>`.  `<id>` is the Pardot ID of the campaign. Refer to [Campaign](../object-field-references#campaign) in [Object Field References](../object-field-references) for more details. Returns the updated version of the campaign. **_Note:_** If the Campaign Alignment feature is enabled, `name` and `cost` are not updateable. |
| `create` | `/api/campaign/version/4/do/create?...` | `user_key, api_key` | Creates a new campaign using the specified data. **_Note:_** If the Campaign Alignment feature is enabled, the `create` operation is not allowed.|


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <campaign>
        <id>2</id>
        <name>"Web Tracking"</name>
        <cost>100</cost>
    </campaign>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<campaign>` | Parent tag. Contains data fields for target campaign. For complete field listing, see [Campaign](../object-field-references#campaign) in [Object Field References](../object-field-references). |

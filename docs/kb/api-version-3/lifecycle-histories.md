# Querying Lifecycle Histories


## Supported Operations<a name="62781-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/lifecycleHistory/version/3/do/query?...` | `user_key, api_key` | Returns the lifecycle history matching the specified criteria parameters. See the [Using Lifecycle Histories](#using-lifecycle-histories) section for a complete description of the lifecycle history [XML Response Format](#xml-response-format). Also see [Lifecycle History](object-field-references#lifecycle-history) in [Object Field References](object-field-references) |

<a name="62781-supported-search-criteria" id="supported-search-criteria"></a>

## Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 lifecycle histories will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.


| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for lifecycle histories that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for lifecycle histories that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `id_greater_than` | `integer` | `<any_positive_integer>` | Searches for lifecycle histories with IDs greater than the specified integer |
| `id_less_than` | `integer` | `<any_positive_integer>` | Searches for lifecycle histories with IDs less than the specified integer |


## Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the lifecycle histories matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. If a number larger than 200 is specified, 200 will be used |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching lifecycle history (according to the specified sorting order) to be returned in the `query` response. The first `offset` matching lifecycle history will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th lifecycle history matched by the provided criteria |
| `sort_by` | `string` | `created_at, id` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supporting Sorting Options](#supported-sorting-options) for more details |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in lifecycle history queries, see Lifecycle History in Object Field References.

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `ascending` | Specifies that the query results should be sorted by the Lifecycle Histories' `created_at` timestamps |
| `id` | `ascending` | Specifies that the query results should be sorted by the Lifecycle Histories' `id` fields |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <lifecycleHistory>...</lifecycleHistory>
        <lifecycleHistory>...</lifecycleHistory>
        <lifecycleHistory>...</lifecycleHistory>
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting lifecycle histories for the specified query |
| `<total_results>` | Contains the number of lifecycle histories selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched lifecycle histories |
| `<lifecycleHistory>` | The data for an individual lifecycle history. See [Using Lifecycle Histories](#using-lifecycle-histories) for a complete description of the lifecycle history [XML Response Format](#xml-response-format). Also see [Lifecycle History](object-field-references#lifecycle-history) in [Object Field References](object-field-references) |


# Using Lifecycle Histories


## Supported Operations<a name="62780-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [Lifecycle History](object-field-references#lifecycle-history) section of [Object Field References](object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/lifecycleHistory/version/3/do/read/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the lifecycle history specified by `<id>`. `<id>` is the Pardot ID of the target lifecycle history. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <lifecycleHistory>
        <id>455069</id>
        <prospect_id>66345</prospect_id>
        <previous_stage_id/>
        <next_stage_id>912</next_stage_id>
        <seconds_elapsed/>
        <created_at>2014-02-28 14:20:47</created_at>
    </lifecycleHistory>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<lifecycleHistory>` | Parent tag. Contains data fields for target lifecycle history. For complete field listing, see [Lifecycle History](object-field-references#lifecycle-history) in [Object Field References](object-field-references). |

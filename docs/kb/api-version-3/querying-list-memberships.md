# Querying List Memberships


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="87486-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/listMembership/version/3/do/query?...` | `user_key, api_key` | Returns the list memberships matching the specified criteria parameters. See the [Using Lists](../using-lists) section for a complete description of the list membership [XML Response Format](../using-list-memberships#xml-response-format). Also see [List Membership](../object-field-references#list-membership) in [Object Field References](../object-field-references). |


## [](#supported-search-criteria-)Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 list memberships will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.


| Parameter              | Datatype         | Options                                                                | Description |
|------------------------|------------------|------------------------------------------------------------------------|-------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for list memberships that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for list memberships that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `deleted` | `string` | `true, false` | Searches for list memberships based on whether they have been deleted. _Default value:_ `false`. |
| `id_greater_than` | `integer` | `<any_positive_integer>` | Searches for list memberships with IDs greater than the specified integer. |
| `id_less_than` | `integer` | `<any_positive_integer>` | Searches for list memberships with IDs less than the specified integer. |
| `list_id` | `integer` | `<any_list_id>` | Searches for list memberships that have this `<list_id>`. `<list_id>` is the Pardot list ID. |
| `updated_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for list memberships that were updated before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `updated_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for list memberships that were updated after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |

## [](#manipulating-the-result-set-)Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the list memberships matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| Parameter              | Datatype         | Options                                                                | Description |
|------------------------|------------------|------------------------------------------------------------------------|-------------|
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. If a number larger than 200 is specified, 200 will be used. |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching list membership(according to the specified sorting order) to be returned in the `query` response. The first `offset` matching list memberships will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th list membership matched by the provided criteria. |
| `sort_by` | `string` | `created_at, id` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. _Default value:_ `id`. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supporting Sorting Options](#supported-sorting-options) for more details. |


## [](#supported-sorting-options-)Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list membership of fields involved in list membership queries, see List membership in Object Field References.

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the list memberships' `created_at` timestamps. |
| `id` | `ascending` | Specifies that the query results should be sorted by the list memberships' `id` fields. |


## [](#xml-response-format-)XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <list_membership>...</list_membership>
        <list_membership>...</list_membership>
        <list_membership>...</list_membership>
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting list memberships for the specified query. |
| `<total_results>` | Contains the number of list memberships selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched list memberships. |
| `<list_membership>` | The data for an individual list membership. See [Using List Memberships](../using-list-memberships) for a complete description of the list membership [XML Response Format](../using-list-memberships#xml-response-format). Also see [List Membership](../object-field-references#list-membership) in [Object Field References](../object-field-references). |


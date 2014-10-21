
# Querying Prospect Accounts


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="70887-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/prospectAccount/version/3/do/query?...` | `user_key, api_key` | Returns the prospect accounts matching the specified criteria parameters. See the [Using Prospect Accounts](../using-prospect-accounts) section for a complete description of the prospect account [XML Response Format](../using-prospect-accounts#xml-response-format). Also see [Prospect Account](../object-field-references#prospectAccount) in [Object Field References](../object-field-references). |

## [](#supported-search-criteria-)Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 prospect accounts will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for prospect accounts that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for prospect accounts that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `id_greater_than` | `integer` | `<any_positive_integer>` | Searches for prospect accounts with IDs greater than the specified integer. |
| `id_less_than` | `integer` | `<any_positive_integer>` | Searches for prospect accounts with IDs less than the specified integer. |
| `name` | `string` | `<any string>` | Searches for prospect accounts a name exactly matching the given name. |
| `updated_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for prospect accounts that were updated before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `updated_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for prospect accounts that were updated after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |

## [](#manipulating-the-result-set-)Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the prospect accounts matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `fields` | `array` | `<comma_separated_field_ids>` | Specifies the fields to be returned. **Note:** All default and custom fields will be returned by default; &lt;id&gt; will always be returned. |
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. If a number larger than 200 is specified, 200 will be used. |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching prospect account (according to the specified sorting order) to be returned in the `query` response. The first `offset` matching prospect accounts will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th prospect account matched by the provided criteria. |
| `sort_by` | `string` | `created_at, id, name, updated_at` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. _Default value:_ `id`. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supporting Sorting Options](#supported-sorting-options) for more details. |

## [](#supported-sorting-options-)Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in prospect account queries, see Prospect Account in Object Field References.


| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the prospect accounts' `created_at` timestamps. |
| `id` | `ascending` | Specifies that the query results should be sorted by the prospect accounts' `id` fields. |
| `name` | `ascending` | Specifies that the query results should be sorted by the prospect accounts' `updated_at` names. |
| `updated_at` | `ascending` | Specifies that the query results should be sorted by the prospect accounts' `updated_at` timestamps. |


## [](#xml-response-format-)XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <prospectAccount>...</prospectAccount>
        <prospectAccount>...</prospectAccount>
        <prospectAccount>...</prospectAccount>
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting prospect accounts for the specified query. |
| `<total_results>` | Contains the number of prospect accounts selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched prospect accounts. |
| `<prospectAccount>` | The data for an individual prospect account. See [Using Prospect Accounts](../using-prospect-accounts) for a complete description of the prospect account [XML Response Format](../using-prospect-accounts#xml-response-format). Also see [Prospect Account](../object-field-references#prospectAccount) in [Object Field References](../object-field-references). |

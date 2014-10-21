# Querying Opportunities


## Supported Operations<a name="14770-supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/opportunity/version/3/do/query?...` | `user_key, api_key` | Returns the opportunities matching the specified criteria parameters. See [Using Opportunities (using-opportunities) for complete descriptions of opportunity [XML Response Formats](../using-opportunities#xml-response-formats). Also see [Opportunity](../object-field references#opportunity) in [Object Field References](../object-field-references). |

## Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 opportunities will be returned with each query request. This limit is not enforced for responses formatted with `output=mobile`.


| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month,<custom_time>` | Selects opportunities that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input formats.html). |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Selects opportunities that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `id_greater_than` | `integer` | Selects opportunities with IDs greater than the specified integer. |
| `id_less_than` | `integer` | Selects opportunities with IDs less than the specified integer. |
| `probability_greater_than` | `integer` | Selects opportunities with probabilities greater than the specified number. |
| `probability_less_than` | `integer` | Selects opportunities with probabilities less than the specified number. |
| `prospect_email` | `string` | Selects opportunities associated with the specified prospect. `prospect_email` must correspond to an existing prospect. **_Note:_** If both `prospect_email` and `prospect_id` are specified, both must correspond to the same prospect. Otherwise, the API will return an error. |
| `prospect_id` | `integer` | Selects opportunities associated with the specified prospect. `prospect_id` must correspond to an existing prospect. **_Note:_** If both `prospect_email` and `prospect_id` are specified, both must correspond to the same prospect. Otherwise, the API will return an error. |
| `value_greater_than` | `integer` | Selects opportunities that have a value greater than a specified integer. |
| `value_less_than` | `integer` | Selects opportunities that have a value less than a specified integer. |


## Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the returned results may not include all opportunities that were matched by the query. The following criteria can be used to navigate through the result set and retrieve the remaining results.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `limit` | `integer` |  | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. |
| `offset` | `integer` |  | Specifies the first matching opportunity (according to the specified sorting order) to be returned in the query response. The first `offset` matching opportunities will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=400` will return the results starting with the 401st opportunity matched by the provided criteria. |
| `output` | `simple, mobile` |  | Specifies the format to be used when returning the results of the query. See [XML Response Formats](../using-opportunities#xml-response-formats) in [Using Opportunities](../using-opportunities) for more details. |
| `sort_by` | `string` | `created_at, id, probability, value` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options (#14770-supported-sorting-options) for more details. _Default value:_ `id`. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default sorting order varies based on the value of the `sort_by` parameter. See [Supported Sorting Options](#supported-sorting-options) for more details. |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in Opportunity queries, see [Opportunity](../object-field-references#opportunity) in [Object Field References](../object-field-references).


| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the opportunities' `created_at` timestamps. |
| `id` | `ascending` | Specifies that the query results should be sorted by the opportunities' `id` fields. |
| `probability` | `descending` | Specifies that the query results should be sorted by the opportunities' `probability` fields. |
| `value` | `descending` | Specifies that the query results should be sorted by the opportunities' `value` fields. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <opportunity>...</opportunity>
            ...
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting opportunities for the specified query. |
| `<total_results>` | Contains the number of opportunities selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all matched opportunities. |
| `<opportunity>` | The data for an individual Opportunity. See [Using Opportunities](../using-opportunities) for complete descriptions of opportunity [XML Response Formats](../using-opportunities#xml-response-formats). Also see [Opportunity](../object-field-references#opportunity) in [Object Field References](../object-field-references). **_Note:_** Data concerning an opportunity's activities will NOT be included in a `query` response. To retrieve this data, use a `read` request for individual opportunities of interest. |


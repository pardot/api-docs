# Querying Users


## Supported Operations<a name="14847-supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/user/version/4/do/query?...` | `user_key, api_key` | Returns the users matching the specified criteria parameters. See the [Using Users](users) section for a complete description of the user [XML Response Format](users#xml-response-format). Also see [User](../object-field-references.md#user) in [Object Field References](../object-field-references.md). |

## Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 users will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.

**Note:** Only users with Administrator privileges can issue `query` requests for other users. If users with lesser privileges issue a `query` request, only data about their own user will be returned.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after`  |  `string`  |  `today, yesterday, last_7_days, this_month, last_month, <custom_time>`  |  Selects users that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `created_before`  |  `string`  |  `today, yesterday, last_7_days, this_month, last_month, <custom_time>`  |  Selects users that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `id_greater_than`  |  `integer`  |  `<any_positive_integer>`  |  Selects users with IDs greater than the specified integer. |
| `id_less_than`  |  `integer`  |  `<any_positive_integer>`  |  Selects users with IDs less than the specified integer. |


## Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the users matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `limit`  |  `integer`  |  `<any_positive_integer>`  |  Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. |
| `offset`  |  `integer`  |  `<any_positive_integer>`  |  Specifies the first matching user (according to the specified sorting order) to be returned in the `query` response. The first `offset` matching users will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th user matched by the provided criteria. |
| `sort_by`  |  `string`  |  `created_at, id`  |  Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. |
| `sort_order`  |  `string`  |  `ascending, descending`  |  Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supporting Sorting Options](#supported-sorting-options) for more details. |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in user queries, see User in Object Field References.

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at`  |  `descending`  |  Specifies that the query results should be sorted by the users' `created_at` timestamps. |
| `id`  |  `ascending`  |  Specifies that the query results should be sorted by the users' `id` fields. |

## XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <user>...</user>
            ...
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>`  |  Contains the resulting users for the specified query. |
| `<total_results>`  |  Contains the number of users selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched users. |
| `<user>`  |  The data for an individual user. See [Using Users](users) for a complete description of the user [XML Response Format](users#xml-response-format). Also see [User](../object-field-references.md#user) in [Object Field References](../object-field-references.md). |

# Using Users


## Supported Operations<a name="14859-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [User](../object-field-references.md#user) section of [Object Field References](../object-field-references.md).

| **Operation** | **URL Format** | **Required Parameters** | **Description** |
| ------------- | -------------- | ----------------------- | --------------- |
| `read` | `/api/user/version/4/do/read/email/<email>?...` | `user_key, api_key, email` | Returns the data for the user specified by `<email>`. `<email>` is the email address of the target user. |
| `read` | `/api/user/version/4/do/read/id/<id>?...` | `user_key, api_key, id` | Returns the data for the user specified by `<id>`. `<id>` is the Pardot ID of the target user. |

## XML Response Format

```
<rsp stat="ok" version="1.0">
    <user>
        ...
    </user>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<user>` | Parent tag. Contains data fields for target user. For complete field listing, see [User](../object-field-references.md#user) in [Object Field References](object-field references). |


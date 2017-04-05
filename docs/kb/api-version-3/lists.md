# Querying Lists


## Supported Operations<a name="62781-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/list/version/3/do/query?...` | `user_key, api_key` | Returns the lists matching the specified criteria parameters. See the [Using Lists](#using-lists) section for a complete description of the list [XML Response Format](#xml-response-format). Also see [List](object-field-references#list) in [Object Field References](object-field-references) |

<a name="62781-supported-search-criteria" id="supported-search-criteria"></a>

## Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 lists will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.


| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for lists that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for lists that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `id_greater_than` | `integer` | `<any_positive_integer>` | Searches for lists with IDs greater than the specified integer |
| `id_less_than` | `integer` | `<any_positive_integer>` | Searches for lists with IDs less than the specified integer |
| `name` | `string` | `<any string>` | Searches for lists a name exactly matching the given name |
| `updated_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for lists that were updated before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `updated_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for lists that were updated after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |


## Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the lists matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. If a number larger than 200 is specified, 200 will be used |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching list (according to the specified sorting order) to be returned in the `query` response. The first `offset` matching lists will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th list matched by the provided criteria |
| `sort_by` | `string` | `created_at, id` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supported Sorting Options](#supported-sorting-options) for more details |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in list queries, see List in Object Field References.

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the lists' `created_at` timestamps |
| `id` | `ascending` | Specifies that the query results should be sorted by the lists' `id` fields |
| `name` | `ascending` | Specifies that the query results should be sorted by the lists' `name` fields |
| `updated_at` | `descending` | Specifies that the query results should be sorted by the lists' `updated_at` timestamps |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <list>...</list>
        <list>...</list>
        <list>...</list>
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting lists for the specified query |
| `<total_results>` | Contains the number of lists selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched lists |
| `<list>` | The data for an individual list. See [Using Lists](#using-lists) for a complete description of the list [XML Response Format](#xml-response-format). Also see [List](../object-field-references#list) in [Object Field References](../object-field-references) |

# Using Lists


## Supported Operations<a name="62780-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [List](../object-field-references#list) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/list/version/3/do/read/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the list specified by `<id>`. `<id>` is the Pardot ID of the target list. |
| `update` | `/api/list/version/3/do/update/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Updates the provided data for the list specified by `<id>`.  `<id>` is the Pardot ID of the list. Refer to [List](object-field-references#list) in [Object Field References](object-field-references) for more details. Returns the updated version of the list. |
| `create` | `/api/list/version/3/do/create?...` | `user_key, api_key` | Creates a new list using the specified data. |
| `delete` | `/api/list/version/3/do/delete/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Deletes the list specified by `<id>`. Returns HTTP 204 No Content on success. **_Note:_** Lists may only be deleted using HTTP methods POST or DELETE. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <list>
        <id>752</id>
        <name>Monthly Newsletter</name>
        <is_public>true</is_public>
        <is_dynamic>false</is_dynamic>
        <title>Newsletter</title>
        <description>For public lists, an optional description may be used to explain to the prospect why they might want to include this list in their subscription preferences.</description>
        <is_crm_visible>false</is_crm_visible>
        <created_at>2014-02-11 15:42:36</created_at>
        <updated_at>2014-03-06 15:28:41</updated_at>
    </list>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<list>` | Parent tag. Contains data fields for target list. For complete field listing, see [List](../object-field-references#list) in [Object Field References](../object-field-references). |

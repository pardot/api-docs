# Querying Custom Redirects


## Supported Operations<a name="62781-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/customRedirect/version/4/do/query?...` | `user_key, api_key` | Returns the custom redirects matching the specified criteria parameters. See the [Using Custom Redirects](#using-custom-redirects) section for a complete description of the custom redirect [XML Response Format](#xml-response-format). Also see [Custom Redirect](../object-field-references#custom-redirect) in [Object Field References](../object-field-references) |

<a name="62781-supported-search-criteria" id="supported-search-criteria"></a>

## Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 custom redirects will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.


| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for custom redirects that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for custom redirects that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `id_greater_than` | `integer` | `<any_positive_integer>` | Searches for custom redirects with IDs greater than the specified integer |
| `id_less_than` | `integer` | `<any_positive_integer>` | Searches for custom redirects with IDs less than the specified integer |
| `updated_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for custom redirects that were updated before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `updated_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for custom redirects that were updated after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |


## Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the custom redirects matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. If a number larger than 200 is specified, 200 will be used |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching custom redirects (according to the specified sorting order) to be returned in the `query` response. The first `offset` matching custom redirects will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th custom redirect matched by the provided criteria |
| `sort_by` | `string` | `created_at, id` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supporting Sorting Options](#supported-sorting-options) for more details |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in custom redirect queries, see Custom Redirect in Object Field References.

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the custom redirects' `created_at` timestamps |
| `id` | `ascending` | Specifies that the query results should be sorted by the custom redirects' `id` fields |
| `updated_at` | `descending` | Specifies that the query results should be sorted by the custom redirects' `updated_at` timestamps |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <customRedirect>...</customRedirect>
        <customRedirect>...</customRedirect>
        <customRedirect>...</customRedirect>
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting custom redirects for the specified query |
| `<total_results>` | Contains the number of custom redirects selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched custom redirects |
| `<customRedirect>` | The data for an individual custom redirect. See [Using Custom Redirects](#using-custom-redirects) for a complete description of the custom redirect [XML Response Format](#xml-response-format). Also see [Custom Redirect](../object-field-references#custom-redirect) in [Object Field References](../object-field-references) |

# Using Custom Redirects


## Supported Operations<a name="62780-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [Custom Redirect](../object-field-references#custom-redirect) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/customRedirect/version/4/do/read/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the custom redirect specified by `<id>`. `<id>` is the Pardot ID of the target custom redirect. |
| `create` | `/api/customRedirect/version/4/do/create?...` | `user_key, api_key, id` | Creates a new custom redirect using the specified data. |
| `update` | `/api/customRedirect/version/4/do/update/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Updates the provided data for the custom redirect specified by `<id>`.  `<id>` is the Pardot ID of the custom redirect. Refer to [Custom Redirect](../object-field-references#custom-redirect) in [Object Field References](../object-field-references) for more details. Returns the updated version of the custom redirect. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
  <customRedirect>
    <id>21</id>
    <name>Linkedin Home Page</name>
    <url>http://www2.pardot.com/l/1/2010-09-21/EMDL2</url>
    <destination_url>http://www.linkedin.com</destination_url>
    <campaign>
        <id>2</id>
        <name>LinkedIn</name>
    </campaign>
    <created_at>2010-09-21 18:47:42</created_at>
    <updated_at>2010-09-22 12:37:29</updated_at>
  </customRedirect>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<form>` | Parent tag. Contains data fields for target form. For complete field listing, see [Form](../object-field-references#form) in [Object Field References](../object-field-references). |
| `<campaign>` | Contains `<id>` and `<name>` of the campaign to which this custom redirect has been assigned. |

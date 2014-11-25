# Querying Forms


## Supported Operations<a name="62781-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/form/version/3/do/query?...` | `user_key, api_key` | Returns the forms matching the specified criteria parameters. See the [Using Forms](../using-forms) section for a complete description of the form [XML Response Format](../using-forms#xml-response-format). Also see [Form](../object-field-references#form) in [Object Field References](../object-field-references) |

<a name="62781-supported-search-criteria" id="supported-search-criteria"></a>

## Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 forms will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.


| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for forms that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for forms that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `id_greater_than` | `integer` | `<any_positive_integer>` | Searches for forms with IDs greater than the specified integer |
| `id_less_than` | `integer` | `<any_positive_integer>` | Searches for forms with IDs less than the specified integer |
| `updated_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for forms that were updated before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `updated_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for forms that were updated after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |


## Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the forms matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. If a number larger than 200 is specified, 200 will be used |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching forms (according to the specified sorting order) to be returned in the `query` response. The first `offset` matching forms will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th form matched by the provided criteria |
| `sort_by` | `string` | `created_at, id` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. _Default value:_ `id` |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supporting Sorting Options](#supported-sorting-options) for more details |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in form queries, see Form in Object Field References.

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the forms' `created_at` timestamps |
| `id` | `ascending` | Specifies that the query results should be sorted by the forms' `id` fields |
| `updated_at` | `ascending` | Specifies that the query results should be sorted by the forms' `updated_at` timestamps |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <form>...</form>
        <form>...</form>
        <form>...</form>
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting forms for the specified query |
| `<total_results>` | Contains the number of forms selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched forms |
| `<form>` | The data for an individual form. See [Using Forms](../using-forms) for a complete description of the form [XML Response Format](../using-forms#xml-response-format). Also see [Form](../object-field-references#form) in [Object Field References](../object-field-references) |

# Using Forms


## Supported Operations<a name="62780-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [Form](../object-field-references#form) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/form/version/3/do/read/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the form specified by `<id>`. `<id>` is the Pardot ID of the target list. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <form>
        <id>1</id>
        <name>Standard Form</name>
        <campaign>
            <id>1</id>
            <name>Website Tracking</name>
        </campaign>
        <embedCode>
            <iframe src="http://www2.pardot.com/l/1/8j56gt" width="100%" height="500" type="text/html" frameborder="0" allowTransparency="true" style="border: 0"></iframe>
        </embedCode>
        <created_at>2007-06-12 18:14:50</created_at>
        <updated_at>2013-11-06 14:34:34</updated_at>
    </form>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<form>` | Parent tag. Contains data fields for target form. For complete field listing, see [Form](../object-field-references#form) in [Object Field References](../object-field-references). |
| `<campaign>` | Contains `<id>` and `<name>` of the campaign to which this form has been assigned. |
| `<embedCode>` | Contains `<iframe>` of the form which you can use to embed the form on your webpage. |
# Querying Custom Fields


## Supported Operations<a name="62781-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/customField/version/3/do/query?...` | `user_key, api_key` | Returns the custom fields matching the specified criteria parameters. See the [Using Custom Fields](#using-custom-fields) section for a complete description of the custom field [XML Response Format](#xml-response-format). Also see [Custom Field](object-field-references#custom-field) in [Object Field References](object-field-references) |

<a name="62781-supported-search-criteria" id="supported-search-criteria"></a>

## Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 custom fields will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.


| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for custom fields that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for custom fields that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `id_greater_than` | `integer` | `<any_positive_integer>` | Searches for custom fields with IDs greater than the specified integer |
| `id_less_than` | `integer` | `<any_positive_integer>` | Searches for custom fields with IDs less than the specified integer |


## Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the custom fields matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. If a number larger than 200 is specified, 200 will be used |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching custom field (according to the specified sorting order) to be returned in the `query` response. The first `offset` matching custom fields will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th custom field matched by the provided criteria |
| `sort_by` | `string` | `created_at, id` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supported Sorting Options](#supported-sorting-options) for more details |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in custom field queries, see Custom Field in Object Field References.

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the custom fields' `created_at` timestamps |
| `id` | `ascending` | Specifies that the query results should be sorted by the custom fields' `id` fields |
| `name` | `ascending` | Specifies that the query results should be sorted by the custom fields' `name` fields |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <customField>...</customField>
        <customField>...</customField>
        <customField>...</customField>
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting custom fields for the specified query |
| `<total_results>` | Contains the number of custom fields selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched custom fields |
| `<customField>` | The data for an individual custom field. See [Using Custom Fields](#using-custom-fields) for a complete description of the custom field [XML Response Format](#xml-response-format). Also see [Custom Field](object-field-references#custom-field) in [Object Field References](object-field-references) |

# Using Custom Fields


## Supported Operations<a name="62780-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [Custom Field](object-field-references#custom-field) section of [Object Field References](object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/customField/version/3/do/read/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the custom field specified by `<id>`. `<id>` is the Pardot ID of the target custom field. |
| `update` | `/api/customField/version/3/do/update/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Updates the provided data for the custom field specified by `<id>`.  `<id>` is the Pardot ID of the custom field. Refer to [Custom Field](object-field-references#custom-field) in [Object Field References](object-field-references) for more details. Returns the updated version of the custom field. |
| `create` | `/api/customField/version/3/do/create?...` | `user_key, api_key` | Creates a new custom field using the specified data. |
| `delete` | `/api/customField/version/3/do/delete/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Deletes the custom field specified by `<id>`. Returns HTTP 204 No Content on success. **_Note:_** Custom Fields may only be deleted using HTTP methods POST or DELETE. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <customField>
        <id>1070</id>
        <name>Checkbox Field</name>
        <field_id>Checkbox_Field</field_id>
        <type>Checkbox</type>
        <type_id>3</type_id>
        <crm_id>Alt_Email__c</crm_id>
        <is_record_multiple_responses>true</is_record_multiple_responses>
        <is_use_values>false</is_use_values>
        <created_at>2014-09-19 11:43:36</created_at>
        <updated_at>2014-11-19 05:04:17</updated_at>
    </customField>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<customField>` | Parent tag. Contains data fields for target custom field. For complete field listing, see [Custom Field](object-field-references#custom-field) in [Object Field References](object-field-references). |

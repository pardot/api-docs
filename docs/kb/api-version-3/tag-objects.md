# Querying TagObjects


## Supported Operations<a name="62781-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/tagObject/version/3/do/query?...` | `user_key, api_key` | Returns the tagObject matching the specified criteria parameters. See the [Using tagObjects](../using-tag-objects) section for a complete description of the tagObject [XML Response Format](../using-tag-objects#xml-response-format). Also see [TagObject](../object-field-references#tag-object) in [Object Field References](../object-field-references) |

<a name="62781-supported-search-criteria" id="supported-search-criteria"></a>

## Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 tagObjects will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.


| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for tagObjects that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Searches for tagObjects that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html) |
| `id_greater_than` | `integer` | `<any_positive_integer>` | Searches for tagObjects with IDs greater than the specified integer |
| `id_less_than` | `integer` | `<any_positive_integer>` | Searches for tagObjects with IDs less than the specified integer |
| `tag_id` | `integer` | `<any_positive_integer>` | Searches for tagObjects with a tag_id exactly matching the given id |
| `type` | `string` | `Automation, Block, Campaign, Competitor, Prospect Custom Field, Custom URL, Drip Program, Email, Email Draft, Email Template, Email Template Draft, File, Form, Form Field, Form Handler, Group, Keyword, Landing Page, Layout Template, List, Opportunity, Paid Search Campaign, Personalization, Profile, Prospect, Prospect Default Field, Segmentation Rule, Site, Site Search, Social Message, User, Dynamic Content` | Searches for tagObjects with a type exactly matching the given type. |
| `object_id` | `integer` | `<any_positive_integer>` | Searches for tagObjects with an object_id exactly matching the given id.  Note: You **must** accompany this parameter with the type parameter. |


## Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the tagObjects matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. If a number larger than 200 is specified, 200 will be used |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching tagObject (according to the specified sorting order) to be returned in the `query` response. The first `offset` matching tagObject will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=10` will return the results starting with the 11th tagObject matched by the provided criteria |
| `sort_by` | `string` | `created_at, id` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. _Default value:_ `id` |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supporting Sorting Options](#supported-sorting-options) for more details |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in tagObject queries, see TagObject in Object Field References.

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the tagObjects' `created_at` timestamps |
| `id` | `ascending` | Specifies that the query results should be sorted by the tagObjects' `id` fields |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <tagObject>...</tagObject>
        <tagObject>...</tagObject>
        <tagObject>...</tagObject>
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting tagObjects for the specified query |
| `<total_results>` | Contains the number of tagObjects selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched tagObject |
| `<tagObject>` | The data for an individual tagObject. See [Using tagObjects](../using-tag-objects) for a complete description of the tagObject [XML Response Format](../using-tag-objects#xml-response-format). Also see [TagObject](../object-field-references#tag-object) in [Object Field References](../object-field-references) |


# Using TagObjects


## Supported Operations<a name="62780-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [tagObject](../object-field-references#tag-object) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/tagObject/version/3/do/read/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the tagObject specified by `<id>`. `<id>` is the Pardot ID of the target tagObject. |
| `removed` | `/api/tagObject/version/3/do/delete/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the tagObject specified by `<id>`. Returns the tagObject ID and date the tagObject was removed. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <tagObject>
        <id>53772</id>
        <tag_id>111</tag_id>
        <type>Prospect</type>
        <object_id>1</object_id>
        <created_at>2011-03-01 16:03:41</created_at>
    </tagObject>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<tagObject>` | Parent tag. Contains data fields for target tagObject. For complete field listing, see [TagObject](../object-field-references#tagObject) in [Object Field References](../object-field-references). |

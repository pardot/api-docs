# Querying List Memberships


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="87486-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/listMembership/version/3/do/query?...` | `user_key, api_key` | Returns the list memberships matching the specified criteria parameters. See the [Using Lists](#using-list-memberships) section for a complete description of the list membership [XML Response Format](#xml-response-format). Also see [List Membership](../object-field-references.md#list-membership) in [Object Field References](../object-field-references.md). |


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
| `sort_by` | `string` | `created_at, id` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#supported-sorting-options) for more details. |
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
| `<list_membership>` | The data for an individual list membership. See [Using List Memberships](#using-list-memberships) for a complete description of the list membership [XML Response Format](#xml-response-format). Also see [List Membership](../object-field-references.md#list-membership) in [Object Field References](../object-field-references.md). |

# Using List Memberships


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="85559-supported-operations" id="supported-operations"></a>

List Membership can be controlled on a Prospect and List basis. In additon, the membership can reflect the opted "in" or opted "out" status for that Prospect and List combination. For a complete list of fields involved in list membership operations, see the [ListMembership](../object-field-references.md#list-membership) section of [Object Field References](../object-field-references.md).

| **Operation** | **URL Format**                                                                            | **Required Parameters**                    | **Description**  |
| ------------- | ----------------------------------------------------------------------------------------- | ------------------------------------------ | -----------------|
| `read`        | `/api/listMembership/version /3/do/read/id/<id>?...`                                       | `user_key, api_key, id`                    | Returns the data for the list membership specified by `<id>`. `<id>` is the Pardot ID of the target list membership. |
| `read`        | `/api/listMembership/version /3/do/read/list_id/<list_id>/ prospect_id/<prospect_id>?...`   | `user_key, api_key, list_id, prospect_id`  | Returns the data for the list membership specified by `<list_id>` and `<prospect_id>`. `<list_id>` is the Pardot list ID of the list and `<prospect_id>` is the Pardot prospect ID of the prospect for the target list membership. |
| `create`      | `/api/listMembership/version /3/do/create/list_id/<list_id>/ prospect_id/<prospect_id>?...` | `user_key, api_key, list_id, prospect_id`  | Creates a new list membership using the specified data. `<list_id>` is the Pardot list ID of the target list and `<prospect_id>` is the Pardot prospect ID of the target prospect. Opting out prospect from list may also be added with this request. |
| `update`      | `/api/listMembership/version /3/do/update/id/<id>?...`                                     | `user_key, api_key, id`                    | Updates the provided data for a list membership specified by `<id>`. `<id>` is the Pardot ID of the target list membership. Fields that are not updated by the request remain unchanged. |
| `update`      | `/api/listMembership/version /3/do/update/list_id/<list_id>/ prospect_id/<prospect_id>?...` | `user_key, api_key, list_id, prospect_id`  | Updates the provided data for a list membership specified by `<list_id>` and `<prospect_id>`. `<list_id>` is the Pardot list ID of the list and `<prospect_id>` is the Pardot prospect ID of the prospect for the target list membership. Fields that are not updated by the request remain unchanged. |
| `delete`      | `/api/listMembership/version /3/do/delete/id/<id>?...`                                     | `user_key, api_key, id`                    | Deletes the list membership specified by `<id>`. `<id>` is the Pardot ID of the target list membership. Returns HTTP 204 No Content on success. |
| `delete`      | `/api/listMembership/version /3/do/delete/list_id/<list_id>/ prospect_id/<prospect_id>?...` | `user_key, api_key, list_id, prospect_id`  | Deletes the list membership specified by `<list_id>` and `<prospect_id>`. `<list_id>` is the Pardot list ID of the list and `<prospect_id>` is the Pardot prospect ID of the prospect for the target list membership. Returns HTTP 204 No Content on success. |


## [](#xml-response-format-)XML Response Format

```
<rsp stat="ok" version="1.0">
    <list_membership>
        <id>1</id>
        <list_id>8</list_id>
        <prospect_id>622</prospect_id>
        <opted_out>false</opted_out>
        <created_at>2013-08-30 16:54:42</created_at>
        <updated_at>2014-10-24 14:04:47</updated_at>
    </list_membership>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<list_membership>` | Parent tag. Contains data fields for target list. For complete field listing, see [List Membership](../object-field-references.md#list-membership) in [Object Field References](../object-field-references.md). |

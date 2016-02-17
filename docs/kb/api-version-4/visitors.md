# Querying Visitors


##
[](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="14837-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/visitor/version/4/do/query?...` | `user_key, api_key` | Returns the visitors matching the specified criteria parameters. See the [Using Visitors](visitors) section for a complete description of visitor [XML Response Formats](visitors#xml-response-formats). Also see [Visitor](object-field-references#visitor) in [Object Field References](object-field-references). |

## [](#supported-search-criteria-)Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile` is specified, 200 visitors will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `created_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Selects visitors that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `created_before` | `string` | `today, yesterday, last_7_days, this_month, last_month,<custom_time>` | Selects visitors that were created before the specified time.If a `<custom_time>` is used, ensure that thespecified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `id_greater_than` | `integer` | `<any_positive_integer>` | Selects visitors with IDs greater than the specified integer. |
| `id_less_than` | `integer` | `<any_positive_integer>` | Selects visitors with IDs less than the specified integer. |
| `updated_after` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Selects visitors that were updated after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `updated_before` | `string` | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Selects visitors that were updated before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using [GNU Date Input Syntax](http://www.gnu.org/software/tar/manual/html_node/Date-input-formats.html). |
| `only_identified` | `boolean` | `true, false` | Selects visitors flagged as "Identified". _Default value:_ `true`. |
| `prospect_ids` | `array` | `<comma_separated_ids>` | Selects visits with the given Prospect IDs. The IDs should be comma separated positive integers (no spaces). We recommend using a POST request when providing this criteria. |


## [](#manipulating-the-result-set-)Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all the visitors matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.

| **Parameter** | **Datatype**                               | **Options**             | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
|`limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching visitor (according to the specified sorting order) to be returned in the query response. The first `offset` matching visitors will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=400` will return the results starting with the 401st visitor matched by the provided criteria. |
| `output` | `string` | `simple, mobile` | Specifies the format to be used when returning the results of the query. See [XML Response Formats](visitors#xml-response-formats) in [Using Visitors](visitors) for more details. |
| `sort_by` | `string` | `created_at, id, updated_at` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options](#14837-supported-sorting-options) for more details. _Default value:_ `id`. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supported Sorting Options](#supported-sorting-options) for more details. |


## [](#supported-sorting-options-)Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in visitor queries, see [Visitor](object-field-references#visitor) in [Object Field References](object-field-references).

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the visitors' `created_at` timestamps. |
| `id` | `ascending` | Specifies that the query results should be sorted by the visitors' `id` fields. |
| `updated_at` | `descending` | Specifies that the query results should be sorted by the visitors' `updated_at` timestamps. |


## [](#xml-response-format-)XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <visitor>...</visitor>
            ...
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting visitors for the specified query. |
| `<total_results>` | Contains the number of visitors selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all of the matched visitors. |
| `<visitor>` | The data for an individual visitor. See [Using Visitors](visitors) for complete descriptions of visitor [XML Response Formats](visitors#xml-response-formats). Also see [Visitor](object-field-references#visitor) in [Object Field References](object-field-references). **_Note:_** Data concerning a visitor's identified company, referrers, or activities will NOT be included in a `query` response. To retrieve this data, use a `read` request to retrieve the data for the visitor of interest. |

# Using Visitors


## Supported Operations<a name="20547-supported-operations"></a>

For a complete list of fields involved in visitor operations, see the [Visitor](object-field-references#visitor) section of [Object Field References](object-field-references).

| **Operation** | **URL Format**   | **Required Parameters** | **Description**  |
| ------------- | ---------------- | ----------------------- | -----------------|
| `assign` | `/api/visitor/version/4/do/assign/id/<id>?...` | `user_key, api_key, id, (prospect_email OR prospect_id)` | Assigns or reassigns the visitor specified by `<id>` to a specified prospect.  One (and only one) of the following parameters must be provided to identify the target prospect: `<prospect_email>` or `<prospect_id>`.  Returns an updated version of the visitor. |
| `read` | `/api/visitor/version/4/do/read/id/<id>?...` | `user_key, api_key, id` | Returns the data for the visitor specified by `<id>`, including associated visitor activities, identified company data, and visitor referrers. `<id>` is the Pardot ID for the target visitor. |

<a name="20547-xml-response-formats"></a>

## XML Response Formats

For `output=full`:

```
<rsp stat="ok" version="1.0">
    <visitor>
        ...
        <prospect>
            ...
        </prospect>
        <identified_company>
            ...
        </identified_company>
        <visitor_referrer>
            ...
        </visitor_referrer>
        <visitor_activities>
            <visitor_activity>
                ...
            </visitor_activity>
        </visitor_activities>
    </visitor>
</rsp>
```

For `output=simple`:

```
<rsp stat="ok" version="1.0">
    <visitor>
        ...
    </visitor>
</rsp>
```

For `output=mobile`:

```
<rsp stat="ok" version="1.0">
    <visitor>
        <id>...</id>
        <prospect_id>...</prospect_id>
        <page_view_count>...</page_view_count>
        <ip_address>...</ip_address>
        <hostname>...</hostname>
        <created_at>...</created_at>
        <updated_at>...</updated_at>
    </visitor>
</rsp>
```

| **Tag**                    | **Description** |
|----------------------------|-----------------|
| `<visitor>` | Parent tag. Contains data fields for target visitor.  For complete field listing, see [Visitor](object-field-references#visitor) in [Object Field References](object-field-references). |
| `<prospect>` | Contains data about the prospect to which this visitor is assigned.  The prospect's data is returned in `mobile` output format.  See [XML Response Formats](using-prospects#xml-response-formats) in [Using Prospects](using-prospects). |
| `<identified_company>` | Contains data about the identified company associated with this visitor.  This leaf only appears if an identified company is associated with this visitor.  See [Identified Company](object-field-references#identified-company) in [Object Field References](object-field-references). |
| `<visitor_referrer>` | Contains data about this visitor's referrer.  This leaf only appears if this visitor has an associated visitor referrer.  For complete field listing, see [Visitor Referrer](object-field-references#visitor-referrer) in [Object Field References](object-field-references). |
| `<visitor_activities>` | Contains all visitor activities associated with this visitor.  Contains only `<visitor_activity>` tags. |
| `<visitor_activity>` | Contains data fields for a visitor activity.  For complete field listing, see [Visitor Activity](object-field-references#visitor-activity) in [Object Field References](object-field-references). |

<a name="20547-assigning-and-reassigning-visitors"></a>

## Assigning and Reassigning Visitors

To assign/reassign a visitor, both the visitor to be assigned and the target prospect of the assignment must be defined.  Visitors are specified by their Pardot ID.  Prospects can be specified by their Pardot user ID or by their email address.  Possible combinations of parameters are shown below.  Developers are responsible for substituting specific values for parameters denoted by `<carets>`.

**_Examples:_**

```
/api/visitor/version/4/do/assign/id/<visitor_id>?prospect_email=<prospect_email>&api_key=<api_key>&user_key=<user_key>
/api/visitor/version/4/do/assign/id/<visitor_id>?prospect_id=<prospect_id>&api_key=<api_key>&user_key=<user_key>
```

XML responses to `assign` requests are identical to `read` requests, but reflect the new visitor assignment in the `<prospect>` node.


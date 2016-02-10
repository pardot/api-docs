# Querying Opportunities


## Supported Operations<a name="14770-supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query` | `/api/opportunity/version/3/do/query?...` | `user_key, api_key` | Returns the opportunities matching the specified criteria parameters. See [Using Opportunities (using-opportunities) for complete descriptions of opportunity [XML Response Formats](opportunities#xml-response-formats). Also see [Opportunity](object-field references#opportunity) in [Object Field References](object-field-references). |

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
| `output` | `simple, mobile` |  | Specifies the format to be used when returning the results of the query. See [XML Response Formats](opportunities#xml-response-formats) in [Using Opportunities](opportunities) for more details. |
| `sort_by` | `string` | `created_at, id, probability, value` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options (#14770-supported-sorting-options) for more details. _Default value:_ `id`. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default sorting order varies based on the value of the `sort_by` parameter. See [Supported Sorting Options](#supported-sorting-options) for more details. |

## Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in Opportunity queries, see [Opportunity](object-field-references#opportunity) in [Object Field References](object-field-references).


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
| `<opportunity>` | The data for an individual Opportunity. See [Using Opportunities](opportunities) for complete descriptions of opportunity [XML Response Formats](opportunities#xml-response-formats). Also see [Opportunity](object-field-references#opportunity) in [Object Field References](object-field-references). **_Note:_** Data concerning an opportunity's activities will NOT be included in a `query` response. To retrieve this data, use a `read` request for individual opportunities of interest. |

# Using Opportunities


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="14772-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in Opportunities operations, see the [Opportunity](object-field-references#opportunity) section of [Object Field References](object-field-references).

**_Note:_** If a salesforce.com or SugarCRM connector is present in the API user's account, Opportunities can be read, but they cannot be modified (created, updated, deleted or undeleted).


| **Operation** | **URL Format**   | **Required Parameters** | **Description**  |
| ------------- | ---------------- | ----------------------- | -----------------|
| `create`      | `/api/opportunity /version/3/do/create /prospect_email /<prospect_email>?...` | `user_key, api_key, prospect_email, name, value, probability` | Creates a new opportunity using the specified data. `prospect_email` must correspond to an existing prospect. `name`, `value`, and `probability` must also be specified. See [Opportunity](object-field-references#opportunity) in [Object Field References](object-field-references) for other field requirements. **_Note:_** If both `prospect_email` and `prospect_id` are specified, both must correspond to the same prospect. Otherwise, the API will return an error. |
| `create`      | `/api/opportunity /version/3/do/create /prospect_id /<prospect_id>?...` | `user_key, api_key, prospect_id, name, value, probability` | Creates a new opportunity using the specified data. `prospect_id` must correspond to an existing prospect. `name`, `value`, and `probability` must also be specified. See [Opportunity](object-field-references#opportunity) in [Object Field References](object-field-references) for other field requirements. **_Note:_** If both `prospect_email` and `prospect_id` are specified, both must correspond to the same prospect. Otherwise, the API will return an error. |
| `read`        | `/api/opportunity /version/3/do/read /id/<id>?...` | `user_key, api_key, id` | Returns the data for the opportunity specified by `id`, including campaign assignment and associated visitor activities. `id` is the Pardot ID for the target opportunity. |
| `update`   | `/api/opportunity /version/3/do/update /id/<id>?...`   | `user_key, api_key, id` | Updates the provided data for the opportunity specified by `id`. `id` is the Pardot ID for the target opportunity. Fields that are not updated by the request remain unchanged. Returns an updated version of the opportunity. |
| `delete`   | `/api/opportunity /version/3/do/delete /id/<id>?...`   | `user_key, api_key, id` | Deletes the opportunity specified by `id`. `id` is the Pardot ID for the target opportunity. Returns no response on success. **_Note:_** Deleting an opportunity, whether via the API or within Pardot, will not delete the Visitor Activities or Score changes for the Prospect to whom the Opportunity is linked.
| `undelete` | `/api/opportunity /version/3/do/undelete /id/<id>?...` | `user_key, api_key, id` | Undeletes the opportunity specified by `id`. `id` is the Pardot ID for the target opportunity. Returns no response on success. |

<a name="14772-xml-response-formats" id="xml-response-formats"></a>

## [](#xml-response-formats-)XML Response Formats

For `output=full`:

```
<rsp stat="ok" version="1.0">
    <opportunity>
        ...
        <campaign>
            ...
        </campaign>
        <prospects>
            <prospect>
                ...
            </prospect>
        </prospects>
        <opportunity_activities>
            <visitor_activity>
                ...
            </visitor_activity>
        </opportunity_activities>
    </opportunity>
</rsp>
```

For `output=simple`:

```
<rsp stat="ok" version="1.0">
    <opportunity>
        ...
        <campaign>
            ...
        </campaign>
        <prospects>
            <prospect>
                ...
            </prospect>
        </prospects>
    </opportunity>
</rsp>
```

For `output=mobile`:

```
<rsp stat="ok" version="1.0">
    <opportunity>
        ...
    </opportunity>
</rsp>
```

| **Tag**                    | **Description** |
|----------------------------|-----------------|
| `<opportunity>`            | Parent tag. Contains data fields for target opportunity. Forcomplete field listing, see [Opportunity](object-field-references#opportunity) in [Object Field References](object-field-references). |
| `<campaign>`               | Contains `<id>` and `<name>` of the campaign to which this opportunity has been assigned. |
| `<prospects>`              | Contains all prospects associated with this opportunity. Contains only `<prospect>` tags. |
| `<opportunity_activities>` | Contains all visitor activities associated with this opportunity. Contains only `<visitor_activity>` tags. |
| `<visitor_activity>`       | Contains data fields for a visitor activity. For complete field listing, see [Visitor Activity](object-field-references#visitor-activity) in [Object Field References](object-field-references). |

<a name="14772-updating-field-values" id="updating-field-values"></a>

## [](#updating-field-values-)Updating Field Values

Modifying values of opportunity data fields is done by submitting an `update` request with parameters for each field to be updated. Each parameter is formatted as `<field_name>=<value>`.

**_Example:_** _Updating the value of a opportunity (whose Pardot ID is 27):_

```
POST: /api/opportunity/version/3/do/update/id/27 message body: value=50000&amp;api_key=&amp;user_key=

GET: /api/opportunity/version/3/do/update/id/27?value=50000&api_key=<api_key>&user_key=<user_key>
```

Only values that are specifically named in the request are updated. All others are left unchanged. To clear a value, submit an `update` request containing a parameter with no specified value, such as `status=`.


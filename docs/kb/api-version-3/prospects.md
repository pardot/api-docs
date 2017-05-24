# Querying Prospects


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="14784-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `query`       | `/api/prospect/version/3/do/query?...`     | `user_key, api_key`     | Returns the prospects matching the specified criteria parameters. See [Using Prospects](prospects/#using-prospects) for complete descriptions of prospect [XML Response Formats](prospects/#xml-response-formats). Also see [Prospect](../object-field-references#prospect) in [Object Field References](../object-field-references). |


## [](#supported-search-criteria-)Supported Search Criteria

Search criteria may be used together in any combination and/or order unless otherwise specified. Unless `output=mobile`is specified, 200 prospects will be returned with each query request. This limit is not enforced for responses formatted for mobile devices.


| Parameter              | Datatype         | Options                                                                | Description |
|------------------------|------------------|------------------------------------------------------------------------|-------------|
| `assigned`             | `boolean`        | `true, false`                                                          | Selects prospects based on whether they are assigned.                                                                                                                                                                                                                                                                                                                                                            |
| `assigned_to_user`     | `integer/string` | `<any_positive_integer>, <any_string>`                                 | Selects prospects based on whether they are assigned to a specified user. Users can be specified by their email address or their Pardot IDs.Note: Using `assigned_to_user` overrides the `assigned` criteria.                                                                                                                                                                                                         |
| `created_after`        | `string`         | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Selects prospects that were created after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using GNU Date Input Syntax.                                                                                                                                                                                                                                                |
| `created_before`       | `string`         | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Selects prospects that were created before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using GNU Date Input Syntax.                                                                                                                                                                                                                                               |
| `deleted`              | `boolean`        | `true, false`                                                          | Selects prospects based on whether they have been deleted.Default value: false.                                                                                                                                                                                                                                                                                                                                  |
| `grade_equal_to`       | `string`         | `A+, A, A-, B+, B, B-, C+, C, C-, D+, D, D-, F`                        | Selects prospects that have a grade equal to the specified grade. Note: Any value provided for `grade_equal_to` MUST be URL-encoded.                                                                                                                                                                                                                                                                                 |
| `grade_greater_than`   | `string`         | `A+, A, A-, B+, B, B-, C+, C, C-, D+, D, D-, F`                        | Selects prospects that have a grade greater than the specified grade. Note: Any value provided for `grade_greater_than` MUST be URL-encoded.                                                                                                                                                                                                                                                                         |
| `grade_less_than`      | `string`         | `A+, A, A-, B+, B, B-, C+, C, C-, D+, D, D-, F`                        | Selects prospects that have a grade less than the specified grade. Note: Any value provided for `grade_less_than` MUST be URL-encoded.                                                                                                                                                                                                                                                                               |
| `id_greater_than`      | `integer`        | `<any_positive_integer>`                                               | Selects prospects with IDs greater than the specified integer.                                                                                                                                                                                                                                                                                                                                                   |
| `id_less_than`         | `integer`        | `<any_positive_integer>`                                               | Selects prospects with IDs less than the specified integer.                                                                                                                                                                                                                                                                                                                                                      |
| `is_starred`           | `boolean`        | `true, false`                                                          | Selects prospects based on whether they are starred.                                                                                                                                                                                                                                                                                                                                                             |
| `last_activity_before` | `string`         | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Selects prospects that have been active before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using GNU Date Input Syntax. Prospects are considered active if a prospect's `last_activity_at` is before the specified time. See [Prospect](../object-field-references#prospect) in [Object Field References](../object-field-references).                                                                                                    |
| `last_activity_after`  | `string`         | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Selects prospects that have been active after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using GNU Date Input Syntax. Prospects are considered active if a prospect's `last_activity_at` is after the specified time. See [Prospect](../object-field-references#prospect) in [Object Field References](../object-field-references).                                                                                                      |
| `last_activity_never`  | `boolean`        | `TRUE`                                                                 | Selects prospects that have never been active. Prospects are considered active if a prospect's `last_activity_at` is null. See [Prospect](../object-field-references#prospect) in [Object Field References](../object-field-references).                                                                                                                                                                                                                                                |
| `list_id`              | `integer`        | `<any positive integer>`                                               | Selects prospects based on their membership of the list with the given `list_id`.                                                                                                                                                                                                                                                                                                                                  |
| `new`                  | `boolean`        | `true, false`                                                          | Selects prospects based on whether they are classified as new. Prospects are considered new if they have not been assigned to a user or a queue, have not been marked as reviewed, and have a `last_activity_at` timestamp specified. See [Prospect](../object-field-references#prospect) in [Object Field References](../object-field-references). Note: Using the new criteria overrides the `assigned`, `assigned_to_user`, `last_activity_at`, and `last_activity_before` criteria if specified. |
| `score_equal_to`       | `integer`        | `<any_integer>`                                                        | Selects prospects that have a score equal to a specified integer.                                                                                                                                                                                                                                                                                                                                                |
| `score_greater_than`   | `integer`        | `<any_integer>`                                                        | Selects prospects that have a score greater than a specified integer.                                                                                                                                                                                                                                                                                                                                            |
| `score_less_than`      | `integer`        | `<any_integer>`                                                        | Selects prospects that have a score less than a specified integer                                                                                                                                                                                                                                                                                                                                                |
| `updated_after`        | `string`         | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Selects prospects that were last updated after the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using GNU Date Input Syntax.                                                                                                                                                                                                                                           |
| `updated_before`       | `string`         | `today, yesterday, last_7_days, this_month, last_month, <custom_time>` | Selects prospects that were last updated before the specified time. If a `<custom_time>` is used, ensure that the specified date is formatted using GNU Date Input Syntax.                                                                                                                                                                                                                                          |

## [](#manipulating-the-result-set-)Manipulating the Result Set

Since `query` result sets are limited to 200 results each, the results returned may not include all prospects that were matched by the query. To retrieve the remaining results, the following criteria can be used to navigate through the result set.


| Parameter              | Datatype         | Options                                                                | Description |
|------------------------|------------------|------------------------------------------------------------------------|-------------|
| `fields` | `array` | `<comma_separated_field_ids>` | Specifies the fields to be returned. **Note:** If this parameter isn't present, all default fields and custom fields for which the prospect has a value will be returned; &lt;id&gt; will always be returned. |
| `limit` | `integer` | `<any_positive_integer>` | Specifies the number of results to be returned. _Default value:_ `200`. **_Note:_** This number cannot be larger than 200. |
| `offset` | `integer` | `<any_positive_integer>` | Specifies the first matching prospect(according to the specified sorting order) to be returned in the query response. The first `offset` matching prospects will be omitted from the response. _Default value:_ `0`. **_Example:_** Specifying `offset=400` will return the results starting with the 401st prospect matched by the provided criteria. |
| `output` | `string` | `simple, mobile` | Specifies the format to be used when returning the results of the query. See [XML Response Formats](prospects/#xml-response-formats) in [Using Prospects](prospects/#using-prospects) for more details. |
| `sort_by` | `string` | `created_at, id, probability, value` | Specifies the field that should be used to sort the results of the query. See [Supported Sorting Options (#14784-supported-sorting-options) for more details. |
| `sort_order` | `string` | `ascending, descending` | Specifies the ordering to be used when sorting the results of the query. The default value varies based on the value of the `sort_by` parameter. See [Supported Sorting Options](#supported-sorting-options) for more details. |

## [](#supported-sorting-options-)Supported Sorting Options

The ordering of the results returned by a `query` request can be changed by specifying `sort_by` and `sort_order` parameters. Any of the following values are valid when specifying the `sort_by` parameter. For a complete list of fields involved in Prospect queries, see [Prospect](../object-field-references#prospect) in [Object Field References](../object-field-references).

| **Value** | **Default Sort Order** | **Description** |
| --------- | ---------------------- | --------------- |
| `created_at` | `descending` | Specifies that the query results should be sorted by the prospects' `created_at` timestamps. |
| `id` | `ascending` | Specifies that the query results should be sorted by the prospects' `id` fields. |
| `last_activity_at` | `descending` | Specifies that the query results should be sorted by the prospects' `last_activity_at` timestamps. |
| `updated_at` | `descending` | Specifies that the query results should be sorted by the prospects' `updated_at` timestamps. |

## [](#xml-response-format-)XML Response Format

```
<rsp stat="ok" version="1.0">
    <result>
        <total_results>...</total_results>
        <prospect>...</prospect>
            ...
    </result>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<result>` | Contains the resulting prospects for the specified query. |
| `<total_results>` | Contains the number of prospects selected by this query. If this value is higher than 200, then several query requests may be necessary to retrieve all matched prospects. |
| `<prospect>` | The data for an individual Prospect. See [Using Prospects](prospects/#using-prospects) for complete descriptions of prospect [XML Response Formats](prospects/#xml-response-formats). Also see [Prospect](../object-field-references#prospect) in [Object Field References](../object-field-references). **_Note:_** Data concerning a prospect's profile criteria matchings, visitors, visitor activities, and list subscriptions will NOT be included in a `query` response. To retrieve this data, submit a `read` request for the prospect of interest. |

# Using Prospects


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="14833-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in Prospect operations, see the [Prospect](../object-field-references#prospect) section of [Object Field References](../object-field-references).


| **Operation** | **URL Format**   | **Required Parameters** | **Description**  |
| ------------- | ---------------- | ----------------------- | -----------------|
| `assign`      | `/api/prospect /version/3 /do/assign/ email/<email>?...` | `user_key, api_key, email, (user_email OR user_id OR group_id)` | Assigns or reassigns the prospect specified by `<email>` to a specified Pardot user or group. One (and only one) of the following parameters must be provided to identify the target user or group: `<user_email>`, `<user_id>`, or `<group_id>`. Returns an updated version of the prospect. **_Note:_** Prospect assignments and reassignments do not overwrite existing assignments in CRMs. |
| `assign`      | `/api/prospect /version/3 /do/assign/ id/<id>?...` | `user_key, api_key, id, (user_email OR user_id OR group_id)` | Assigns or reassigns the prospect specified by `<id>` to a specified Pardot user or group. One (and only one) of the following parameters must be provided to identify the target user or group: `<user_email>`, `<user_id>`, or `<group_id>`. Returns an updated version of the prospect. **_Note:_** Prospect assignments and reassignments do not overwrite existing assignments in CRMs. |
| `unassign`    | `/api/prospect /version/3 /do/unassign/ email/<email>?...` | `user_key, api_key, email` | Unassigns the prospect specified by `<email>`. Returns an updated version of the prospect. **_Note:_**Prospect assignments and reassignments do not overwrite existing assignments in CRMs. **_Note:_** Prospect assignments and reassignments do not overwrite existing assignments in CRMs. |
| `unassign`    | `/api/prospect /version/3 /do/unassign/ id/<id>?...`   | `user_key, api_key, id` | Unassigns the prospect specified by `<id>`. Returns an updated version of the prospect. **_Note:_** Prospect assignments and reassignments do not overwrite existing assignments in CRMs. **_Note:_** Prospect assignments and reassignments do not overwrite existing assignments in CRMs. |
| `create`      | `/api/prospect /version/3 /do/create/ email/<email>?...` | `user_key, api_key, email` | Creates a new prospect using the specified data. `<email>` must be a unique email address. Email list subscriptions and custom field data may also be added with this request. Refer to the [Updating Email List Subscriptions](#updating-email-list-subscriptions) and [Updating Field Values](#14833-updating-field-values) sections for more details.
| `batchCreate` | `/api/prospect /version/3 /do/batchCreate? prospects=<data>...` | `user_key, api_key, prospects` | Creates new prospects using the provided `<data>` in either XML or JSON. See [Endpoints for Batch Processing](#endpoints-for-batch-processing)
| `read`        | `/api/prospect /version/3 /do/read/ email/<email>?...` | `user_key, api_key, email` | Returns data for the prospect specified by `<email>`, including campaign assignment, profile criteria matching statuses, associated visitor activities, email list subscriptions, and custom field data. `<email>` is the email address of the target prospect. |
| `read`        | `/api/prospect /version/3 /do/read/ id/<id>?...` | `user_key, api_key, id` | Returns data for the prospect specified by `<id>`, including campaign assignment, profile criteria matching statuses, associated visitor activities, email list subscriptions, and custom field data. `<id>` is the Pardot ID of the target prospect. |
| `update`      | `/api/prospect /version/3 /do/update/ email/<email>?...` | `user_key, api_key, email` | Updates the provided data for a prospect specified by `<email>`. `<email>` is the email address of the prospect. Fields that are not updated by the request remain unchanged. Email list subscriptions and custom field data may also be updated with this request. Refer to the [Updating Email List Subscriptions](#updating-email-list-subscriptions) and [Updating Field Values](#14833-updating-field-values) sections for more details. Returns an updated version of the prospect. **_Note:_** Prospect email addresses cannot be updated using this method. |
| `update`      | `/api/prospect /version/3 /do/update/ id/<id>?...` | `user_key, api_key, id` | Updates the provided data for a prospect specified by `<id>`. `<id>` is the Pardot ID of the prospect. Fields that are not updated by the request remain unchanged. Email list subscriptions and custom field data may also be updated with this request. Refer to the [Updating Email List Subscriptions](#updating-email-list-subscriptions) and [Updating Field Values](#14833-updating-field-values) sections for more details. Returns an updated version of the prospect. |
| `batchUpdate` | `/api/prospect /version/3 /do/batchUpdate? prospects=<data>...` | `user_key, api_key, prospects` | Updates prospects using the provided `<data>` in either XML or JSON. See [Endpoints for Batch Processing](#endpoints-for-batch-processing)
| `upsert`      | `/api/prospect /version/3 /do/upsert/ email/<email>?...`   | `user_key, api_key, email` | Updates the provided data for the prospect specified by `<email>`. If a prospect with the provided email address does not yet exist, a new prospect is created using the `<email>` value. Fields that are not updated by the request remain unchanged. Email list subscriptions and custom field data may also be updated with this request. Refer to the [Updating Email List Subscriptions](#14833-updating-email-list-subscriptions) and [Updating Field Values](#14833-updating-field-values) sections for more details. Returns an updated version of the prospect. |
| `upsert`      | `/api/prospect /version/3 /do/upsert/ id/<id>?...` | `user_key, api_key, (id OR email)` | Updates the provided data for the prospect specified by `<id>`. If an `<email>` value is provided, it is used to update the prospect's email address. If a prospect with the provided ID is not found, Pardot searches for a prospect identified by `<email>`. If a prospect with the provided email address does not yet exist, a new prospect is created using `<email>` value. Fields that are not updated by the request remain unchanged. Email list subscriptions and custom field data may also be updated with this request. Refer to the [Updating Email List Subscriptions](#updating-email-list-subscriptions) and [Updating Field Values](#14833-updating-field-values) sections for more details. Returns an updated version of the prospect.
| `batchUpsert` | `/api/prospect /version/3 /do/batchUpsert? prospects=<data>...` | `user_key, api_key, prospects` | Updates prospects using the provided `<data>` in either XML or JSON. See [Endpoints for Batch Processing](#endpoints-for-batch-processing)
| `delete`      | `/api/prospect /version/3 /do/delete/ email/<email>?...` | `user_key, api_key, email` | Deletes the prospect specified by `<email>`. Returns HTTP 204 No Content on success. **_Note:_** Prospects may only be deleted using HTTP methods POST or DELETE. |
| `delete`      | `/api/prospect /version/3 /do/delete/ id/<id>?...` | `user_key, api_key, id` | Deletes the prospect specified by `<id>`. Returns HTTP 204 No Content on success. **_Note:_** Prospects may only be deleted using HTTP methods POST or DELETE. |



<a name="14833-xml-response-formats" id="xml-response-formats"></a>

## [](#xml-response-formats-)XML Response Formats

For `output=full`:

```
<rsp stat="ok" version="1.0">
    <prospect>
        ...
        <campaign>
            ...
        </campaign>
        <assigned_to>
            ...
        </assigned_to>
        <last_activity>
            ...
        </last_activity>
        <profile>
            ...
            <profile_criteria>
                ...
            </profile_criteria>
        </profile>
        <visitors>
            <visitor>
                ...
                <identified_company>
                    ...
                </identified_company>
                <visitor_referrer>
                    ...
                </visitor_referrer>
            </visitor>
        </visitors>
        <visitor_activities>
            <visitor_activity>
                ...
            </visitor_activity>
        </visitor_activities>
        <lists>
            <list_subscription>
                ...
                <list>
                    ...
                </list>
            </list_subscription>
        </lists>
    </prospect>
</rsp>
```

For `output=simple`:

```
<rsp stat="ok" version="1.0">
    <prospect>
        ...
        <campaign>
            ...
        </campaign>
        <assigned_to>
            ...
        </assigned_to>
        <last_activity>
            ...
        </last_activity>
    </prospect>
</rsp>
```

For `output=mobile`:

```
<rsp stat="ok" version="1.0">
    <prospect>
        <id>...</id>
        <first_name>...</first_name>
        <last_name>...</last_name>
        <email>...</email>
        <company>...</company>
    </prospect>
</rsp>
```
| **Tag**                    | **Description** |
|----------------------------|-----------------|
| `<prospect>`            | Parent tag. Contains data fields for the target prospect (including custom fields). For complete field listing, see [Prospect](../object-field-references#prospect) in [Object Field References](../object-field-references). |
| `<value>`               | Child tag of data fields with multiple values. Only appears with custom fields that have multiple values.|
| `<campaign>` | Contains `<id>` and `<name>` of the campaign to which this prospect has been assigned. This leaf only appears if the prospect has been assigned to a campaign. |
| `<assigned_to>` | Contains a `<user>` node detailing the user to whom this prospect has been assigned. This leaf only appears if the prospect has been assigned to a user. See [User](../object-field-references#user) in [Object Field References](../object-field-references). |
| `<last_activity>` | Contains a `<visitor_activity>` node detailing this prospect's most recent activity. This leaf only appears if the prospect has visitor activities associated with it. For complete field listing, see [Visitor Activity](../object-field-references#visitor-activity) in [Object Field References](../object-field-references). |
| `<profile>` | Contains all data fields for the profile associated with this prospect. Also contains several `<profile_criteria>` tags. For complete field listing, see [Profile](../object-field-references#profile) in [Object Field References.](../object-field-references) |
| `<profile_criteria>` | Contains all data fields for the profile criteria associated with the prospect's assigned profile. For complete field listing, see [Profile Criteria](../object-field-references#profile-criteria) in [Object Field References](../object-field-references). |
| `<visitors>` | Contains all visitors associated with this prospect. Contains only `<visitor>` tags. |
| `<visitor>` | Contains data fields for a visitor activity, as well as an `<identified_company>` and a `<visitor_referrer>` tag. For complete field listing, see [Visitor](../object-field-references#visitor) in [Object Field References](../object-field-references). |
| `<identified_company>` | Contains data field for a visitor's identified company. For complete field listing, see [Identified Company](../object-field-references#identified-company) in [Object Field References](../object-field-references). |
| `<visitor_referrer>` | Contains data fields for a visitor's referrer. For complete field listing, see [Visitor Referrer](../object-field-references#visitor-referrer) in [Object Field References](../object-field-references). |
| `<visitor_activities>` | Contains all visitor activities associated with this prospect. Contains only `<visitor_activity>` tags. |
| `<visitor_activity>` | Contains data fields for a visitor activity. For complete field listing, see [Visitor Activity](../object-field-references#visitor-activity) in [Object Field References](../object-field-references). |
| `<lists>` | Contains all email list subscriptions for this prospect. Contains only `<list_subscription>` tags. |
| `<list_subscription>` | Contains data fields for an email list subscription, as well as a `<list>` tag. For complete field listing, see [Email List Subscription](../object-field-references#email-list-subscription) in [Object Field References](../object-field-references). |
| `<list>` | Contains data fields for an email list. For complete field listing, see [Email List](../object-field-references#email-list) in [Object Field References](../object-field-references). |

<a name="14833-assigning-and-reassigning-prospects" id="assigning-and-reassigning-prospects"></a>

## [](#assigning-and-reassigning-prospects-)Assigning and Reassigning Prospects

To assign/reassign a prospect, both the prospect to be assigned and the target user or group of the assignment must be defined. Prospects can be specified by their Pardot ID or email address. Users or groups can be specified by their Pardot user ID, email address, or Pardot group ID. Possible combinations of parameters are shown below. Developers are responsible for substituting specific values for parameters denoted by `<carets>`.

**_Examples:_**

/api/prospect/version/3/do/assign/email/?user_email=&amp;api_key=&amp;user_key=

/api/prospect/version/3/do/assign/email/?user_id=&amp;api_key=&amp;user_key=

/api/prospect/version/3/do/assign/email/?group_id=&amp;api_key=&amp;user_key=

/api/prospect/version/3/do/assign/id/?user_email=&amp;api_key=&amp;user_key=

/api/prospect/version/3/do/assign/id/?user_id=&amp;api_key=&amp;user_key=

/api/prospect/version/3/do/assign/id/?group_id=&amp;api_key=&amp;user_key=

XML responses to `assign` requests are identical to `read` requests, but reflect the new prospect assignment in the `<assigned_to>` node.

<a name="14833-creating-prospects" id="creating-prospects"></a>

## [](#creating-prospects-)Creating Prospects

To create a prospect via the API, only a valid and unique email address is required. Values for any other prospect fields may also be provided in the `create` request. Developers are responsible for substituting specific values for parameters denoted by `<carets>`.

_**Example:** Creating a new prospect_/api/prospect/version/3/do/create/email/[new_prospect@pardot.com](mailto:new_prospect@pardot.com)?first_name=New&amp;last_name=Prospect&amp;api_key=&amp;user_key=

XML responses to `create` requests are identical to `update` and `read` requests. If no `campaign_id` value is provided, the new prospect will be automatically assigned to the oldest existing campaign.

<a name="14833-updating-field-values" id="updating-field-values"></a>

## [](#endpoints-batch-processing-)Endpoints for Batch Processing

There are 3 endpoints available for batch processing up to 50 prospects at a time:

/api/prospect/version/3/do/batchCreate

/api/prospect/version/3/do/batchUpdate

/api/prospect/version/3/do/batchUpsert

These endpoints expect a query variable called "prospects" which holds either JSON or XML encoded data. Each prospect should have a unique identifier which will be used in the return output.

JSON Example:

```
{
    "prospects": {
        "1234": {
            "first_name": "New first name",
            "last_name": "New last name"
        },
        "some@email.com": {
            "first_name": "New first name",
            "last_name": "New last name"
        },
        "some.other@email.com": {
            "first_name": "New first name",
            "last_name": "New last name"
        }
    }
}
```
XML Example:
```
<prospects>
    <prospect identifier="1234">
        <first_name>New first name</first_name>
        <last_name>New last name</last_name>
    </prospect>
    <prospect identifier="some@email.com">
        <first_name>New first name</first_name>
        <last_name>New last name</last_name>
    </prospect>
    <prospect identifier="some.other@email.com">
        <first_name>New first name</first_name>
        <last_name>New last name</last_name>
    </prospect>
</prospects>
```

If using `batchCreate`, you'll need to provide a valid and unique email address for each prospect. The `batchUpdate` and `batchUpsert` endpoints allow the use of a prospect ID or prospect email address.

**_Example:_**

/api/prospect/version/3/do/batchUpdate?prospects={"prospects":{"some@email.com":{"first_name":"New first name","last_name":"New last name"},"1234":{"first_name":"New first name","last_name":"New last name"}}}&api_key=&user_key=

**Note:** The return value will either be XML or JSON (XML by default. If you want JSON, then add "&format=json" to your HTTP query).


## [](#updating-field-values-)Updating Field Values

Modifying values of prospect data fields is done by submitting an `update` request with parameters for each field to be updated. Each parameter is formatted as `<field_name>=<value>`. Custom field values are updated using the same syntax.

_**Example:** Updating the phone number of a prospect whose email address is_ `bob@pardot.com`: /api/prospect/version/3/do/update/email/[bob@pardot.com](mailto:bob@pardot.com)?phone=888-123-4567&amp;api_key=&amp;user_key=

Only values that are specifically named in the request are updated. All others are left unchanged. To clear a value, submit an `update` request containing a parameter with no specified value, such as `phone=`.

**_Note:_** Any field that is set to record multiple responses cannot have its values cleared this way.

<a name="14833-updating-fields-with-predefined-values" id="updating-fields-with-predefined-values"></a>

## [](#updating-fields-with-predefined-values-)Updating Fields with Predefined Values

Modifying values of prospect data fields with predefined values is accomplished through an `update` request with parameters for each field to be updated. Each parameter is formatted as `<field_name>=<value>` where `<value>` matches the predefined field value. Custom field values are updated using the same syntax.

_**Example:** Updating the category of a prospect whose email address is_ `bob@pardot.com` *to the category `consumer`: /api/prospect/version/3/do/update/email/[bob@pardot.com](mailto:bob@pardot.com)?category=consumer&amp;api_key=&amp;user_key=

<a name="14833-updating-fields-with-multiple-values" id="updating-fields-with-multiple-values"></a>

## [](#updating-fields-with-multiple-values-)Updating Fields with Multiple Values

Updating field values with multiple values follows the same convention as fields with predefined values, but requires a different parameter naming scheme to allow multiplicity. An `update` request is submitted with parameters formatted as `<field_name>_<count>=<field_value>` where `<count>` is an integer denoting the current parameter's place in sequence. `<count>` must start at 0 and increase by 1 until all desired values are submitted.

_**Example:** Modifying the values of a custom field with field name_ `past_jobs` _for a prospect with a Pardot ID of_ `5`: /api/prospect/version/3/do/update/id/5?past_jobs_0=janitor&amp;past_jobs_1=security&amp;api_key=&amp;user_key=

**Note:** Checkbox and multi-select fields are the only field types that can be updated in this manner. To clear all of the values for a checkbox or multi-select field, use `<field_name>_0=`. To clear specific values, just set the values that should remain in the prospect record using the method above.

<a name="14833-updating-email-list-subscriptions" id="updating-email-list-subscriptions"></a>

## [](#updating-email-list-subscriptions-)Updating Email List Subscriptions

To modify email list subscriptions for a prospect, the Pardot ID of the email list is required. Once the ID is obtained, an `update` is submitted with parameters formatted as `list_<list_id>=1` to create a subscription and `list_<list_id>=0` to end a subscription.

_**Example:** Adding a prospect whose email address is_ `bob@pardot.com` _to an email list with Pardot ID_ `8`: /api/prospect/version/3/do/update/email/[bob@pardot.com](mailto:bob@pardot.com)?list_8=1&amp;api_key=&amp;user_key=

Requests that attempt to subscribe a prospect to lists that it is already subscribed to are ignored. Unsubscribe requests are handled similarly.

<a name="14833-updating-profile-criteria-matching-statuses" id="updating-profile-criteria-matching-statuses"></a>

## [](#updating-profile-criteria-matching-statuses-)Updating Profile Criteria Matching Statuses

To modify a prospect's matching status for associated profile criteria, the Pardot ID of the profile criteria is required. Once the ID is obtained, an `update` is submitted with parameters formatted as `profile_criteria_<profile_criteria_id>=<status>`. The value of `<status>` may be either `match`, `nomatch`, or `unknown`.

_**Example:** Setting a profile criteria for a prospect whose email address is_ `bob@pardot.com` _to_ `match`: /api/prospect/version/3/do/update/email/[bob@pardot.com](mailto:bob@pardot.com)?profile_criteria_8=match&amp;api_key=&amp;user_key=_**Example:** Setting a profile criteria for a prospect with Pardot ID_ `58` _to_ `nomatch`: /api/prospect/version/3/do/update/id/58?profile_criteria_8=nomatch&amp;api_key=&amp;user_key=

Only profile criteria that belong to the profile associated with the prospect can be updated using this method. Requests to update profile criteria not associated with the assigned profile will be ignored. Using any matching status values other than `match`, `nomatch`, or `unknown` will result in an error message. See [Error Codes &amp; Messages](../error-codes-messages) for details.

<a name="14833-updating-prospect-account-matching-statuses" id="updating-prospect-account-matching-statuses"></a>

## [](#updating-prospect-account-associations-)Updating Prospect Account Associations

To modify a prospect's matching status for associated prospect account, the Pardot ID of the prospect account is required. Once the ID is obtained, an `update` is submitted with parameters formatted as `prospect_account_id=<id>`.

_**Example:** Setting a prospect account for a prospect whose email address is_ `bob@pardot.com` _to_ `match`: /api/prospect/version/3/do/update/email/[bob@pardot.com](mailto:bob@pardot.com)?prospect_account_id=&amp;api_key=&amp;user_key=

A prospect account with the id must exist, and can not be set if a CRM connector is set up in the account.

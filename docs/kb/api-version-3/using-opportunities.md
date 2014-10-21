# API (version 3) - Using Opportunities


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="14772-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in Opportunities operations, see the [Opportunity](../object-field-references#opportunity) section of [Object Field References](../object-field-references).

**_Note:_** If a salesforce.com or SugarCRM connector is present in the API user's account, Opportunities can be read, but they cannot be modified (created, updated, deleted or undeleted).


| **Operation** | **URL Format**   | **Required Parameters** | **Description**  |
| ------------- | ---------------- | ----------------------- | -----------------|
| `create`      | `/api/opportunity /version/3/do/create /prospect_email /**__**?...` | `user_key, api_key, prospect_email, name, value, probability` | Creates a new opportunity using the specified data. `prospect_email` must correspond to an existing prospect. `name`, `value`, and `probability` must also be specified. See [Opportunity](../object-field-references#opportunity) in [Object Field References](../object-field-references) for other field requirements. **_Note:_** If both `prospect_email` and `prospect_id` are specified, both must correspond to the same prospect. Otherwise, the API will return an error. |
| `create`      | `/api/opportunity /version/3/do/create /prospect_id /**__**?...` | `user_key, api_key, prospect_id, name, value, probability` | Creates a new opportunity using the specified data. `prospect_id` must correspond to an existing prospect. `name`, `value`, and `probability` must also be specified. See [Opportunity](../object-field-references#opportunity) in [Object Field References](../object-field-references) for other field requirements. **_Note:_** If both `prospect_email` and `prospect_id` are specified, both must correspond to the same prospect. Otherwise, the API will return an error. |
| `read`        | `/api/opportunity /version/3/do/read /id/**__**?...` | `user_key, api_key, id` | Returns the data for the opportunity specified by `id`, including campaign assignment and associated visitor activities. `id` is the Pardot ID for the target opportunity. |
| `update`   | `/api/opportunity /version/3/do/update /id/**__**?...`   | `user_key, api_key, id` | Updates the provided data for the opportunity specified by `id`. `id` is the Pardot ID for the target opportunity. Fields that are not updated by the request remain unchanged. Returns an updated version of the opportunity. |
| `delete`   | `/api/opportunity /version/3/do/delete /id/**__**?...`   | `user_key, api_key, id` | Deletes the opportunity specified by `id`. `id` is the Pardot ID for the target opportunity. Returns no response on success. **_Note:_** Deleting an opportunity, whether via the API or within Pardot, will not delete the Visitor Activities or Score changes for the Prospect to whom the Opportunity is linked.
| `undelete` | `/api/opportunity /version/3/do/undelete /id/**__**?...` | `user_key, api_key, id` | Undeletes the opportunity specified by `id`. `id` is the Pardot ID for the target opportunity. Returns no response on success. |

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
| `<opportunity>`            | Parent tag. Contains data fields for target opportunity. Forcomplete field listing, see [Opportunity](../object-field-references#opportunity) in [Object Field References](../object-field-references). |
| `<campaign>`               | Contains `<id>` and `<name>` of the campaign to which this opportunity has been assigned. |
| `<prospects>`              | Contains all prospects associated with this opportunity. Contains only `<prospect>` tags. |
| `<opportunity_activities>` | Contains all visitor activities associated with this opportunity. Contains only `<visitor_activity>` tags. |
| `<visitor_activity>`       | Contains data fields for a visitor activity. For complete field listing, see [Visitor Activity](../object-field-references#visitor-activity) in [Object Field References](../object-field-references). |

<a name="14772-updating-field-values" id="updating-field-values"></a>

## [](#updating-field-values-)Updating Field Values

Modifying values of opportunity data fields is done by submitting an `update` request with parameters for each field to be updated. Each parameter is formatted as `<field_name>=<value>`.

**_Example:_** _Updating the value of a opportunity (whose Pardot ID is 27):_

```
POST: /api/opportunity/version/3/do/update/id/27 message body: value=50000&amp;api_key=&amp;user_key=

GET: /api/opportunity/version/3/do/update/id/27?value=50000&api_key=<api_key>&user_key=<user_key>
```

Only values that are specifically named in the request are updated. All others are left unchanged. To clear a value, submit an `update` request containing a parameter with no specified value, such as `status=`.


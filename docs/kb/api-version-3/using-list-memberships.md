# Using List Memberships


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="85559-supported-operations" id="supported-operations"></a>

List Membership can be controlled on a Prospect and List basis. In additon, the membership can reflect the opted "in" or opted "out" status for that Prospect and List combination. For a complete list of fields involved in list membership operations, see the [ListMembership](../object-field-references#list-membership) section of [Object Field References](../object-field-references).

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
| `<list_membership>` | Parent tag. Contains data fields for target list. For complete field listing, see [List Membership](../object-field-references#list-membership) in [Object Field References](../object-field-references). |


# Using Prospect Accounts


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="70888-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [Prospect Account](../object-field-references#prospectAccount) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------
| `create` | `/api/prospectAccount/version/3/do/create?...` | `user_key, api_key` | Create a new prospect account. |
| `describe` | `/api/prospectAccount/version/3/do/describe?...` | `user_key, api_key` | Returns the field metadata for prospect accounts, explaining what fields are available, their types, whether they are required, and their options (for dropdowns, radio buttons, etc) |
| `read` | `/api/prospectAccount/version/3/do/read/id/**_<id>_**?...` | `user_key, api_key, id` | Returns the data for the prospect account specified by `<id>`. `<id>` is the Pardot ID of the target prospect account. |
| `update` | `/api/prospectAccount/version/3/do/update/id/**_<id>_**?...` | `user_key, api_key, id` | Update the data for the prospect account specified by `<id>`. `<id>` is the Pardot ID of the target prospect account. |


## [](#xml-response-format-)XML Response Format

```
<rsp stat="ok" version="1.0">
    <prospectAccount>
        <id>1234</id>
        <name>Acme, Inc.</name>
        <created_at>2012-03-21 17:20:30</created_at>
        <updated_at>2012-05-15 09:57:11</updated_at>
    </prospectAccount>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<prospectAccount>` | Parent tag. Contains data fields for target prospect account. For complete field listing, see [Prospect Account](../object-field-references#prospectAccount) in [Object Field References](../object-field-references). |


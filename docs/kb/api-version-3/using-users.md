# Using Users


## Supported Operations<a name="14859-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [User](../object-field-references#user) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format** | **Required Parameters** | **Description** |
| ------------- | -------------- | ----------------------- | --------------- |
| `read` | `/api/user/version/3/do/read/email/**_<email>_**?...` | `user_key, api_key, id` | Returns the data for the user specified by `<email>`. `<email>` is the email address of the target user. |
| `read` | `/api/user/version/3/do/read/id/**_<id>_**?...` | `user_key, api_key, id` | Returns the data for the user specified by `<id>`. `<id>` is the Pardot ID of the target user. |

## XML Response Format

```
<rsp stat="ok" version="1.0">
    <user>
        ...
    </user>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<user>` | Parent tag. Contains data fields for target user. For complete field listing, see [User](../object-field-references#user) in [Object Field References](../object-field references). |


# Reading Emails


## Supported Operations<a name="71862-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [User](../object-field-references#email) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/email/version/3/do/read/id/**_<email id>_**?...` | `user_key, api_key, email` | Returns the data for the email specified by `<id>`. `<id>` is the Pardot ID of the target target email. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <email>
        ...
    </email>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<email>` | Parent tag. Contains data fields for target email. For complete field listing, see [email](../object-field-references#email) in [Object Field References](../object-field-references). |

# Using Visitor Activities


## Supported Operations<a name="25688-supported-operations"></a>

For a complete list of fields involved in visitor activity operations, see the [VisitorActivity](../object-field-references#visitor-activity) section of [Object Field References](object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/visitorActivity/version/3/do/read/id/**_<id>_**?...` | `user_key, api_key, id` | Returns the data for the visitor activity specified by `<id>`. is the Pardot ID for the target visitor activity. |

## XML Response Formats

```
<rsp stat="ok" version="1.0">
    <visitorActivity>
        ...
    </visitorActivity>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
`<visitorActivity>` | Parent tag. Contains data fields for target visitorActivity. For complete field listing, see [Visitor Activity](../object-field-references#visitor-activity) in [Object Field References](../object-field-references). |

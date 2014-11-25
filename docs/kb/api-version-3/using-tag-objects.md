
# Using TagObjects


## Supported Operations<a name="62780-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [tagObject](../object-field-references#tag-object) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/tagObject/version/3/do/read/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the tagObject specified by `<id>`. `<id>` is the Pardot ID of the target tagObject. |
| `removed` | `/api/tagObject/version/3/do/delete/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the tagObject specified by `<id>`. Returns the tagObject ID and date the tagObject was removed. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <tagObject>
        <id>53772</id>
        <tag_id>111</tag_id>
        <type>Prospect</type>
        <object_id>1</object_id>
        <created_at>2011-03-01 16:03:41</created_at>
    </tagObject>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<tagObject>` | Parent tag. Contains data fields for target tagObject. For complete field listing, see [TagObject](../object-field-references#tagObject) in [Object Field References](../object-field-references). |

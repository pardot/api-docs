
# Using Lists


## Supported Operations<a name="62780-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [List](../object-field-references#list) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/list/version/3/do/read/id/**_<id>_**?...` | `user_key, api_key, id` | Returns the data for the list specified by `<id>`. `<id>` is the Pardot ID of the target list. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <list>
        <id>2387</id>
        <name>Awesome Prospects</name>
        <is_public>true</is_public>
        <title>A longer title for this list</title>
        <description>For public lists, an optional description may be used to explain to the prospect why they might want to include this list in their subscription preferences.</description>
        <is_crm_visible>true</is_crm_visible>
        <created_at>2012-03-21 17:20:30</created_at>
        <updated_at>2012-05-15 09:57:11</updated_at>
    </list>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<list>` | Parent tag. Contains data fields for target list. For complete field listing, see [List](../object-field-references#list) in [Object Field References](../object-field-references). |

# Reading Files


## Supported Operations<a name="62780-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [File](../object-field-references#file) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/file/version/4/do/read/id/`**_`<id>`_**`?...` | `user_key, api_key, id` | Returns the data for the file specified by `<id>`. `<id>` is the Pardot ID of the target file. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <file>
      <id>43</id>
      <name>Pricing Guide - PDF</name>
      <created_at>2014-09-03 11:08:00</created_at>
      <updated_at>2014-09-03 11:08:00</updated_at>
   </file>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<file>`            | Parent tag. Contains data fields for the target file. For complete field listing, see [File](../object-field-references#file) in [Object Field References](../object-field-references). |
| `<campaign>` | Contains `<id>` and `<name>` of the campaign to which this file has been assigned. This leaf only appears if the file has been assigned to a campaign. |


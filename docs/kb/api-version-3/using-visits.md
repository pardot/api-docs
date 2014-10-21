# Using Visits


## Supported Operations<a name="14846-supported-operations"></a>

For a complete list of fields involved in visitor operations, see the [Visit](../object-field-references#visit) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**   | **Required Parameters** | **Description**  |
| ------------- | ---------------- | ----------------------- | -----------------|
| `read` | `/api/visit/version/3/do/read/id/**_<id>_**?...` | `user_key, api_key, id` | Returns the data for the visit specified by `<id>`, including associated visitor page views. `<id>` is the Pardot ID for the target visit. |

<a name="14846-xml-response-formats"></a>

## XML Response Formats

```
<rsp stat="ok" version="1.0">
    <visit>
        ...
        <visitor_page_views>
            <visitor_page_view>
                ...
            </visitor_page_view>
        </visitor_page_views>
    </visit>
</rsp>
```

| **Tag**                    | **Description** |
|----------------------------|-----------------|
| `<visit>` | Parent tag. Contains data fields for target visit.  For complete field listing, see [Visit](../object-field-references#visit) in [Object Field References](../object-field-references). |
| `<visitor_page_views>` | Contains all visitor page views associated with this visitor.  Contains only `<visitor_page_view>` tags. |
| `<visitor_page_view>` | Contains data fields for a visitor page view.  For complete field listing, see [Visitor Page View](../object-field-references#visitor-page-view) in [Object Field References](../object-field-references). |

# API (version 3) - Using Visitors


## Supported Operations<a name="20547-supported-operations"></a>

For a complete list of fields involved in visitor operations, see the [Visitor](../object-field-references#visitor) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**   | **Required Parameters** | **Description**  |
| ------------- | ---------------- | ----------------------- | -----------------|
| `assign` | `/api/visitor/version/3/do/assign/id/**_<id>_**?...` | `user_key, api_key, id, (prospect_email OR prospect_id)` | Assigns or reassigns the visitor specified by `<id>` to a specified prospect.  One (and only one) of the following parameters must be provided to identify the target prospect: `<prospect_email>` or `<prospect_id>`.  Returns an updated version of the visitor. |
| `read` | `/api/visitor/version/3/do/read/id/**_<id>_**?...` | `user_key, api_key, id` | Returns the data for the visitor specified by `<id>`, including associated visitor activities, identified company data, and visitor referrers. `<id>` is the Pardot ID for the target visitor. |

<a name="20547-xml-response-formats"></a>

## XML Response Formats

For `output=full`:

```
<rsp stat="ok" version="1.0">
    <visitor>
        ...
        <prospect>
            ...
        </prospect>
        <identified_company>
            ...
        </identified_company>
        <visitor_referrer>
            ...
        </visitor_referrer>
        <visitor_activities>
            <visitor_activity>
                ...
            </visitor_activity>
        </visitor_activities>
    </visitor>
</rsp>
```

For `output=simple`:

```
<rsp stat="ok" version="1.0">
    <visitor>
        ...
    </visitor>
</rsp>
```

For `output=mobile`:

```
<rsp stat="ok" version="1.0">
    <visitor>
        <id>...</id>
        <prospect_id>...</prospect_id>
        <page_view_count>...</page_view_count>
        <ip_address>...</ip_address>
        <hostname>...</hostname>
        <created_at>...</created_at>
        <updated_at>...</updated_at>
    </visitor>
</rsp>
```

| **Tag**                    | **Description** |
|----------------------------|-----------------|
| `<visitor>` | Parent tag. Contains data fields for target visitor.  For complete field listing, see [Visitor](../object-field-references#visitor) in [Object Field References](../object-field-references). |
| `<prospect>` | Contains data about the prospect to which this visitor is assigned.  The prospect's data is returned in `mobile` output format.  See [XML Response Formats](using-prospects#xml-response-formats) in [Using Prospects](using-prospects). |
| `<identified_company>` | Contains data about the identified company associated with this visitor.  This leaf only appears if an identified company is associated with this visitor.  See [Identified Company](../object-field-references#identified-company) in [Object Field References](../object-field-references). |
| `<visitor_referrer>` | Contains data about this visitor's referrer.  This leaf only appears if this visitor has an associated visitor referrer.  For complete field listing, see [Visitor Referrer](../object-field-references#visitor-referrer) in [Object Field References](../object-field-references). |
| `<visitor_activities>` | Contains all visitor activities associated with this visitor.  Contains only `<visitor_activity>` tags. |
| `<visitor_activity>` | Contains data fields for a visitor activity.  For complete field listing, see [Visitor Activity](../object-field-references#visitor-activity) in [Object Field References](../object-field-references). |

<a name="20547-assigning-and-reassigning-visitors"></a>

## Assigning and Reassigning Visitors

To assign/reassign a visitor, both the visitor to be assigned and the target prospect of the assignment must be defined.  Visitors are specified by their Pardot ID.  Prospects can be specified by their Pardot user ID or by their email address.  Possible combinations of parameters are shown below.  Developers are responsible for substituting specific values for parameters denoted by `<carets>`.

**_Examples:_**

```
/api/visitor/version/3/do/assign/id/<visitor_id>?prospect_email=<prospect_email>&api_key=<api_key>&user_key=<user_key>
/api/visitor/version/3/do/assign/id/<visitor_id>?prospect_id=<prospect_id>&api_key=<api_key>&user_key=<user_key>
```

XML responses to `assign` requests are identical to `read` requests, but reflect the new visitor assignment in the `<prospect>` node.


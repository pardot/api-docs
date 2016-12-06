
# Querying Accounts


## Supported Operations<a name="71862-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/account/version/4/do/read` | `user_key, api_key` | Returns the data for the account of the currently logged in user. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <account>
        <id>1</id>
        <company>Company Name</company>
        <level>Pardot Account Level</level>
        <website>http://www.company-website.com</website>
        <vanity_domain>http://go.localhost.com</vanity_domain>
        <plugin_campaign_id>1</plugin_campaign_id>
        <tracking_code_template>[... Tracking code template ...]</tracking_code_template>
        <address1>1234 Any Streep</address1>
        <address2>Suite 9876</address2>
        <city>Atlanta</city>
        <state>Georgia</state>
        <territory/>
        <zip>30326</zip>
        <country>United States</country>
        <phone>555-555-5555</phone>
        <fax/>
        <created_at>2008-03-26 09:42:51</created_at>
        <updated_at>2016-11-10 15:06:33</updated_at>
    </account>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<account>` | Parent tag. Contains data fields for current account.|

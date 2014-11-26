# Reading Email Templates


## Supported Operations<a name="71862-supported-operations" id="supported-operations"></a>


| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/emailTemplate/version/3/do/read/id/<email template id>` | `user_key, api_key, emailTemplateId` | Returns the data for the email template specified by `<id>`. `<id>` is the Pardot ID of the target email template. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <emailTemplate>
        <error></error>
        <errorCode></errorCode>
        <errorMessage></errorMessage>
    </emailTemplate>
    --- or ---
    <emailTemplate>
        <error></error>
        <sendOptions>
            <replyToAddress></replyToAddress>
            <sendFromData></sendFromData>
        </sendOptions>
        <id></id>
        <name></name>
        <htmlMessage></htmlMessage>
        <textMessage></textMessage>
        <isDripEmail></isDripEmail>
        <isListEmail></isListEmail>
        <subject></subject>
    </emailTemplate>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<emailTemplate>` | Parent tag. Contains data fields for target email template. |
| `<error>` | Flag if an error occurred. |
| `<errorCode>` | Code for the error which occurred. |
| `<errorMessage>` | The error description. |
| `<sendOptions>` | The associated send options object. Contains sender specific data. |
| `<replyToAddress>` | The email address set for the email's Reply-To header. |
| `<sendFromData>` | A JSON array representing the sender hierarchy tied to the email template. |
| `<id>` | The Pardot ID of the email template. |
| `<name>` | The name of the email template. |
| `<htmlMessage>` | The HTML version of the email template body. |
| `<textMessage>` | The plain text version of the email template body. |
| `<isDripEmail>` | Flag if the template is available for use in drip programs. |
| `<isListEmail>` | Flag if the template is available for use in list emails. |
| `<subject>` | The subject of the email message. |

# List One to One Email Templates

## Supported Operations<a name="71862-supported-operations" id="supported-operations"></a>

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `listOneToOne` | `/api/emailTemplate/version/3/do/listOneToOne` | `user_key, api_key` | `Returns a list of email templates which are enabled for use in one to one emails.` |

## XML Response Format

```
<rsp stat="ok" version="1.0">
    <emailTemplates>
        <templates>
            <id></id>
            <name></name>
            <isOneToOneEmail></isOneToOneEmail>
            <isArchived></isArchived>
            <isAutoResponderEmail></isAutoResponderEmail>
            <isDripEmail></isDripEmail>
            <isListEmail></isListEmail>
            <subject></subject>
        </templates>
        <templates>...</templates>
        <templates>...</templates>
    </emailTemplates>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<emailTemplates>` | Parent tag. Contains individual email template records. |
| `<templates>` | Individual template parent tag. |
| `<id>` | The Pardot ID of the email template. |
| `<name>` | The name of the email template. |
| `<isOneToOneEmail>` | Flag if the email template is available for use in one to one emails (always true). |
| `<isArchived>` | Flag if the email template is currently in the Recycle Bin in Pardot. |
| `<isAutoResponderEmail>` | Flag if the email template is available for use as an auto response from a form submission. |
| `<isDripEmail>` | Flag if the email template is available for use in a drip program. |
| `<isListEmail>` | Flag if the email template is available for use in a list email. |
| `<subject>` | The subject of the email message. |
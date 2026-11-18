# ![salesforce update sink](_images/kamelets/salesforce-update-sink.svg) Salesforce Update Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Changes fields of an existing Salesforce record, such as the phone number of a contact, for each message; the message names the record and the new values.

Use it to keep Salesforce records in step with another system, for example to update the address of an account when it changes in the ERP. To create records use `salesforce-create-sink`, and to create or update many records matched by an external ID, `salesforce-composite-upsert-sink`.

Input: the body is JSON text with three fields: `sObjectName`, the API name of the kind of record (such as `Contact`); `sObjectId`, the ID of the record; and `payload`, an object with the fields to change and their new values. For example `{"sObjectName": "Contact", "sObjectId": "003XXXXXXXXXXXXXXX", "payload": {"Phone": "+45 1234 5678"}}`. The fields that are not in `payload` keep their values.

Output: when it is used inside a route, the body afterwards is the `payload` as JSON text.

Good to know: a message without `sObjectName` or `sObjectId`, for a record that does not exist, or with a change that Salesforce refuses, fails. The message decides which record is changed, so place this sink only after a source you trust.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-update-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The consumer key of the connected app that the Kamelet logs in through. In Salesforce Setup, open App Manager, choose View on the app, then Manage Consumer Details. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The consumer secret of the same connected app, shown next to the consumer key under Manage Consumer Details. | string |  |  |
| **authenticationType** | Authentication Type | How the Kamelet logs in. `USERNAME_PASSWORD` needs `userName` and `password`; `CLIENT_CREDENTIALS` needs only the consumer key and secret, and a run-as user set for the client credentials flow in the connected app; `REFRESH_TOKEN` needs `refreshToken`; `JWT` needs `userName`, `keystore` and `jwtAudience`. Enum values: \* USERNAME\_PASSWORD \* CLIENT\_CREDENTIALS \* REFRESH\_TOKEN \* JWT | string | USERNAME\_PASSWORD |  |
| **instanceUrl** | Instance URL | The address of your org, such as `[https://mycompany.my.salesforce.com](https://mycompany.my.salesforce.com)`. Only needed when the answer to the login does not give it. | string |  | https://myinstance.my.salesforce.com |
| **jwtAudience** | JWT Audience | The audience of the JWT that the Kamelet signs to log in: `[https://login.salesforce.com](https://login.salesforce.com)` for a production org, or `[https://test.salesforce.com](https://test.salesforce.com)` for a sandbox. Only used by `JWT`. | string |  | https://login.salesforce.com |
| **keystore** | Keystore | A reference to a bean of type `org.apache.camel.support.jsse.KeyStoreParameters`, written as `#bean:` and the name of the bean, holding the private key that signs the JWT. Its certificate must be uploaded to the connected app, under Use Digital Signatures. Only used by `JWT`. | string |  | #bean:myKeystore |
| **loginUrl** | Login URL | The address the Kamelet logs in to. Keep the default for a production org, use `[https://test.salesforce.com](https://test.salesforce.com)` for a sandbox, or the My Domain address of your org. | string | [https://login.salesforce.com](https://login.salesforce.com) | https://test.salesforce.com |
| **password** | Password | The password of `userName`. When Salesforce asks for a security token, such as from outside the trusted IP ranges of the org, add the token of the user at the end of the password; the user gets a new one from Reset My Security Token in their personal settings. Only used by `USERNAME_PASSWORD`. | string |  |  |
| **refreshToken** | Refresh Token | A refresh token of the connected app for the user to act as, obtained once through an OAuth login in a browser with the `refresh_token` scope. Only used by `REFRESH_TOKEN`. | string |  |  |
| **userName** | Username | The user name of the Salesforce user to log in as, which looks like an email address. Used by the `USERNAME_PASSWORD` and `JWT` authentication types. | string |  |  |

## Dependencies

At runtime, the `salesforce-update-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jsonpath
    
-   camel:jackson3
    
-   camel:salesforce
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:salesforce-update-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Salesforce Update Sink Kamelet Description

### Salesforce CRM Integration

This Kamelet integrates with Salesforce CRM to update existing records. It provides record modification through Salesforce’s REST API.

### Record Updates

Each message names the record to update and the new values, as JSON text:

```json
{
  "sObjectName": "Contact",
  "sObjectId": "003XXXXXXXXXXXXXXX",
  "payload": {
    "Phone": "+45 1234 5678"
  }
}
```

-   `sObjectName`: the API name of the kind of record
    
-   `sObjectId`: the Salesforce ID of the record
    
-   `payload`: the fields to change, by their API names, with their new values
    

### Field-Level Updates

Only the fields in `payload` are changed; the other fields of the record keep their values.

### Validation and Workflow

Updated records are subject to Salesforce’s validation rules, workflow rules, and triggers. A change that Salesforce refuses fails the message.

### API Authentication

The Kamelet logs in through a connected app of your org. Create one in Salesforce Setup, under App Manager, with OAuth enabled, and copy its consumer key and secret into `clientId` and `clientSecret`. `authenticationType` chooses how the Kamelet logs in, and which other options it needs.

### Audit Trail

Salesforce maintains audit trails for record updates, including:

-   Field history tracking
    
-   User identification
    
-   Timestamp information
    
-   Before and after values
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-update-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-update-sink.kamelet.yaml)
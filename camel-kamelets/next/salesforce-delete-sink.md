# ![salesforce delete sink](_images/kamelets/salesforce-delete-sink.svg) Salesforce Delete Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Deletes the Salesforce record that each message names by its ID, such as a contact or an account.

Use it to remove records from Salesforce when they are removed in another system, for example to delete a contact when a customer closes their account.

Input: the body is JSON text with two fields: `sObjectName`, the API name of the kind of record (such as `Contact`), and `sObjectId`, the ID of the record. For example `{"sObjectName": "Contact", "sObjectId": "003XXXXXXXXXXXXXXX"}`. Other fields are ignored.

Output: when it is used inside a route, the body afterwards is empty.

Good to know: Salesforce moves the deleted record to its Recycle Bin. A message without `sObjectName` or `sObjectId`, or for a record that does not exist, fails. The message decides which record is deleted, so place this sink only after a source you trust.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-delete-sink` Kamelet:

     
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

At runtime, the `salesforce-delete-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:salesforce
    
-   camel:kamelet
    
-   camel:jsonpath
    

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
            uri: "kamelet:salesforce-delete-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Salesforce Delete Sink Kamelet Description

### Salesforce CRM Integration

This Kamelet integrates with Salesforce CRM to delete records. It provides record deletion through Salesforce’s REST API.

### Record Deletion

Each message names the record to delete, as JSON text:

```json
{
  "sObjectName": "Contact",
  "sObjectId": "003XXXXXXXXXXXXXXX"
}
```

-   `sObjectName`: the API name of the kind of record
    
-   `sObjectId`: the Salesforce ID of the record
    

Because the message decides which record is deleted, place this Kamelet only after a source you trust.

### Safety and Recovery

Salesforce provides safety mechanisms for deleted records:

-   Deleted records are moved to the Recycle Bin
    
-   Records can be restored within the retention period
    
-   Audit trails maintain deletion history
    

### Cascade Effects

Salesforce’s cascade deletion rules apply: deleting a record can also delete related records, as the relationships of your org define.

### API Authentication

The Kamelet logs in through a connected app of your org. Create one in Salesforce Setup, under App Manager, with OAuth enabled, and copy its consumer key and secret into `clientId` and `clientSecret`. `authenticationType` chooses how the Kamelet logs in, and which other options it needs.

### Permission Controls

Respects Salesforce’s object-level security settings: the user the Kamelet logs in as must be allowed to delete the records.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-delete-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-delete-sink.kamelet.yaml)
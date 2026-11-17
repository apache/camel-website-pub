# ![salesforce source](_images/kamelets/salesforce-source.svg) Salesforce Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives an event each time a Salesforce record that matches a SOQL query is created, updated, deleted or undeleted, through a PushTopic of the Streaming API.

Use it to react to changes in Salesforce, for example to copy each new contact to a mailing tool or to alert a team when an opportunity is won. For Platform Events and Change Data Capture through the newer Pub/Sub API, use `salesforce-pubsub-source`.

Output: the body is the record as JSON text, with the fields that the query selects. The `CamelSalesforceEventType` header says what happened: `created`, `updated`, `deleted` or `undeleted`. The `CamelSalesforceReplayId` header identifies the event.

Good to know: when it starts, it creates the PushTopic `topicName` in Salesforce with `query` and the notify options, or updates it when it exists, so the user needs the permission to create PushTopics. By default only new records send an event; turn on `notifyForOperationUpdate` and the others for more. Only the events after the start are received, unless `replayId` is set.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The consumer key of the connected app that the Kamelet logs in through. In Salesforce Setup, open App Manager, choose View on the app, then Manage Consumer Details. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The consumer secret of the same connected app, shown next to the consumer key under Manage Consumer Details. | string |  |  |
| **query** | Query | **Required** The SOQL query of the PushTopic. It chooses the kind of record, the fields to send, and with an optional `WHERE` the records to watch. It must select `Id`. | string |  | SELECT Id, Name, Email, Phone FROM Contact |
| **topicName** | Topic Name | **Required** The name of the PushTopic that the Kamelet creates or updates in Salesforce with `query`, and listens to. | string |  | ContactTopic |
| **authenticationType** | Authentication Type | How the Kamelet logs in. `USERNAME_PASSWORD` needs `userName` and `password`; `CLIENT_CREDENTIALS` needs only the consumer key and secret, and a run-as user set for the client credentials flow in the connected app; `REFRESH_TOKEN` needs `refreshToken`; `JWT` needs `userName`, `keystore` and `jwtAudience`. Enum values: \* USERNAME\_PASSWORD \* CLIENT\_CREDENTIALS \* REFRESH\_TOKEN \* JWT | string | USERNAME\_PASSWORD |  |
| **instanceUrl** | Instance URL | The address of your org, such as `[https://mycompany.my.salesforce.com](https://mycompany.my.salesforce.com)`. Only needed when the answer to the login does not give it. | string |  | https://myinstance.my.salesforce.com |
| **jwtAudience** | JWT Audience | The audience of the JWT that the Kamelet signs to log in: `[https://login.salesforce.com](https://login.salesforce.com)` for a production org, or `[https://test.salesforce.com](https://test.salesforce.com)` for a sandbox. Only used by `JWT`. | string |  | https://login.salesforce.com |
| **keystore** | Keystore | A reference to a bean of type `org.apache.camel.support.jsse.KeyStoreParameters`, written as `#bean:` and the name of the bean, holding the private key that signs the JWT. Its certificate must be uploaded to the connected app, under Use Digital Signatures. Only used by `JWT`. | string |  | #bean:myKeystore |
| **loginUrl** | Login URL | The address the Kamelet logs in to. Keep the default for a production org, use `[https://test.salesforce.com](https://test.salesforce.com)` for a sandbox, or the My Domain address of your org. | string | [https://login.salesforce.com](https://login.salesforce.com) | https://test.salesforce.com |
| **notifyForFields** | Notify For Fields | Which changed fields make an update send an event: `ALL` any field, `REFERENCED` a field of the `SELECT` or the `WHERE` of `query`, `SELECT` a field of the `SELECT`, `WHERE` a field of the `WHERE`. Enum values: \* ALL \* REFERENCED \* SELECT \* WHERE | string | ALL |  |
| **notifyForOperationCreate** | Notify Operation Create | If true, an event is sent when a record that matches `query` is created. | boolean | true |  |
| **notifyForOperationDelete** | Notify Operation Delete | If true, an event is sent when a record that matches `query` is deleted. | boolean | false |  |
| **notifyForOperationUndelete** | Notify Operation Undelete | If true, an event is sent when a deleted record that matches `query` is restored from the Recycle Bin. | boolean | false |  |
| **notifyForOperationUpdate** | Notify Operation Update | If true, an event is sent when a record that matches `query` is updated; `notifyForFields` says which fields count. | boolean | false |  |
| **operation** | Operation | The kind of subscription of the Salesforce component. Leave it as `subscribe`, the only one that works with the other options of this Kamelet. | string | subscribe |  |
| **password** | Password | The password of `userName`. When Salesforce asks for a security token, such as from outside the trusted IP ranges of the org, add the token of the user at the end of the password; the user gets a new one from Reset My Security Token in their personal settings. Only used by `USERNAME_PASSWORD`. | string |  |  |
| **rawPayload** | Raw Payload | If true, the record is passed on as the JSON text that Salesforce sent, instead of being read and written again. The body is JSON text either way. | boolean | false |  |
| **refreshToken** | Refresh Token | A refresh token of the connected app for the user to act as, obtained once through an OAuth login in a browser with the `refresh_token` scope. Only used by `REFRESH_TOKEN`. | string |  |  |
| **replayId** | Replay Id | Where to start: `-1` for only the events after the start, as when it is not set; `-2` for all the events that Salesforce still keeps; or the replay ID of an event, from its `CamelSalesforceReplayId` header, for the events after it. | long |  |  |
| **userName** | Username | The user name of the Salesforce user to log in as, which looks like an email address. Used by the `USERNAME_PASSWORD` and `JWT` authentication types. | string |  |  |

## Dependencies

At runtime, the `salesforce-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
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
      uri: "kamelet:salesforce-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Salesforce Source Kamelet Description

### Authentication

This Kamelet logs in through a connected app of your org. You need to create a connected app in Salesforce and obtain its consumer key and consumer secret. `authenticationType` chooses how the Kamelet logs in: by default with `userName` and `password`.

### How It Works

The Kamelet uses a PushTopic of the Salesforce Streaming API. When it starts, it creates the PushTopic named `topicName` with the SOQL `query` and the notify options, or updates it when it already exists. Salesforce then sends an event each time a record that matches the query is created, updated, deleted or undeleted, as the notify options choose. By default only new records send an event.

### Configuration

The Salesforce Source Kamelet supports the following configurations:

-   **Consumer Key** (`clientId`) and **Consumer Secret** (`clientSecret`): of the connected app (required)
    
-   **Username** (`userName`) and **Password** (`password`): the user to log in as, for the default authentication type
    
-   **Login URL** (`loginUrl`): Salesforce login URL (default: [https://login.salesforce.com](https://login.salesforce.com))
    
-   **Query** (`query`): the SOQL query of the PushTopic, which must select `Id` (required)
    
-   **Topic Name** (`topicName`): the name of the PushTopic (required)
    
-   **Notify options**: which operations (`notifyForOperationCreate`, `notifyForOperationUpdate`, …​) and which fields (`notifyForFields`) send an event
    

### Output Format

The Kamelet outputs each record as JSON text, with the fields that the query selects. The `CamelSalesforceEventType` header says what happened to the record: `created`, `updated`, `deleted` or `undeleted`.

### Setup Requirements

1.  Create a Connected App in Salesforce Setup
    
2.  Configure OAuth settings and permissions
    
3.  Obtain the consumer key and consumer secret
    
4.  Generate or obtain the security token of the user, when needed
    
5.  Ensure the user has API access and the permission to create PushTopics
    

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:salesforce-source"
      parameters:
        clientId: "{{salesforce.clientId}}"
        clientSecret: "{{salesforce.clientSecret}}"
        userName: "salesforce-user@example.com"
        password: "{{salesforce.passwordAndToken}}"
        topicName: "TechAccounts"
        query: "SELECT Id, Name, Industry FROM Account WHERE Industry = 'Technology'"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Custom Login URL and Updates

```yaml
- route:
    from:
      uri: "kamelet:salesforce-source"
      parameters:
        clientId: "{{salesforce.clientId}}"
        clientSecret: "{{salesforce.clientSecret}}"
        userName: "salesforce-user@example.com"
        password: "{{salesforce.passwordAndToken}}"
        loginUrl: "https://test.salesforce.com"
        topicName: "ContactChanges"
        query: "SELECT Id, FirstName, LastName, Email FROM Contact"
        notifyForOperationUpdate: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### SOQL Query Examples

-   Simple selection: `SELECT Id, Name FROM Account`
    
-   With conditions: `SELECT Id, Name FROM Account WHERE Industry = 'Technology'`
    

### Security Considerations

-   Store credentials securely using secrets management
    
-   Use IP restrictions in Connected App settings
    
-   Rotate client secrets periodically
    
-   Monitor API usage to stay within limits
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-source.kamelet.yaml)
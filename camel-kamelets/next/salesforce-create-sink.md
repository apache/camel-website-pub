# ![salesforce create sink](_images/kamelets/salesforce-create-sink.svg) Salesforce Create Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Creates a new record, such as a contact, an account or a lead, in Salesforce for each message.

Use it to add to Salesforce what happens in other systems, for example a contact for each web form sent or a lead from a marketing tool. To change existing records use `salesforce-update-sink`, and to create or update many records at once, matched by an external ID, `salesforce-composite-upsert-sink`.

Input: the body is the fields of the new record as JSON text, with the API names of the fields, such as `{"LastName": "Lovelace", "Email": "[ada@example.com](mailto:ada@example.com)"}`. It is sent to Salesforce as it is. The kind of record comes from `sObjectName`.

Output: when it is used inside a route, the body afterwards is the answer of Salesforce as JSON text, with the `id` of the new record, `success` and `errors`.

Good to know: a record that Salesforce refuses, for example because a required field is missing or a validation rule fails, fails the message. `sObjectName` must be set, or the Kamelet does not start.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-create-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The consumer key of the connected app that the Kamelet logs in through. In Salesforce Setup, open App Manager, choose View on the app, then Manage Consumer Details. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The consumer secret of the same connected app, shown next to the consumer key under Manage Consumer Details. | string |  |  |
| **sObjectName** | Object Name | **Required** The API name of the kind of record to create, such as `Contact`, `Account` or `Lead`, or a custom object such as `Invoice__c`. It must be set, or the Kamelet does not start. | string |  | Contact |
| **authenticationType** | Authentication Type | How the Kamelet logs in. `USERNAME_PASSWORD` needs `userName` and `password`; `CLIENT_CREDENTIALS` needs only the consumer key and secret, and a run-as user set for the client credentials flow in the connected app; `REFRESH_TOKEN` needs `refreshToken`; `JWT` needs `userName`, `keystore` and `jwtAudience`. Enum values: \* USERNAME\_PASSWORD \* CLIENT\_CREDENTIALS \* REFRESH\_TOKEN \* JWT | string | USERNAME\_PASSWORD |  |
| **instanceUrl** | Instance URL | The address of your org, such as `[https://mycompany.my.salesforce.com](https://mycompany.my.salesforce.com)`. Only needed when the answer to the login does not give it. | string |  | https://myinstance.my.salesforce.com |
| **jwtAudience** | JWT Audience | The audience of the JWT that the Kamelet signs to log in: `[https://login.salesforce.com](https://login.salesforce.com)` for a production org, or `[https://test.salesforce.com](https://test.salesforce.com)` for a sandbox. Only used by `JWT`. | string |  | https://login.salesforce.com |
| **keystore** | Keystore | A reference to a bean of type `org.apache.camel.support.jsse.KeyStoreParameters`, written as `#bean:` and the name of the bean, holding the private key that signs the JWT. Its certificate must be uploaded to the connected app, under Use Digital Signatures. Only used by `JWT`. | string |  | #bean:myKeystore |
| **loginUrl** | Login URL | The address the Kamelet logs in to. Keep the default for a production org, use `[https://test.salesforce.com](https://test.salesforce.com)` for a sandbox, or the My Domain address of your org. | string | [https://login.salesforce.com](https://login.salesforce.com) | https://test.salesforce.com |
| **password** | Password | The password of `userName`. When Salesforce asks for a security token, such as from outside the trusted IP ranges of the org, add the token of the user at the end of the password; the user gets a new one from Reset My Security Token in their personal settings. Only used by `USERNAME_PASSWORD`. | string |  |  |
| **refreshToken** | Refresh Token | A refresh token of the connected app for the user to act as, obtained once through an OAuth login in a browser with the `refresh_token` scope. Only used by `REFRESH_TOKEN`. | string |  |  |
| **userName** | Username | The user name of the Salesforce user to log in as, which looks like an email address. Used by the `USERNAME_PASSWORD` and `JWT` authentication types. | string |  |  |

## Dependencies

At runtime, the `salesforce-create-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:salesforce-create-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Salesforce Create Sink Kamelet Description

### Salesforce CRM Integration

This Kamelet integrates with Salesforce CRM to create a new record for each message. It provides direct integration with Salesforce’s REST API for record creation operations.

### Object Flexibility

The `sObjectName` option names the kind of record to create, by its API name. It supports any Salesforce object, including:

-   Standard objects (`Account`, `Contact`, `Lead`, etc.)
    
-   Custom objects specific to your organization, such as `Invoice__c`
    
-   Junction objects for many-to-many relationships
    

### Field Mapping

The body is the fields of the new record as JSON text, with the API names of the fields. It is sent to Salesforce as it is, so turn the data of other systems into these names before this Kamelet.

### API Authentication

The Kamelet logs in through a connected app of your org. Create one in Salesforce Setup, under App Manager, with OAuth enabled, and copy its consumer key and secret into `clientId` and `clientSecret`. `authenticationType` chooses how the Kamelet logs in, and which other options it needs.

### Data Validation

Salesforce’s validation rules, field requirements, and business logic apply to the new records. A record that Salesforce refuses fails the message.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: '{"LastName": "Lovelace", "Email": "ada@example.com"}'
        contentType: application/json
        repeatCount: 1
      steps:
        - to:
            uri: "kamelet:salesforce-create-sink"
            parameters:
              sObjectName: Contact
              clientId: "{{salesforce.clientId}}"
              clientSecret: "{{salesforce.clientSecret}}"
              userName: "{{salesforce.userName}}"
              password: "{{salesforce.password}}"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-create-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-create-sink.kamelet.yaml)
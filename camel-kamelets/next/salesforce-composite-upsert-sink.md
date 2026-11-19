# ![salesforce composite upsert sink](_images/kamelets/salesforce-composite-upsert-sink.svg) Salesforce composite upsert Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Creates or updates many Salesforce records of one kind in a single call, matching each record to an existing one by an external ID field.

Use it to copy a batch of customers, products or orders from another system into Salesforce without creating duplicates: a record whose external ID is already in Salesforce is updated, the others are created. To create or change one record at a time, use `salesforce-create-sink` or `salesforce-update-sink`.

Input: the body is JSON text with a `records` list. Each record gives its kind in `attributes`, such as `{"attributes": {"type": "Contact"}, "External_Id__c": "C-1", "LastName": "Lovelace"}`, and holds the external ID field named by `sObjectIdName` with its value, and the fields to set. Salesforce accepts up to 200 records in one call.

Output: when it is used inside a route, the body afterwards is a List with one result per record, in the same order, each with `id`, `success`, `created` (true for a new record) and `errors`.

Good to know: a record that Salesforce refuses does not fail the message, and the other records are still saved: check `success` in the results. Headers that start with `CamelSalesforce` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-composite-upsert-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The consumer key of the connected app that the Kamelet logs in through. In Salesforce Setup, open App Manager, choose View on the app, then Manage Consumer Details. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The consumer secret of the same connected app, shown next to the consumer key under Manage Consumer Details. | string |  |  |
| **sObjectIdName** | External ID Field | **Required** The API name of the field that matches each record to an existing one, such as `External_Id__c`. In Salesforce the field must be marked as External ID. | string |  | External\_Id\_\_c |
| **sObjectName** | Object Name | **Required** The API name of the kind of the records, such as `Contact`, `Account` or `Product2`, or a custom object such as `Invoice__c`. All the records of a message are of this kind. | string |  | Contact |
| **authenticationType** | Authentication Type | How the Kamelet logs in. `USERNAME_PASSWORD` needs `userName` and `password`; `CLIENT_CREDENTIALS` needs only the consumer key and secret, and a run-as user set for the client credentials flow in the connected app; `REFRESH_TOKEN` needs `refreshToken`; `JWT` needs `userName`, `keystore` and `jwtAudience`. Enum values: \* USERNAME\_PASSWORD \* CLIENT\_CREDENTIALS \* REFRESH\_TOKEN \* JWT | string | USERNAME\_PASSWORD |  |
| **instanceUrl** | Instance URL | The address of your org, such as `[https://mycompany.my.salesforce.com](https://mycompany.my.salesforce.com)`. Only needed when the answer to the login does not give it. | string |  | https://myinstance.my.salesforce.com |
| **jwtAudience** | JWT Audience | The audience of the JWT that the Kamelet signs to log in: `[https://login.salesforce.com](https://login.salesforce.com)` for a production org, or `[https://test.salesforce.com](https://test.salesforce.com)` for a sandbox. Only used by `JWT`. | string |  | https://login.salesforce.com |
| **keystore** | Keystore | A reference to a bean of type `org.apache.camel.support.jsse.KeyStoreParameters`, written as `#bean:` and the name of the bean, holding the private key that signs the JWT. Its certificate must be uploaded to the connected app, under Use Digital Signatures. Only used by `JWT`. | string |  | #bean:myKeystore |
| **loginUrl** | Login URL | The address the Kamelet logs in to. Keep the default for a production org, use `[https://test.salesforce.com](https://test.salesforce.com)` for a sandbox, or the My Domain address of your org. | string | [https://login.salesforce.com](https://login.salesforce.com) | https://test.salesforce.com |
| **password** | Password | The password of `userName`. When Salesforce asks for a security token, such as from outside the trusted IP ranges of the org, add the token of the user at the end of the password; the user gets a new one from Reset My Security Token in their personal settings. Only used by `USERNAME_PASSWORD`. | string |  |  |
| **refreshToken** | Refresh Token | A refresh token of the connected app for the user to act as, obtained once through an OAuth login in a browser with the `refresh_token` scope. Only used by `REFRESH_TOKEN`. | string |  |  |
| **userName** | Username | The user name of the Salesforce user to log in as, which looks like an email address. Used by the `USERNAME_PASSWORD` and `JWT` authentication types. | string |  |  |

## Dependencies

At runtime, the `salesforce-composite-upsert-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:salesforce-composite-upsert-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Salesforce Composite Upsert Sink Kamelet Description

### Salesforce CRM Integration

This Kamelet integrates with Salesforce CRM using the composite upsert operation of the sObject Collections API. Several records are processed in a single API call, which reduces API usage.

### Upsert Operations

Performs upsert (insert or update) operations: a record whose external ID is already in Salesforce is updated, and the others are created. This avoids duplicate records when the same data is sent again.

### Input Format

The body is JSON text with a `records` list. All the records are of the kind named by `sObjectName`, and each one holds the external ID field named by `sObjectIdName`:

```json
{
  "records": [
    { "attributes": { "type": "Contact" }, "External_Id__c": "C-1", "LastName": "Lovelace" },
    { "attributes": { "type": "Contact" }, "External_Id__c": "C-2", "LastName": "Hopper" }
  ]
}
```

Salesforce accepts up to 200 records in one call.

### External ID Matching

Uses an external ID field for record matching, so that records keep the IDs of the system they come from. The field must be marked as External ID in Salesforce.

### Error Handling

The Kamelet does not use all-or-none: a record that Salesforce refuses does not fail the message, and the other records are still saved. The result is a list with one entry per record, in the same order, each with `id`, `success`, `created` (true for a new record) and `errors`.

### API Authentication

The Kamelet logs in through a connected app of your org. Create one in Salesforce Setup, under App Manager, with OAuth enabled, and copy its consumer key and secret into `clientId` and `clientSecret`. `authenticationType` chooses how the Kamelet logs in, and which other options it needs.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-composite-upsert-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-composite-upsert-sink.kamelet.yaml)
# ![salesforce delete sink](_images/kamelets/salesforce-delete-sink.svg) Salesforce Delete Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Remove an object from Salesforce.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-delete-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The Salesforce application consumer key. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The Salesforce application consumer secret. | string |  |  |
| **authenticationType** | Authentication Type | Authentication type to use. USERNAME\_PASSWORD needs userName and password, CLIENT\_CREDENTIALS needs only the consumer key and secret, REFRESH\_TOKEN needs refreshToken, JWT needs keystore and jwtAudience. Enum values: \* USERNAME\_PASSWORD \* CLIENT\_CREDENTIALS \* REFRESH\_TOKEN \* JWT | string | USERNAME\_PASSWORD |  |
| **instanceUrl** | Instance URL | Salesforce instance URL, needed when the authentication response does not carry one. | string |  | https://myinstance.my.salesforce.com |
| **jwtAudience** | JWT Audience | Audience claim for the JWT authentication type, usually the login URL of the target org. | string |  | https://login.salesforce.com |
| **keystore** | Keystore | Reference to a registry bean of type org.apache.camel.support.jsse.KeyStoreParameters, written as "#bean:myBeanName", holding the certificate that signs the JWT. Required by the JWT authentication type and ignored by the others. | string |  | #bean:myKeystore |
| **loginUrl** | Login URL | The Salesforce instance login URL. | string | [https://login.salesforce.com](https://login.salesforce.com) |  |
| **password** | Password | The Salesforce user password. | string |  |  |
| **refreshToken** | Refresh Token | Refresh token used by the REFRESH\_TOKEN authentication type. | string |  |  |
| **userName** | Username | The Salesforce username. | string |  |  |

## Dependencies

At runtime, the `salesforce-delete-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:salesforce
    
-   camel:kamelet
    
-   camel:core
    
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

This Kamelet integrates with Salesforce CRM to delete records from Salesforce objects. It provides secure record deletion capabilities through Salesforce’s REST API.

### Record Deletion

Deletes records from specified Salesforce objects using record IDs or external ID fields. Supports deletion of records from any accessible Salesforce object.

### Safety and Recovery

Salesforce provides safety mechanisms for deleted records:

-   Deleted records are moved to the Recycle Bin
    
-   Records can be restored within the retention period
    
-   Audit trails maintain deletion history
    

### Cascade Effects

Considers Salesforce’s cascade deletion rules and relationships when deleting records, ensuring referential integrity and proper handling of related data.

### Bulk Operations

Can be used for both individual record deletions and bulk deletion operations, depending on the integration requirements and data volume.

### Permission Controls

Respects Salesforce’s object-level and field-level security settings, ensuring that only authorized operations are performed based on user permissions.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-delete-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-delete-sink.kamelet.yaml)
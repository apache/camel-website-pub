# ![salesforce create sink](_images/kamelets/salesforce-create-sink.svg) Salesforce Create Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Create an object in Salesforce.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-create-sink` Kamelet:

     
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
| **sObjectName** | Object Name | The type of the object. | string |  | Contact |
| **userName** | Username | The Salesforce username. | string |  |  |

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

This Kamelet integrates with Salesforce CRM to create new records in Salesforce objects. It provides direct integration with Salesforce’s REST API for record creation operations.

### Record Creation

Creates new records in specified Salesforce objects (such as Accounts, Contacts, Leads, Opportunities, or custom objects) using the Salesforce REST API.

### Object Flexibility

Supports creation of records in any Salesforce object, including:

-   Standard objects (Account, Contact, Lead, etc.)
    
-   Custom objects specific to your organization
    
-   Junction objects for many-to-many relationships
    

### Field Mapping

Maps incoming data fields to Salesforce object fields, enabling seamless data transformation and integration between external systems and Salesforce.

### API Authentication

Uses Salesforce OAuth or other supported authentication mechanisms for secure API access and operation authorization.

### Data Validation

Leverages Salesforce’s built-in data validation rules, field requirements, and business logic to ensure data quality and consistency during record creation.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-create-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-create-sink.kamelet.yaml)
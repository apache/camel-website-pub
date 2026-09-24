# ![salesforce source](_images/kamelets/salesforce-source.svg) Salesforce Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive updates from Salesforce.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The Salesforce application consumer key. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The Salesforce application consumer secret. | string |  |  |
| **query** | Query | **Required** The query to execute on Salesforce. | string |  | SELECT Id, Name, Email, Phone FROM Contact |
| **topicName** | Topic Name | **Required** The name of the topic or channel. | string |  | ContactTopic |
| **authenticationType** | Authentication Type | Authentication type to use. USERNAME\_PASSWORD needs userName and password, CLIENT\_CREDENTIALS needs only the consumer key and secret, REFRESH\_TOKEN needs refreshToken, JWT needs keystore and jwtAudience. Enum values: \* USERNAME\_PASSWORD \* CLIENT\_CREDENTIALS \* REFRESH\_TOKEN \* JWT | string | USERNAME\_PASSWORD |  |
| **instanceUrl** | Instance URL | Salesforce instance URL, needed when the authentication response does not carry one. | string |  | https://myinstance.my.salesforce.com |
| **jwtAudience** | JWT Audience | Audience claim for the JWT authentication type, usually the login URL of the target org. | string |  | https://login.salesforce.com |
| **keystore** | Keystore | Reference to a registry bean of type org.apache.camel.support.jsse.KeyStoreParameters, written as "#bean:myBeanName", holding the certificate that signs the JWT. Required by the JWT authentication type and ignored by the others. | string |  | #bean:myKeystore |
| **loginUrl** | Login URL | The Salesforce instance login URL. | string | [https://login.salesforce.com](https://login.salesforce.com) |  |
| **notifyForFields** | Notify For Fields | Notify for fields. Enum values: \* ALL \* REFERENCED \* SELECT \* WHERE | string | ALL |  |
| **notifyForOperationCreate** | Notify Operation Create | Notify for create operation. | boolean | true |  |
| **notifyForOperationDelete** | Notify Operation Delete | Notify for delete operation. | boolean | false |  |
| **notifyForOperationUndelete** | Notify Operation Undelete | Notify for undelete operation. | boolean | false |  |
| **notifyForOperationUpdate** | Notify Operation Update | Notify for update operation. | boolean | false |  |
| **operation** | Operation | The operation to use. | string | subscribe |  |
| **password** | Password | The Salesforce user password. | string |  |  |
| **rawPayload** | Raw Payload | Use raw payload String for request and response (either JSON or XML depending on format), instead of DTOs, false by default. | boolean | false |  |
| **refreshToken** | Refresh Token | Refresh token used by the REFRESH\_TOKEN authentication type. | string |  |  |
| **replayId** | Replay Id | The replayId value to use when subscribing to the Streaming API. | long |  |  |
| **userName** | Username | The Salesforce username. | string |  |  |

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

This Kamelet requires Salesforce OAuth2 authentication using client credentials. You need to create a connected app in Salesforce and obtain the client ID, client secret, and other authentication details.

### Configuration

The Salesforce Source Kamelet supports the following configurations:

-   **Client ID**: Salesforce connected app client ID (required)
    
-   **Client Secret**: Salesforce connected app client secret (required)
    
-   **Username**: Salesforce username (required)
    
-   **Password**: Salesforce password + security token (required)
    
-   **Login URL**: Salesforce login URL (default: [https://login.salesforce.com](https://login.salesforce.com))
    
-   **API Version**: Salesforce API version (default: latest)
    
-   **SObject Name**: Salesforce object to query (required)
    
-   **SObject Query**: SOQL query to execute
    

### Output Format

The Kamelet outputs Salesforce records as JSON objects following the Salesforce REST API response format, including record metadata and field values.

### Setup Requirements

1.  Create a Connected App in Salesforce Setup
    
2.  Configure OAuth settings and permissions
    
3.  Obtain Client ID and Client Secret
    
4.  Generate or obtain security token for the user
    
5.  Ensure proper API permissions are granted
    

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:salesforce-source"
      parameters:
        clientId: "your-client-id"
        clientSecret: "your-client-secret"
        username: "salesforce-user@example.com"
        password: "password-with-security-token"
        sObjectName: "Account"
        sObjectQuery: "SELECT Id, Name, Industry FROM Account WHERE Industry = 'Technology'"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Custom Login URL

```yaml
- route:
    from:
      uri: "kamelet:salesforce-source"
      parameters:
        clientId: "your-client-id"
        clientSecret: "your-client-secret"
        username: "salesforce-user@example.com"
        password: "password-with-security-token"
        loginUrl: "https://test.salesforce.com"
        sObjectName: "Contact"
        sObjectQuery: "SELECT Id, FirstName, LastName, Email FROM Contact WHERE CreatedDate = TODAY"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### SOQL Query Examples

-   Simple selection: `SELECT Id, Name FROM Account`
    
-   With conditions: `SELECT Id, Name FROM Account WHERE Industry = 'Technology'`
    
-   With date filters: `SELECT Id, Name FROM Account WHERE CreatedDate >= YESTERDAY`
    
-   With relationships: `SELECT Id, Name, (SELECT Id, FirstName FROM Contacts) FROM Account`
    

### Security Considerations

-   Store credentials securely using secrets management
    
-   Use IP restrictions in Connected App settings
    
-   Rotate client secrets periodically
    
-   Monitor API usage to stay within limits
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-source.kamelet.yaml)
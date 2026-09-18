# ![ms exchange online imap oauth source](_images/kamelets/ms-exchange-online-imap-oauth-source.svg) Microsoft Exchange IMAP OAuth2 Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive unread emails from an IMAP Microsoft Exchange mail server, marking them as read once they are received.

## Configuration Options

The following table summarizes the configuration options available for the `ms-exchange-online-imap-oauth-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Client ID | **Required** Azure Active Directory Application Client ID. | string |  |  |
| **clientSecret** | Client Secret | **Required** The Azure Active Directory Application Client Secret. | string |  |  |
| **tenantId** | Tenant ID | **Required** Azure Active Directory Tenant ID. | string |  |  |
| **username** | Username | **Required** The username to access the mail box. | string |  | arthur@mycompany.com// |
| **connectionHost** | Connection Host | The IMAP server host. | string | outlook.office365.com |  |
| **connectionPort** | Connection Port | The IMAP server port. | string | 993 |  |
| **delay** | Delay | The delay between fetches in milliseconds. | integer | 60000 |  |
| **fetchSize** | Fetch Size | The number of messages fetched for each poll (-1 for no limits). | integer | 10 |  |

## Dependencies

At runtime, the `ms-exchange-online-imap-oauth-source` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kamelet
    
-   camel:mail-microsoft-oauth
    
-   camel:mail
    

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
      uri: "kamelet:ms-exchange-online-imap-oauth-source"
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

## Ms Exchange Online Imap Oauth Source Kamelet Description

### Authentication methods

This Kamelet connects to Ms Exchange Online Imap Oauth using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Ms Exchange Online Imap Oauth and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Ms Exchange Online Imap Oauth:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: ms-exchange-online-imap-oauth-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: ms-exchange-online-imap-oauth-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ms-exchange-online-imap-oauth-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ms-exchange-online-imap-oauth-source.kamelet.yaml)
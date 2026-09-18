# ![mail sink](_images/kamelets/mail-sink.svg) Mail Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send mails to given SMTP server.

## Configuration Options

The following table summarizes the configuration options available for the `mail-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Host | **Required** The mail server host. | string |  | smtp.gmail.com |
| **password** | Password | **Required** The password to access the mail box. | string |  |  |
| **username** | Username | **Required** The username to access the mail box. | string |  |  |
| **connectionPort** | Port | The mail server port. | string | 25 |  |
| **from** | From | The `from` field of the outgoing mail. | string |  |  |
| **subject** | Subject | The mail subject of the outgoing mail. | string |  |  |
| **to** | To | The `to` field of the outgoing mail. | string |  |  |

## Dependencies

At runtime, the `mail-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:mail
    
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
            uri: "kamelet:mail-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Mail Sink Kamelet Description

### SMTP Email Delivery

This Kamelet sends emails through SMTP servers with configurable authentication and addressing.

### Required Configuration

-   **Connection Host**: SMTP server hostname (e.g., smtp.gmail.com)
    
-   **Username and Password**: SMTP authentication credentials
    

### Optional Configuration

-   **Connection Port**: SMTP port (defaults to 25)
    
-   **From**: Sender email address
    
-   **To**: Primary recipient
    
-   **Subject**: Email subject line
    

### Email Headers Support

The Kamelet supports various email headers through CloudEvents: - `ce-subject`: Override email subject - `ce-from`: Override sender address - `ce-to`: Override recipient address - `ce-cc`: Add CC recipients

### Usage

Enables automated email notifications, alerts, and reports by sending emails through configured SMTP servers as part of integration workflows.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-sink.kamelet.yaml)
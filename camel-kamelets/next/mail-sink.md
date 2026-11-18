# ![mail sink](_images/kamelets/mail-sink.svg) Mail Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as an email through an SMTP server, with the body as the text of the email.

Use it to send notifications, alerts or reports by email, for example tell a team when an order fails or send a daily summary.

Input: the body is the text of the email. With a `Content-Type` header of `text/html`, the email is sent as HTML. The `ce-subject`, `ce-from`, `ce-to` and `ce-cc` headers set the subject, the sender, the recipients and the copy recipients of one email, in place of the options; several addresses are separated by commas. Other mail headers on the message, such as `To` or `Bcc`, are removed and not used.

Output: the message is unchanged. The `CamelMailMessageId` header holds the ID of the email that was sent.

Good to know: each email needs a sender, recipients and a subject, from the options or from the `ce-from`, `ce-to` and `ce-subject` headers. The default protocol, `smtps`, connects with TLS from the start, usually on port 465, and checks the certificate of the server. For a server that uses STARTTLS, usually on port 587, set `protocol` to `smtp` and `startTls` to true: the connection is then encrypted before the login, the certificate and the host name of the server are checked, and sending fails when the server does not offer STARTTLS. With `smtp` alone, the connection, the password and the emails are not encrypted.

## Configuration Options

The following table summarizes the configuration options available for the `mail-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Host | **Required** The host name of the SMTP server of the mail provider, without a port. | string |  | smtp.example.com |
| **password** | Password | **Required** The password of `username` on the SMTP server. | string |  |  |
| **username** | Username | **Required** The user to log in to the SMTP server as, usually an email address. | string |  |  |
| **connectionPort** | Port | The port of the SMTP server, usually 465 for `smtps`, 587 for `smtp` with `startTls`, and 25 for `smtp` without encryption. | string | 465 |  |
| **from** | From | The sender address of the emails. The `ce-from` header replaces it for one message. It can be left empty when every message has that header. | string |  | alerts@example.com// |
| **protocol** | Protocol | How to connect to the server. `smtps` connects with TLS from the start, usually on port 465. `smtp` connects without encryption, so the password and the emails are sent as clear text, unless `startTls` is true. Enum values: \* smtp \* smtps | string | smtps |  |
| **startTls** | STARTTLS | Whether to switch an `smtp` connection to TLS with the STARTTLS command before logging in, as most mail providers ask for on port 587. When true, the certificate and the host name of the server are checked, and sending fails when the server does not offer STARTTLS, so the password is never sent as clear text. Only used when `protocol` is `smtp`; with `smtps` the connection is encrypted from the start. When false or not set, the Kamelet does not ask for STARTTLS, and a server that offers the login only after STARTTLS, such as Gmail or Office 365 on port 587, rejects the emails. | boolean |  |  |
| **subject** | Subject | The subject of the emails. The `ce-subject` header replaces it for one message. It can be left empty when every message has that header. | string |  | Order failed |
| **to** | To | The recipient of the emails; several addresses are separated by commas. The `ce-to` header replaces it for one message. It can be left empty when every message has that header. | string |  | team@example.com// |

## Dependencies

At runtime, the `mail-sink` Kamelet relies upon the presence of the following dependencies:

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

-   **Connection Port**: SMTP port (defaults to 465)
    
-   **Protocol**: `smtps` (the default, TLS from the start) or `smtp` (no encryption, unless **STARTTLS** is on)
    
-   **STARTTLS**: with `smtp`, switch the connection to TLS before logging in, as most mail providers ask for on port 587
    
-   **From**: Sender email address
    
-   **To**: Recipients, separated by commas
    
-   **Subject**: Email subject line
    

**From**, **To** and **Subject** can be left empty when every message carries the matching `ce-from`, `ce-to` and `ce-subject` header.

### Connecting to the SMTP Server

   
| Protocol | STARTTLS | Usual port | Connection |
| --- | --- | --- | --- |
| `smtps` | (not used) | 465 | TLS from the start. The certificate of the server is checked. |
| `smtp` | `true` | 587 | Starts without TLS, then switches to TLS with STARTTLS before logging in. The certificate and the host name of the server are checked. Sending fails when the server does not offer STARTTLS, so the password is never sent as clear text. |
| `smtp` | not set or `false` | 25 | No encryption: the password and the emails are sent as clear text. A server that offers the login only after STARTTLS, such as Gmail or Office 365 on port 587, rejects the emails. |

For example, to send through a provider on port 587:

```yaml
connectionHost: smtp.example.com
connectionPort: 587
protocol: smtp
startTls: true
```

### Email Headers Support

The Kamelet supports various email headers through CloudEvents: - `ce-subject`: Override email subject - `ce-from`: Override sender address - `ce-to`: Override recipient address - `ce-cc`: Add CC recipients

Other mail headers on the message, such as `To`, `Cc` or `Bcc`, are removed. A `Content-Type` header of `text/html` sends the body as an HTML email.

### Usage

Enables automated email notifications, alerts, and reports by sending emails through configured SMTP servers as part of integration workflows.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-sink.kamelet.yaml)
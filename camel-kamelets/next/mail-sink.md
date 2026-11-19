# ![mail sink](_images/kamelets/mail-sink.svg) Mail Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as an email through an SMTP server, with the body as the text of the email.

Use it to send notifications, alerts or reports by email, for example tell a team when an order fails or send a daily summary.

Input: the body is the text of the email. It is sent as the type in `contentType`; when that is not set, as the type in the `Content-Type` header, such as `text/html` for an HTML email, and otherwise as plain text. The `ce-subject`, `ce-from`, `ce-to` and `ce-cc` headers set the subject, the sender, the recipients and the copy recipients of one email, each in place of its option; several addresses are separated by commas. Other mail headers on the message, such as `To`, `Bcc` or `Reply-To`, are removed and not used, so the blind copy recipients and the reply address come only from the `bcc` and `replyTo` options.

Output: the message is unchanged. The `CamelMailMessageId` header holds the ID of the email that was sent.

Good to know: each email needs a sender, recipients and a subject, from the options or from the `ce-from`, `ce-to` and `ce-subject` headers. The default protocol, `smtps`, connects with TLS from the start, usually on port 465, and checks the certificate of the server. For a server that uses STARTTLS, usually on port 587, set `protocol` to `smtp` and `startTls` to true: the connection is then encrypted before the login, the certificate and the host name of the server are checked, and sending fails when the server does not offer STARTTLS. With `smtp` alone, the connection, the password and the emails are not encrypted. The certificate is checked against the certificate authorities that Java trusts. To trust a private one with Camel JBang or Camel Main, set the application properties `camel.ssl.enabled=true`, `camel.ssl.trustStore`, `camel.ssl.trustStorePassword`, and `camel.component.smtps.useGlobalSslContextParameters=true` for `smtps` or `camel.component.smtp.useGlobalSslContextParameters=true` for `smtp` with `startTls`: that trust store then replaces the one of Java for every connection of the application with that protocol.

## Configuration Options

The following table summarizes the configuration options available for the `mail-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Host | **Required** The host name of the SMTP server of the mail provider, without a port. | string |  | smtp.example.com |
| **password** | Password | **Required** The password of `username` on the SMTP server. | string |  |  |
| **username** | Username | **Required** The user to log in to the SMTP server as, usually an email address. | string |  |  |
| **bcc** | Bcc | The blind copy recipients of the emails; several addresses are separated by commas. They receive each email, and the other recipients do not see them. Messages cannot change them. | string |  | archive@example.com// |
| **cc** | Cc | The copy recipients of the emails; several addresses are separated by commas. The `ce-cc` header replaces it for one message. | string |  | manager@example.com// |
| **connectionPort** | Port | The port of the SMTP server, usually 465 for `smtps`, 587 for `smtp` with `startTls`, and 25 for `smtp` without encryption. | string | 465 |  |
| **contentType** | Content Type | The type of the text in the body of every email, such as `text/html` to send HTML emails. When it is set, the `Content-Type` header of the message is not used. When it is not set, that header sets the type, and without it the emails are sent as plain text (`text/plain`). Some sources set that header, such as `timer-source`, which sets `text/plain` by default. | string |  | text/html |
| **from** | From | The sender address of the emails. The `ce-from` header replaces it for one message. It can be left empty when every message has that header. | string |  | alerts@example.com// |
| **protocol** | Protocol | How to connect to the server. `smtps` connects with TLS from the start, usually on port 465. `smtp` connects without encryption, so the password and the emails are sent as clear text, unless `startTls` is true. Enum values: \* smtp \* smtps | string | smtps |  |
| **replyTo** | Reply To | The address that replies to the emails go to, in place of the sender; several addresses are separated by commas. Messages cannot change it. | string |  | support@example.com// |
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
    
-   **Cc**: Copy recipients, separated by commas
    
-   **Bcc**: Blind copy recipients, separated by commas
    
-   **Reply To**: The address that replies go to, in place of the sender
    
-   **Content Type**: The type of the text in the body, such as `text/html` (default: plain text)
    

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

The Kamelet supports various email headers through CloudEvents: - `ce-subject`: Override email subject - `ce-from`: Override sender address - `ce-to`: Override the `to` recipients - `ce-cc`: Override the `cc` recipients

Each header replaces only its own option: with a `ce-to` header, the `cc` and `bcc` recipients of the options still receive the email. Other mail headers on the message, such as `To`, `Cc`, `Bcc` or `Reply-To`, are removed, so the blind copy recipients and the reply address come only from the options. A `Content-Type` header, such as `text/html`, sets the type of one email when the `contentType` option is not set; when it is set, the header is not used.

For example, to send HTML emails to a team, with a copy to a manager, a blind copy to an archive mailbox, and replies to the support address:

```yaml
connectionHost: smtp.example.com
username: alerts@example.com
password: secret
from: alerts@example.com
to: team@example.com
cc: manager@example.com
bcc: archive@example.com
replyTo: support@example.com
contentType: text/html
subject: Order failed
```

### Trusting a Private Certificate Authority

The certificate of the server is checked against the certificate authorities that Java trusts. For a server with a certificate from a private or self-signed authority, put that authority in a trust store file (JKS or PKCS12), and set these application properties with Camel JBang or Camel Main:

```properties
camel.ssl.enabled=true
camel.ssl.trustStore=file:/etc/mail/truststore.p12
camel.ssl.trustStorePassword=changeit
# with protocol smtps
camel.component.smtps.useGlobalSslContextParameters=true
# with protocol smtp and startTls true
camel.component.smtp.useGlobalSslContextParameters=true
```

That trust store then replaces the one of Java for every connection of the application with that protocol. The host name of the server is still checked.

### Usage

Enables automated email notifications, alerts, and reports by sending emails through configured SMTP servers as part of integration workflows.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-sink.kamelet.yaml)
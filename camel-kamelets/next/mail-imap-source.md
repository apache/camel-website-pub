# ![mail imap source](_images/kamelets/mail-imap-source.svg) Mail IMAP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the unread emails in the inbox of a mailbox over IMAP, one message per email, and marks each email as read.

Use it to start a flow from incoming email, for example turn support requests into tickets, or process the orders and invoices that customers send by email. For a Microsoft 365 mailbox that needs an OAuth login, use `ms-exchange-online-imap-oauth-source`, and for Gmail through its API, use `google-mail-source`.

Output: the body is the text of the email. For an email with several parts, such as text and HTML or attachments, it is the text of the first part; attachments are not in the body. The `ce-subject`, `ce-from`, `ce-to` and `ce-cc` headers hold the subject and the addresses, and the headers of the email, such as `Subject`, `From`, `Date` and `Message-ID`, are copied too.

Good to know: emails stay in the mailbox, marked as read, and emails that are already read are skipped. It reads only the `INBOX` folder. It always connects with TLS (IMAPS) and checks the certificate of the server. It checks for new email once a minute by default (`delay`).

## Configuration Options

The following table summarizes the configuration options available for the `mail-imap-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name of the IMAP server of the mail provider, without a port. | string |  | imap.example.com |
| **connectionPort** | Connection Port | **Required** The port of the IMAP server for TLS connections (IMAPS), usually 993. | string | 993 |  |
| **password** | Password | **Required** The password of `username`. Some providers need an app password here, made in the security settings of the account, instead of the password of the account. | string |  |  |
| **username** | Username | **Required** The user to log in to the mailbox as, usually the email address. | string |  |  |
| **delay** | Delay | How long to wait between two checks of the mailbox, in milliseconds. The default, 60000, is one minute. | integer | 60000 |  |
| **fetchSize** | Fetch Size | The most emails to read at each check of the mailbox. Use -1 for no limit. | integer | 10 |  |

## Dependencies

At runtime, the `mail-imap-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:mail-imap-source"
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

## Mail IMAP Source Kamelet Description

### Authentication

This Kamelet requires username and password authentication to connect to an IMAP mail server. It always connects with TLS (IMAPS) and checks the certificate of the server.

### Configuration

The Mail IMAP Source Kamelet supports the following configurations:

-   **Connection Host** (`connectionHost`): IMAP server hostname (required)
    
-   **Connection Port** (`connectionPort`): IMAPS server port (default: 993)
    
-   **Username** (`username`): Email account username (required)
    
-   **Password** (`password`): Email account password (required)
    
-   **Fetch Size** (`fetchSize`): The most emails to read at each check (default: 10, -1 for no limit)
    
-   **Delay** (`delay`): Milliseconds between two checks of the mailbox (default: 60000)
    

The Kamelet reads only the unread emails of the `INBOX` folder, and marks each one as read. Emails are not deleted.

### Output Format

The body is the text of the email; for an email with several parts, it is the text of the first part, and attachments are not in the body. The `ce-subject`, `ce-from`, `ce-to` and `ce-cc` headers hold the subject and the addresses, and the headers of the email (`Subject`, `From`, `Date`, …​) are copied too.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:mail-imap-source"
      parameters:
        connectionHost: "imap.gmail.com"
        connectionPort: "993"
        username: "user@gmail.com"
        password: "app-password"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with a Shorter Delay

```yaml
- route:
    from:
      uri: "kamelet:mail-imap-source"
      parameters:
        connectionHost: "mail.example.com"
        connectionPort: "993"
        username: "support@example.com"
        password: "mailpass"
        delay: 10000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Security Considerations

-   Use app-specific passwords for Gmail and similar providers
    
-   Store credentials securely using secrets management
    
-   Consider OAuth2 authentication for enhanced security
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-imap-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-imap-source.kamelet.yaml)
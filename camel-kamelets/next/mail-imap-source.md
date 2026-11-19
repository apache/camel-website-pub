# ![mail imap source](_images/kamelets/mail-imap-source.svg) Mail IMAP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the unread emails in a folder of a mailbox over IMAP, by default the inbox, one message per email, and marks each email as read.

Use it to start a flow from incoming email, for example turn support requests into tickets, or process the orders and invoices that customers send by email. For a Microsoft 365 mailbox that needs an OAuth login, use `ms-exchange-online-imap-oauth-source`, and for Gmail through its API, use `google-mail-source`.

Output: the body is the text of the email. For an email with several parts, such as text and HTML or attachments, it is the text of the first part; attachments are not in the body. The `ce-subject`, `ce-from`, `ce-to` and `ce-cc` headers hold the subject and the addresses, and the headers of the email, such as `Subject`, `From`, `Date` and `Message-ID`, are copied too.

Good to know: by default it reads the `INBOX` folder, emails stay in the folder, marked as read, and emails that are already read are skipped. Set `delete` or `moveTo` to remove the emails once they are processed, `unseen` to false to read the emails that are already read too, and the search options, such as `searchFrom` or `searchSubject`, to read only some emails; an email must match every search option that is set. An email whose processing fails stays unread and is read again at the next check. An email that cannot be read at all, such as one with a broken format, fails every check of the mailbox until it is removed, unless `skipFailedMessage` is true. It always connects with TLS (IMAPS), and checks the certificate and the host name of the server against the certificate authorities that Java trusts. To trust a private one with Camel JBang or Camel Main, set the application properties `camel.ssl.enabled=true`, `camel.ssl.trustStore`, `camel.ssl.trustStorePassword` and `camel.component.imaps.useGlobalSslContextParameters=true`: that trust store then replaces the one of Java for every IMAPS connection of the application. It checks for new email once a minute by default (`delay`).

## Configuration Options

The following table summarizes the configuration options available for the `mail-imap-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name of the IMAP server of the mail provider, without a port. | string |  | imap.example.com |
| **connectionPort** | Connection Port | **Required** The port of the IMAP server for TLS connections (IMAPS), usually 993. | string | 993 |  |
| **password** | Password | **Required** The password of `username`. Some providers need an app password here, made in the security settings of the account, instead of the password of the account. | string |  |  |
| **username** | Username | **Required** The user to log in to the mailbox as, usually the email address. | string |  |  |
| **copyTo** | Copy To | The folder to copy each email to once it is processed, such as `Archive`. The folder is created when it does not exist. The email also stays in the folder that is read, and the copy is not marked as read. An email whose processing fails is not copied. | string |  | Archive |
| **delay** | Delay | How long to wait between two checks of the mailbox, in milliseconds. The default, 60000, is one minute. | integer | 60000 |  |
| **delete** | Delete | Whether to delete each email from the folder once it is processed. When it is not set, emails stay in the folder, marked as read. An email whose processing fails is not deleted. | boolean |  |  |
| **fetchSize** | Fetch Size | The most emails to read at each check of the mailbox. Use -1 for no limit. | integer | 10 |  |
| **folderName** | Folder Name | The folder to read the emails from. When it is not set, the Kamelet reads the `INBOX` folder. A subfolder is written with the separator of the server, usually `/` or `.`, such as `INBOX/Orders`. When the folder does not exist, each check of the mailbox fails with a warning in the log. | string |  | INBOX/Orders |
| **moveTo** | Move To | The folder to move each email to once it is processed, such as `Processed`. The folder is created when it does not exist. The email is then no longer in the folder that is read. An email whose processing fails is not moved. | string |  | Processed |
| **peek** | Peek | Whether to keep an email unread while it is processed, so that an email whose processing fails stays unread and is read again at the next check. When it is not set, this is on. When false, an email is marked as read as soon as it is read, and an email whose processing fails is not read again. | boolean |  |  |
| **searchFrom** | Search From | Read only the emails whose sender contains this text, such as `billing@supplier.example`. Upper and lower case are the same. The mail server does the search, and some servers match only a whole address, so give the whole address to be safe. | string |  | \\billing@supplier.example// |
| **searchSubject** | Search Subject | Read only the emails whose subject contains this text, such as `invoice`. Upper and lower case are the same. | string |  | invoice |
| **searchSubjectOrBody** | Search Subject or Body | Read only the emails whose subject or text contains this text, such as `refund`. Upper and lower case are the same. | string |  | refund |
| **searchTo** | Search To | Read only the emails whose `To` recipients contain this text, such as an address. The copy recipients (`Cc`) are not searched. Upper and lower case are the same. The mail server does the search, and some servers match only a whole address, so give the whole address to be safe. | string |  | orders@example.com// |
| **skipFailedMessage** | Skip Failed Email | Whether to skip an email that cannot be read at all, such as one with a broken format, and go on with the other emails. When it is not set, such an email fails the whole check of the mailbox, again at each check, and no email is read until it is removed from the folder. A skipped email stays in the folder, unread, and no error is logged. | boolean |  |  |
| **unseen** | Unread Only | Whether to read only the emails that are not marked as read. When it is not set, only unread emails are read. When false, the emails that are already read are read too; without `delete` or `moveTo`, every email in the folder is then read again at each check. | boolean |  |  |

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

This Kamelet requires username and password authentication to connect to an IMAP mail server. It always connects with TLS (IMAPS) and checks the certificate and the host name of the server.

### Configuration

The Mail IMAP Source Kamelet supports the following configurations:

-   **Connection Host** (`connectionHost`): IMAP server hostname (required)
    
-   **Connection Port** (`connectionPort`): IMAPS server port (default: 993)
    
-   **Username** (`username`): Email account username (required)
    
-   **Password** (`password`): Email account password (required)
    
-   **Fetch Size** (`fetchSize`): The most emails to read at each check (default: 10, -1 for no limit)
    
-   **Delay** (`delay`): Milliseconds between two checks of the mailbox (default: 60000)
    
-   **Folder Name** (`folderName`): The folder to read (default: `INBOX`)
    
-   **Unread Only** (`unseen`): Set to `false` to read the emails that are already read too
    
-   **Delete** (`delete`), **Move To** (`moveTo`), **Copy To** (`copyTo`): What to do with each email once it is processed
    
-   **Peek** (`peek`): Keeps an email unread while it is processed (on by default)
    
-   **Skip Failed Email** (`skipFailedMessage`): Skips an email that cannot be read at all
    
-   **Search From**, **Search To**, **Search Subject**, **Search Subject or Body** (`searchFrom`, `searchTo`, `searchSubject`, `searchSubjectOrBody`): Read only the emails that match
    

By default, the Kamelet reads only the unread emails of the `INBOX` folder, and marks each one as read. Emails are not deleted.

### What Happens to an Email

  
| Options | Once the email is processed | When processing the email fails |
| --- | --- | --- |
| none | Stays in the folder, marked as read. | Stays unread, and is read again at the next check. |
| `delete: true` | Deleted from the folder. | Stays unread, and is read again at the next check. |
| `moveTo: Processed` | Moved to `Processed`, marked as read. The folder is created when it does not exist. | Stays unread, and is read again at the next check. |
| `copyTo: Archive` | Stays in the folder, marked as read. An unread copy is put in `Archive`. | Stays unread, not copied, and is read again at the next check. |
| `peek: false` | As above. | Marked as read, and not read again. |
| `unseen: false` without `delete` or `moveTo` | Stays in the folder, and is read again at every check. | Read again at every check. |

An email that cannot be read at all, such as one with a broken format, fails the whole check of the mailbox, so no email is read until it is removed. With `skipFailedMessage: true`, it is skipped and stays unread, and the other emails are read.

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

### Example: Invoices from a Supplier

Read the emails from one sender with `invoice` in the subject, from a subfolder, and move each one to `Processed` once it is processed:

```yaml
- route:
    from:
      uri: "kamelet:mail-imap-source"
      parameters:
        connectionHost: "mail.example.com"
        connectionPort: "993"
        username: "accounts@example.com"
        password: "mailpass"
        folderName: "INBOX/Suppliers"
        searchFrom: "billing@supplier.example"
        searchSubject: "invoice"
        moveTo: "Processed"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Every search option that is set must match. The mail server does the search, without telling upper and lower case apart. Some servers match only a whole address in `searchFrom` and `searchTo`, so give the whole address.

### Trusting a Private Certificate Authority

The certificate of the server is checked against the certificate authorities that Java trusts. For a server with a certificate from a private or self-signed authority, put that authority in a trust store file (JKS or PKCS12), and set these application properties with Camel JBang or Camel Main:

```properties
camel.ssl.enabled=true
camel.ssl.trustStore=file:/etc/mail/truststore.p12
camel.ssl.trustStorePassword=changeit
camel.component.imaps.useGlobalSslContextParameters=true
```

That trust store then replaces the one of Java for every IMAPS connection of the application. The host name of the server is still checked.

### Security Considerations

-   Use app-specific passwords for Gmail and similar providers
    
-   Store credentials securely using secrets management
    
-   Consider OAuth2 authentication for enhanced security
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-imap-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-imap-source.kamelet.yaml)
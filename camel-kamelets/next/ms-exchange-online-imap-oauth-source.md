# ![ms exchange online imap oauth source](_images/kamelets/ms-exchange-online-imap-oauth-source.svg) Microsoft Exchange IMAP OAuth2 Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the unread emails in a folder of a Microsoft 365 (Exchange Online) mailbox over IMAP, by default the inbox, logging in with OAuth 2.0, and marks each email as read.

Use it to process the email that arrives in a Microsoft 365 mailbox where login with a password is turned off, for example orders, invoices or support requests sent to a shared address. For other mail servers, use `mail-imap-source`.

Output: the body is the text of the email. For an email with several parts, such as text and HTML or attachments, it is the content of the parts, which the next step reads as the text of the first part. The headers of the email, such as `Subject`, `From`, `To` and `Date`, are copied to the message.

Good to know: it logs in as an application, not as a person: register an application in Microsoft Entra ID (formerly Azure Active Directory) with a client secret, and allow it to read the mailbox over IMAP. It gets a token when it starts, so with wrong credentials, such as an unknown tenant ID, the integration does not start. By default it reads the `INBOX` folder, emails stay in the folder, marked as read, and emails that are already read are skipped. Set `delete` or `moveTo` to remove the emails once they are processed, `unseen` to false to read the emails that are already read too, and the search options, such as `searchFrom` or `searchSubject`, to read only some emails; an email must match every search option that is set. An email whose processing fails stays unread and is read again at the next check. An email that cannot be read at all, such as one with a broken format, fails every check of the mailbox until it is removed, unless `skipFailedMessage` is true. It connects over TLS, and checks for new email once a minute by default (`delay`).

## Configuration Options

The following table summarizes the configuration options available for the `ms-exchange-online-imap-oauth-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Client ID | **Required** The Application (client) ID of the app registration, a GUID shown on its overview page in the Azure portal. | string |  |  |
| **clientSecret** | Client Secret | **Required** A client secret of the app registration, made under Certificates and secrets in the Azure portal. Use the value of the secret, not its ID. | string |  |  |
| **tenantId** | Tenant ID | **Required** The ID of your Microsoft Entra ID tenant (directory), a GUID shown as Directory (tenant) ID on the overview page of the app registration in the Azure portal. | string |  | 11111111-2222-3333-4444-555555555555 |
| **username** | Username | **Required** The email address of the mailbox to read. | string |  | orders@example.com// |
| **connectionHost** | Connection Host | The host name of the IMAP server. The default is the IMAP server of Microsoft 365. | string | outlook.office365.com |  |
| **connectionPort** | Connection Port | The port of the IMAP server for TLS connections (IMAPS). | string | 993 |  |
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

At runtime, the `ms-exchange-online-imap-oauth-source` Kamelet relies upon the presence of the following dependencies:

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

## Microsoft Exchange IMAP OAuth2 Source Kamelet Description

### Authentication

This Kamelet logs in to a Microsoft 365 (Exchange Online) mailbox over IMAP with OAuth 2.0, as an application and not as a person (the client credentials flow). It needs:

-   An app registration in Microsoft Entra ID (formerly Azure Active Directory), with a client secret.
    
-   The app allowed to read the mailbox over IMAP. In Microsoft’s documentation on OAuth for IMAP, this is the `IMAP.AccessAsApp` application permission of Office 365 Exchange Online, with admin consent, and the service principal of the app given access to the mailbox in Exchange Online.
    

From the app registration, use the Directory (tenant) ID as `tenantId`, the Application (client) ID as `clientId`, and the value of the client secret as `clientSecret`. Set `username` to the email address of the mailbox.

### Output format

By default, the Kamelet reads the unread emails of the `INBOX` folder, one message per email, and marks each email as read. Emails stay in the mailbox. The body is the text of the email; for an email with several parts (text and HTML, attachments), it is the multipart content, which reads as the text of the first part. The headers of the email, such as `Subject`, `From`, `To` and `Date`, are copied to the message.

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:ms-exchange-online-imap-oauth-source"
      parameters:
        tenantId: "11111111-2222-3333-4444-555555555555"
        clientId: "{{exchange.clientId}}"
        clientSecret: "{{exchange.clientSecret}}"
        username: "orders@example.com"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Choosing and Moving Emails

These options work as in `mail-imap-source`:

-   `folderName`: the folder to read, such as `Inbox/Orders` (default: `INBOX`).
    
-   `unseen`: set to `false` to read the emails that are already read too.
    
-   `delete`, `moveTo`, `copyTo`: what to do with each email once it is processed. A folder in `moveTo` or `copyTo` is created when it does not exist.
    
-   `peek`: keeps an email unread while it is processed, so that an email whose processing fails is read again at the next check (on by default).
    
-   `skipFailedMessage`: skips an email that cannot be read at all, such as one with a broken format, instead of failing every check of the mailbox.
    
-   `searchFrom`, `searchTo`, `searchSubject`, `searchSubjectOrBody`: read only the emails that match. Every search option that is set must match.
    

For example, to read the orders from one sender and move each one to the `Processed` folder:

```yaml
- route:
    from:
      uri: "kamelet:ms-exchange-online-imap-oauth-source"
      parameters:
        tenantId: "11111111-2222-3333-4444-555555555555"
        clientId: "{{exchange.clientId}}"
        clientSecret: "{{exchange.clientSecret}}"
        username: "orders@example.com"
        searchFrom: "orders@shop.example"
        searchSubject: "order"
        moveTo: "Processed"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ms-exchange-online-imap-oauth-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ms-exchange-online-imap-oauth-source.kamelet.yaml)
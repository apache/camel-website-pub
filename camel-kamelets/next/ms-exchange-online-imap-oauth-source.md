# ![ms exchange online imap oauth source](_images/kamelets/ms-exchange-online-imap-oauth-source.svg) Microsoft Exchange IMAP OAuth2 Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the unread emails in the inbox of a Microsoft 365 (Exchange Online) mailbox over IMAP, logging in with OAuth 2.0, and marks each email as read.

Use it to process the email that arrives in a Microsoft 365 mailbox where login with a password is turned off, for example orders, invoices or support requests sent to a shared address. For other mail servers, use `mail-imap-source`.

Output: the body is the text of the email. For an email with several parts, such as text and HTML or attachments, it is the content of the parts, which the next step reads as the text of the first part. The headers of the email, such as `Subject`, `From`, `To` and `Date`, are copied to the message.

Good to know: it logs in as an application, not as a person: register an application in Microsoft Entra ID (formerly Azure Active Directory) with a client secret, and allow it to read the mailbox over IMAP. It gets a token when it starts, so with wrong credentials, such as an unknown tenant ID, the integration does not start. Emails stay in the mailbox, marked as read, and emails that are already read are skipped. It reads only the `INBOX` folder, over TLS, and checks for new email once a minute by default (`delay`).

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
| **delay** | Delay | How long to wait between two checks of the mailbox, in milliseconds. The default, 60000, is one minute. | integer | 60000 |  |
| **fetchSize** | Fetch Size | The most emails to read at each check of the mailbox. Use -1 for no limit. | integer | 10 |  |

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

The Kamelet reads the unread emails of the `INBOX` folder, one message per email, and marks each email as read. Emails stay in the mailbox. The body is the text of the email; for an email with several parts (text and HTML, attachments), it is the multipart content, which reads as the text of the first part. The headers of the email, such as `Subject`, `From`, `To` and `Date`, are copied to the message.

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ms-exchange-online-imap-oauth-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ms-exchange-online-imap-oauth-source.kamelet.yaml)
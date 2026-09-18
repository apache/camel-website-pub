# ![mail imap source](_images/kamelets/mail-imap-source.svg) Mail IMAP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive unread emails from an IMAP mail server, marking them as read once they are received.

## Configuration Options

The following table summarizes the configuration options available for the `mail-imap-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The IMAP server host. | string |  | imap.gmail.com |
| **connectionPort** | Connection Port | **Required** The IMAP server port. | string | 993 |  |
| **password** | Password | **Required** The password to access the mail box. | string |  |  |
| **username** | Username | **Required** The username to access the mail box. | string |  |  |
| **delay** | Delay | The delay between fetches in milliseconds. | integer | 60000 |  |
| **fetchSize** | Fetch Size | The number of messages fetched for each poll (-1 for no limits). | integer | 10 |  |

## Dependencies

At runtime, the `mail-imap-source` Kamelet relies upon the presence of the following dependencies:

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

This Kamelet requires username and password authentication to connect to an IMAP mail server. It supports both standard and secure IMAP connections.

### Configuration

The Mail IMAP Source Kamelet supports the following configurations:

-   **Host**: IMAP server hostname (required)
    
-   **Port**: IMAP server port (default: 993 for IMAPS, 143 for IMAP)
    
-   **Username**: Email account username (required)
    
-   **Password**: Email account password (required)
    
-   **Folder**: Email folder to monitor (default: "INBOX")
    
-   **Unseen Only**: Only process unread emails (default: true)
    
-   **Delete**: Delete emails after processing (default: false)
    
-   **Connection Encryption**: Use SSL/TLS encryption (default: true)
    

### Output Format

The Kamelet outputs email messages including headers, body content, attachments, and metadata such as sender, recipient, and timestamp information.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:mail-imap-source"
      parameters:
        host: "imap.gmail.com"
        port: "993"
        username: "user@gmail.com"
        password: "app-password"
        folder: "INBOX"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Custom Folder

```yaml
- route:
    from:
      uri: "kamelet:mail-imap-source"
      parameters:
        host: "mail.example.com"
        port: "993"
        username: "support@example.com"
        password: "mailpass"
        folder: "Support"
        unseenOnly: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Email Deletion

```yaml
- route:
    from:
      uri: "kamelet:mail-imap-source"
      parameters:
        host: "imap.example.com"
        username: "processor@example.com"
        password: "mailpass"
        folder: "Processing"
        delete: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Security Considerations

-   Use app-specific passwords for Gmail and similar providers
    
-   Enable SSL/TLS encryption for secure connections
    
-   Store credentials securely using secrets management
    
-   Consider OAuth2 authentication for enhanced security
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-imap-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mail-imap-source.kamelet.yaml)
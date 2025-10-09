# ![dropbox source](_images/kamelets/dropbox-source.svg) Dropbox Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume Files from Dropbox.

## Configuration Options

The following table summarizes the configuration options available for the `dropbox-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Dropbox Access Token | **Required** The access Token to use to access Dropbox. | string |  |  |
| **clientIdentifier** | Client Identifier | **Required** Dropbox App client Identifier. | string |  |  |
| **period** | Period between Polls | **Required** The interval between fetches to the Dropbox remote path in milliseconds. | integer | 10000 |  |
| **query** | Queries | **Required** A space-separated list of sub-strings to search for. A file matches only if it contains all the sub-strings. If this option is not set, all files is matched. | string |  |  |
| **remotePath** | Remote Path | **Required** Original file or folder to work with. | string |  |  |

## Dependencies

At runtime, the `dropbox-source` Kamelet relies upon the presence of the following dependencies:

-   camel:dropbox
    
-   camel:kamelet
    
-   camel:core
    
-   camel:jsonpath
    
-   camel:timer
    

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
      uri: "kamelet:dropbox-source"
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

## Dropbox Source Kamelet Description

This Kamelet consumes files from Dropbox by periodically searching for files matching specified criteria, downloading them, and then deleting them from Dropbox after processing.

### Authentication methods

This Kamelet requires Dropbox authentication using:

-   **accessToken**: OAuth 2.0 access token for Dropbox API access
    
-   **clientIdentifier**: Your Dropbox App client identifier
    

To obtain these credentials:

1.  Create a Dropbox App in the [Dropbox App Console](https://www.dropbox.com/developers/apps)
    
2.  Generate an access token for your app
    
3.  Use the App Key as the client identifier
    

### Configuration requirements

The Kamelet requires the following mandatory properties:

-   **period**: Polling interval in milliseconds (default: 10000)
    
-   **accessToken**: Dropbox OAuth access token
    
-   **clientIdentifier**: Dropbox App client identifier
    
-   **remotePath**: The folder path in Dropbox to search
    
-   **query**: Search query to filter files
    

### File processing behavior

The Kamelet follows this process:

1.  Searches for files in the specified Dropbox path using the query
    
2.  Downloads each matching file
    
3.  Sends the file content to the sink
    
4.  Deletes the file from Dropbox after successful processing
    

> **Warning**
> Files are permanently deleted from Dropbox after processing. Ensure you have backups if needed.

### Usage examples

Basic file consumption from a Dropbox folder:

```yaml
- route:
    from:
      uri: "kamelet:dropbox-source"
      parameters:
        accessToken: "your-oauth-token"
        clientIdentifier: "your-app-key"
        remotePath: "/inbox"
        query: ".txt"
        period: 30000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Search for specific file types:

```yaml
- route:
    from:
      uri: "kamelet:dropbox-source"
      parameters:
        accessToken: "your-oauth-token"
        clientIdentifier: "your-app-key"
        remotePath: "/documents"
        query: "invoice .pdf"
        period: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/dropbox-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/dropbox-source.kamelet.yaml)
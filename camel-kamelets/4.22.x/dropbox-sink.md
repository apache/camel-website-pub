# ![dropbox sink](_images/kamelets/dropbox-sink.svg) Dropbox Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Upload Files to Dropbox.

## Configuration Options

The following table summarizes the configuration options available for the `dropbox-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Dropbox Access Token | **Required** The access Token to use to access Dropbox. | string |  |  |
| **clientIdentifier** | Client Identifier | **Required** Dropbox App client Identifier. | string |  |  |
| **remotePath** | Remote Path | **Required** Original file or folder to work with. | string |  |  |
| **uploadMode** | Upload Mode | **Required** The uploading mode in case a file with the same name exists on Dropbox. Choose `add` or `force`. With `add`, the new file is renamed. With `force`, the existing file is overwritten. | string | add |  |

## Dependencies

At runtime, the `dropbox-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:dropbox
    
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
            uri: "kamelet:dropbox-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Dropbox Sink Kamelet Description

### Authentication

This Kamelet uses OAuth 2.0 access token authentication to connect to Dropbox. You need to provide: - Access Token: OAuth access token from Dropbox - Client Identifier: Your Dropbox App client identifier

### File Upload Configuration

The Kamelet uploads files to a specified remote path on Dropbox with configurable upload modes: - `add`: Renames the new file if a file with the same name exists - `force`: Overwrites the existing file

### Optional Headers

In the header, you can optionally set the `file` / `ce-file` property to specify the name of the file to upload.

If you do not set the property in the header, the Kamelet uses a default naming convention.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/dropbox-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/dropbox-sink.kamelet.yaml)
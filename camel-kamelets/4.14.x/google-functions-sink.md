# ![google functions sink](_images/kamelets/google-functions-sink.svg) Google Functions Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to Google Functions.

## Configuration Options

The following table summarizes the configuration options available for the `google-functions-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **functionName** | Function Name | **Required** The Function name. | string |  |  |
| **projectId** | Project Id | **Required** The Google Cloud Functions Project ID. | string |  |  |
| **region** | Region | **Required** The region where Google Cloud Functions has been deployed. | string |  |  |
| **serviceAccountKey** | Service Account Key | **Required** The path to the service account key file that provides credentials for the Google Cloud Functions platform. You must encode this value in base64. | binary |  |  |

## Dependencies

At runtime, the `google-functions-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:google-functions
    
-   camel:jackson
    

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
            uri: "kamelet:google-functions-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Google Functions Sink Kamelet Description

### Authentication

This Kamelet uses Google Cloud service account authentication. You must provide a base64-encoded service account key for Google Cloud Functions access.

### Required Configuration

-   **Project ID**: The Google Cloud Functions Project ID
    
-   **Region**: The region where Google Cloud Functions has been deployed
    
-   **Function Name**: The specific function name to invoke
    
-   **Service Account Key**: Base64-encoded service account credentials
    

### Function Invocation

The Kamelet sends data to the specified Google Cloud Function, enabling serverless processing of your data streams.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-functions-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-functions-sink.kamelet.yaml)
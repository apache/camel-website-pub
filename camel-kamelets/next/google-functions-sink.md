# ![google functions sink](_images/kamelets/google-functions-sink.svg) Google Functions Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Calls a function in Google Cloud Functions for each message, with the body as the data of the call.

Use it to hand each message to your own serverless code, for example to enrich, check or store it, without running a web server for it.

Input: the body is the data to call the function with, as text; bytes and streams are read as text. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`.

Output: when it is used inside a route, the body afterwards is the result that the function returned, as text, and the `CamelGoogleCloudFunctionsResponseObject` header holds the whole response of the call.

Good to know: it calls the function through the Cloud Functions API (the `call` method), with the service account key, not through the HTTP address of the function.

## Configuration Options

The following table summarizes the configuration options available for the `google-functions-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **functionName** | Function Name | **Required** The name of the function, as shown in the list of functions in the Google Cloud console. | string |  | process-order |
| **projectId** | Project ID | **Required** The ID of the Google Cloud project where the function is deployed, as shown in the Google Cloud console. It is the project ID, not the project name or number. | string |  | my-project-123 |
| **region** | Region | **Required** The region where the function is deployed. | string |  | us-central1 |
| **serviceAccountKey** | Service Account Key | **Required** The JSON key of a service account that may call the function, such as one with the Cloud Functions Invoker role, encoded in Base64: create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys, then encode the downloaded file, for example with `base64 -w0 key.json`. It is the content of the key file, not its path. | binary |  |  |

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
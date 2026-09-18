# ![google bigquery sink](_images/kamelets/google-bigquery-sink.svg) Google Big Query Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to a Google Big Query table.

## Configuration Options

The following table summarizes the configuration options available for the `google-bigquery-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **dataset** | Big Query Dataset Id | **Required** The Big Query Dataset ID. | string |  |  |
| **projectId** | Google Cloud Project Id | **Required** The Google Cloud Project ID. | string |  |  |
| **serviceAccountKey** | Service Account Key | **Required** The service account key to use as credentials for the BigQuery Service. You must encode this value in base64. | binary |  |  |
| **table** | Big Query Table Id | **Required** The Big Query Table ID. | string |  |  |

## Dependencies

At runtime, the `google-bigquery-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kamelet
    
-   camel:google-bigquery
    
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
            uri: "kamelet:google-bigquery-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Google Big Query Sink Kamelet Description

### Authentication

This Kamelet uses Google Cloud service account authentication. You must provide a base64-encoded service account key for BigQuery access.

### Input Format

This Kamelet expects JSON-formatted data as input for insertion into BigQuery tables.

### Required Configuration

-   **Project ID**: The Google Cloud Project ID
    
-   **Dataset**: The Big Query Dataset ID
    
-   **Table**: The Big Query Table ID
    
-   **Service Account Key**: Base64-encoded service account credentials
    

### Data Processing

The Kamelet automatically unmarshals JSON data using Jackson before sending it to the specified BigQuery table.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-bigquery-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-bigquery-sink.kamelet.yaml)
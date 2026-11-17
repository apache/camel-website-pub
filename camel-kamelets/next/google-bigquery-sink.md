# ![google bigquery sink](_images/kamelets/google-bigquery-sink.svg) Google Big Query Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Inserts each message as one or more rows into a table in Google BigQuery.

Use it to load events or records into BigQuery for analytics and reports, such as orders, page views or sensor readings, as they happen.

Input: the body is JSON text: a JSON object for one row, or a JSON array of objects for several rows. The names of the fields are the names of the columns of the table, such as `{"id": 1, "item": "book"}`.

Output: when it is used inside a route, the body afterwards is the parsed JSON: a Map for one row, or a List of Maps.

Good to know: the table must exist with its columns. A message with a field that is not a column of the table, or with a body that is not JSON, fails, and none of its rows are inserted.

## Configuration Options

The following table summarizes the configuration options available for the `google-bigquery-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **dataset** | BigQuery Dataset ID | **Required** The ID of the dataset that holds the table, as shown in the BigQuery console. | string |  | shop |
| **projectId** | Google Cloud Project ID | **Required** The ID of the Google Cloud project that holds the dataset, as shown in the Google Cloud console. It is the project ID, not the project name or number. | string |  | my-project-123 |
| **serviceAccountKey** | Service Account Key | **Required** The JSON key of a service account that may insert rows into the table, such as one with the BigQuery Data Editor role, encoded in Base64: create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys, then encode the downloaded file, for example with `base64 -w0 key.json`. | binary |  |  |
| **table** | BigQuery Table ID | **Required** The ID of the table to insert the rows into, without the project and dataset. | string |  | orders |

## Dependencies

At runtime, the `google-bigquery-sink` Kamelet relies upon the presence of the following dependencies:

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

This Kamelet expects JSON text as input: a JSON object for one row, or a JSON array of objects for several rows. The names of the fields are the names of the columns of the table, for example `{"id": 1, "item": "book"}`. A field that is not a column of the table fails the message.

### Required Configuration

-   **Project ID**: The Google Cloud Project ID
    
-   **Dataset**: The Big Query Dataset ID
    
-   **Table**: The Big Query Table ID
    
-   **Service Account Key**: Base64-encoded service account credentials
    

### Data Processing

The Kamelet automatically unmarshals JSON data using Jackson before sending it to the specified BigQuery table.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-bigquery-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-bigquery-sink.kamelet.yaml)
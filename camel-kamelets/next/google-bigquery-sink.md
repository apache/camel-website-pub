# ![google bigquery sink](_images/kamelets/google-bigquery-sink.svg) Google Big Query Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Inserts each message as one or more rows into a table in Google BigQuery.

Use it to load events or records into BigQuery for analytics and reports, such as orders, page views or sensor readings, as they happen.

Input: the body is a JSON object for one row, or a JSON array of objects for several rows, as JSON text, or as a Map or a List of Maps, which is written as JSON. The names of the fields are the names of the columns of the table, such as `{"id": 1, "item": "book"}`.

Output: when it is used inside a route, the body afterwards is the parsed JSON: a Map for one row, or a List of Maps, and the `Content-Type` header is `application/json`.

Good to know: the table must exist with its columns. A message with a field that is not a column of the table, or with a body that is not JSON, fails, and none of its rows are inserted. Headers that start with `CamelGoogleBigQuery` are removed from the message first, so they cannot change what the Kamelet does. A message that is sent again, for example after a failure, adds its rows again, unless `useAsInsertId` names a field that identifies each row.

## Configuration Options

The following table summarizes the configuration options available for the `google-bigquery-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **dataset** | BigQuery Dataset ID | **Required** The ID of the dataset that holds the table, as shown in the BigQuery console. | string |  | shop |
| **projectId** | Google Cloud Project ID | **Required** The ID of the Google Cloud project that holds the dataset, as shown in the Google Cloud console. It is the project ID, not the project name or number. | string |  | my-project-123 |
| **serviceAccountKey** | Service Account Key | **Required** The JSON key of a service account that may insert rows into the table, such as one with the BigQuery Data Editor role, encoded in Base64: create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys, then encode the downloaded file, for example with `base64 -w0 key.json`. | binary |  |  |
| **table** | BigQuery Table ID | **Required** The ID of the table to insert the rows into, without the project and dataset. | string |  | orders |
| **useAsInsertId** | Insert ID Field | The name of a field of each row whose value is sent as the insert ID of the row, such as `orderId`. BigQuery uses the insert ID to drop, on a best-effort basis, a row that it received with the same insert ID shortly before, such as a message sent again after a failed attempt. The field must hold text, such as `"o-1001"`; a message with a row whose field holds a number fails, and none of its rows are inserted. A row without the field is sent without an insert ID. When it is not set, no row has an insert ID, and a row sent twice is added twice. | string |  | orderId |

## Dependencies

At runtime, the `google-bigquery-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:google-bigquery
    
-   camel:jackson3
    

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

### Insert IDs

A message that is sent again, for example after a failure, adds its rows again. With `useAsInsertId`, the value of a field of each row is sent as the insert ID of the row, and BigQuery uses it to drop, on a best-effort basis, a row that it received with the same insert ID shortly before. The field must hold text: a message with a row whose field holds a number fails. A row without the field is sent without an insert ID.

```yaml
- to:
    uri: "kamelet:google-bigquery-sink"
    parameters:
      projectId: "my-project-123"
      dataset: "shop"
      table: "orders"
      serviceAccountKey: "{{gcp.serviceAccountKey}}"
      useAsInsertId: "orderId"
```

For a body such as `{"orderId": "o-1001", "item": "book"}`, the insert ID of the row is `o-1001`. In a JSON array, each row gets the insert ID of its own field.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-bigquery-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-bigquery-sink.kamelet.yaml)
# Google BigQuery

JVM since1.0.0 Native since1.6.0

Access Google Cloud BigQuery service using SQL queries or Google Client Services API

## What’s inside

-   [Google BigQuery component](../../../../components/4.18.x/google-bigquery-component.md), URI syntax: `google-bigquery:projectId:datasetId:tableId`
    
-   [Google BigQuery Standard SQL component](../../../../components/4.18.x/google-bigquery-sql-component.md), URI syntax: `google-bigquery-sql:projectId:queryString`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-google-bigquery)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-google-bigquery</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

If you want to read SQL scripts from the classpath with `google-bigquery-sql` in native mode, then you will need to ensure that they are added to the native image via the `quarkus.native.resources.includes` configuration property. Please check [Quarkus documentation](https://quarkus.io/guides/building-native-image#quarkus-native-pkg-native-config_quarkus.native.resources.includes) for more details.
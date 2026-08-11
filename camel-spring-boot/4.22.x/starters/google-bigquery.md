# Google BigQuery

Google BigQuery data warehouse for analytics.

## What’s inside

-   [Google BigQuery component](../../../components/4.22.x/google-bigquery-component.md), URI syntax: `google-bigquery:projectId:datasetId:tableId`
    
-   [Google BigQuery Standard SQL component](../../../components/4.22.x/google-bigquery-sql-component.md), URI syntax: `google-bigquery-sql:projectId:queryString`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-google-bigquery-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.component.google-bigquery-sql.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.google-bigquery-sql.connection-factory | ConnectionFactory to obtain connection to Bigquery Service. If not provided the default one will be used. The option is a org.apache.camel.component.google.bigquery.GoogleBigQueryConnectionFactory type. |  | GoogleBigQueryConnectionFactory |
| camel.component.google-bigquery-sql.enabled | Whether to enable auto configuration of the google-bigquery-sql component. This is enabled by default. |  | Boolean |
| camel.component.google-bigquery-sql.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.google-bigquery-sql.project-id | Google Cloud Project Id |  | String |
| camel.component.google-bigquery.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.google-bigquery.connection-factory | ConnectionFactory to obtain connection to Bigquery Service. If not provided the default one will be used. The option is a org.apache.camel.component.google.bigquery.GoogleBigQueryConnectionFactory type. |  | GoogleBigQueryConnectionFactory |
| camel.component.google-bigquery.dataset-id | BigQuery Dataset Id |  | String |
| camel.component.google-bigquery.enabled | Whether to enable auto configuration of the google-bigquery component. This is enabled by default. |  | Boolean |
| camel.component.google-bigquery.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.google-bigquery.project-id | Google Cloud Project Id |  | String |
# ![salesforce composite upsert sink](_images/kamelets/salesforce-composite-upsert-sink.svg) Salesforce composite upsert Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Upsert Composite List of sObjects in Salesforce.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-composite-upsert-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The Salesforce application consumer key. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The Salesforce application consumer secret. | string |  |  |
| **password** | Password | **Required** The Salesforce user password. | string |  |  |
| **sObjectIdName** | Object Id Name | **Required** The Field Name of the External ID of the Salesforce object. Required if using a key-value pair. | string |  |  |
| **sObjectName** | Object Name | **Required** The type of the Salesforce object. Required if using a key-value pair. | string |  | Contact |
| **userName** | Username | **Required** The Salesforce username. | string |  |  |
| **loginUrl** | Login URL | The Salesforce instance login URL. | string | [https://login.salesforce.com](https://login.salesforce.com) |  |

## Dependencies

At runtime, the `salesforce-composite-upsert-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:jsonpath
    
-   camel:jackson
    
-   camel:salesforce
    
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
            uri: "kamelet:salesforce-composite-upsert-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Salesforce Composite Upsert Sink Kamelet Description

### Salesforce CRM Integration

This Kamelet integrates with Salesforce CRM using composite upsert operations. Composite operations allow multiple records to be processed in a single API call, improving efficiency and reducing API usage.

### Upsert Operations

Performs upsert (insert or update) operations that create new records if they don’t exist or update existing records based on external ID fields. This provides flexible data synchronization capabilities.

### Batch Processing

Composite operations enable batch processing of multiple records in a single request, reducing API call overhead and improving performance for bulk data operations.

### External ID Matching

Uses external ID fields for record matching, allowing integration with external systems while maintaining data relationships and avoiding duplicate records.

### API Efficiency

Salesforce composite operations optimize API usage by:

-   Reducing the number of API calls
    
-   Minimizing network round trips
    
-   Improving overall integration performance
    
-   Supporting bulk data operations
    

### Error Handling

Provides detailed error information for each record in the composite operation, enabling granular error handling and data quality management.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-composite-upsert-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-composite-upsert-sink.kamelet.yaml)
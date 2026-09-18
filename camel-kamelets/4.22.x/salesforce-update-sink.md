# ![salesforce update sink](_images/kamelets/salesforce-update-sink.svg) Salesforce Update Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Update an object in Salesforce.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-update-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The Salesforce application consumer key. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The Salesforce application consumer secret. | string |  |  |
| **password** | Password | **Required** The Salesforce user password. | string |  |  |
| **userName** | Username | **Required** The Salesforce username. | string |  |  |
| **loginUrl** | Login URL | The Salesforce instance login URL. | string | [https://login.salesforce.com](https://login.salesforce.com) |  |

## Dependencies

At runtime, the `salesforce-update-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:salesforce-update-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Salesforce Update Sink Kamelet Description

### Salesforce CRM Integration

This Kamelet integrates with Salesforce CRM to update existing records in Salesforce objects. It provides efficient record modification capabilities through Salesforce’s REST API.

### Record Updates

Updates existing records in specified Salesforce objects using record IDs or external ID fields. Supports partial updates where only modified fields are updated.

### Field-Level Updates

Enables selective field updates without affecting other record fields, providing granular control over data modifications and preserving unchanged data.

### Optimistic Locking

Salesforce provides optimistic locking mechanisms to prevent conflicts when multiple systems attempt to update the same record simultaneously.

### Validation and Workflow

Updated records are subject to Salesforce’s validation rules, workflow rules, and triggers, ensuring business logic enforcement and data integrity.

### Audit Trail

Salesforce maintains comprehensive audit trails for record updates, including:

-   Field history tracking
    
-   User identification
    
-   Timestamp information
    
-   Before and after values
    

### Integration Patterns

Supports various integration patterns including:

-   Real-time data synchronization
    
-   Batch update operations
    
-   Event-driven updates
    
-   Scheduled data maintenance
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-update-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-update-sink.kamelet.yaml)
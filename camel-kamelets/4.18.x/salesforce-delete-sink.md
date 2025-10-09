# ![salesforce delete sink](_images/kamelets/salesforce-delete-sink.svg) Salesforce Delete Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Remove an object from Salesforce.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-delete-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The Salesforce application consumer key. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The Salesforce application consumer secret. | string |  |  |
| **password** | Password | **Required** The Salesforce user password. | string |  |  |
| **userName** | Username | **Required** The Salesforce username. | string |  |  |
| **loginUrl** | Login URL | The Salesforce instance login URL. | string | [https://login.salesforce.com](https://login.salesforce.com) |  |

## Dependencies

At runtime, the `salesforce-delete-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:salesforce
    
-   camel:kamelet
    
-   camel:core
    
-   camel:jsonpath
    

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
            uri: "kamelet:salesforce-delete-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Salesforce Delete Sink Kamelet Description

### Salesforce CRM Integration

This Kamelet integrates with Salesforce CRM to delete records from Salesforce objects. It provides secure record deletion capabilities through Salesforce’s REST API.

### Record Deletion

Deletes records from specified Salesforce objects using record IDs or external ID fields. Supports deletion of records from any accessible Salesforce object.

### Safety and Recovery

Salesforce provides safety mechanisms for deleted records:

-   Deleted records are moved to the Recycle Bin
    
-   Records can be restored within the retention period
    
-   Audit trails maintain deletion history
    

### Cascade Effects

Considers Salesforce’s cascade deletion rules and relationships when deleting records, ensuring referential integrity and proper handling of related data.

### Bulk Operations

Can be used for both individual record deletions and bulk deletion operations, depending on the integration requirements and data volume.

### Permission Controls

Respects Salesforce’s object-level and field-level security settings, ensuring that only authorized operations are performed based on user permissions.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-delete-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-delete-sink.kamelet.yaml)
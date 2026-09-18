# ![insert field action](_images/kamelets/insert-field-action.svg) Insert Field Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Adds a custom field with a simple language parsed value to the message in transit.

## Configuration Options

The following table summarizes the configuration options available for the `insert-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **field** | Field | **Required** The name of the field to be added. | string |  |  |
| **value** | Value | **Required** The value of the field. | string |  |  |

## Dependencies

At runtime, the `insert-field-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:jackson
    
-   camel:kamelet
    
-   camel:kafka
    

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
            uri: "kamelet:insert-field-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/insert-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/insert-field-action.kamelet.yaml)
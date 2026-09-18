# ![mask field action](_images/kamelets/mask-field-action.svg) Mask Fields Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Mask fields with a constant value in the message in transit.

## Configuration Options

The following table summarizes the configuration options available for the `mask-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **fields** | Fields | **Required** Comma separated list of fields to mask. | string |  |  |
| **replacement** | Replacement | **Required** Replacement for the fields to be masked. | string |  |  |

## Dependencies

At runtime, the `mask-field-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:core
    
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
            uri: "kamelet:mask-field-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mask-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mask-field-action.kamelet.yaml)
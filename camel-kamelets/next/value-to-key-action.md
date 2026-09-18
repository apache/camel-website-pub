# ![value to key action](_images/kamelets/value-to-key-action.svg) Value to Key Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Replace the Kafka record key with a new key formed from a fields subset coming from the message body.

## Configuration Options

The following table summarizes the configuration options available for the `value-to-key-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **fields** | Fields | **Required** Comma separated list of fields to be used to form the new key. | string |  |  |

## Dependencies

At runtime, the `value-to-key-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:value-to-key-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/value-to-key-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/value-to-key-action.kamelet.yaml)
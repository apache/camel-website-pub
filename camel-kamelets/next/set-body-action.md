# ![set body action](_images/kamelets/set-body-action.svg) Set Body Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sets a simple language parsed value as the new message body in transit.

## Configuration Options

The following table summarizes the configuration options available for the `set-body-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **value** | Value | **Required** The value to set as new body. | string |  |  |

## Dependencies

At runtime, the `set-body-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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
            uri: "kamelet:set-body-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/set-body-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/set-body-action.kamelet.yaml)
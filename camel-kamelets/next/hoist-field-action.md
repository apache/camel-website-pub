# ![hoist field action](_images/kamelets/hoist-field-action.svg) Hoist Field Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Wrap data in a single field.

## Configuration Options

The following table summarizes the configuration options available for the `hoist-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **field** | Field | **Required** The name of the field that will contain the event. | string |  |  |

## Dependencies

At runtime, the `hoist-field-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:hoist-field-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/hoist-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/hoist-field-action.kamelet.yaml)
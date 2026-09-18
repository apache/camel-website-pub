# ![velocity template action](_images/kamelets/velocity-template-action.svg) Velocity Template Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Apply a Velocity Template.

## Configuration Options

The following table summarizes the configuration options available for the `velocity-template-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Template | **Required** The inline template. | string |  | file:////template.vm |

## Dependencies

At runtime, the `velocity-template-action` Kamelet relies upon the presence of the following dependencies:

-   camel:velocity
    
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
            uri: "kamelet:velocity-template-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/velocity-template-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/velocity-template-action.kamelet.yaml)
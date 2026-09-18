# ![jolt transformation action](_images/kamelets/jolt-transformation-action.svg) Jolt Transformation Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Apply a Jolt Transformation.

## Configuration Options

The following table summarizes the configuration options available for the `jolt-transformation-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Template | **Required** The inline template. | string |  | file:////template.json |
| **transform** | Transform DSL | Specifies the Transform DSL of the endpoint resource. If none is specified, Chainr is used. Enum values: \* Chainr \* Shiftr \* Defaultr \* Removr \* Sortr | string | Chainr |  |

## Dependencies

At runtime, the `jolt-transformation-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jolt
    
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
            uri: "kamelet:jolt-transformation-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jolt-transformation-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jolt-transformation-action.kamelet.yaml)
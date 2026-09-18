# ![json patch action](_images/kamelets/json-patch-action.svg) Json Patch Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Apply a Json Patch Transformation.

## Configuration Options

The following table summarizes the configuration options available for the `json-patch-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Template | **Required** The json patch transformation. | string |  | file:////template.json |

## Dependencies

At runtime, the `json-patch-action` Kamelet relies upon the presence of the following dependencies:

-   camel:json-patch
    
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
            uri: "kamelet:json-patch-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/json-patch-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/json-patch-action.kamelet.yaml)
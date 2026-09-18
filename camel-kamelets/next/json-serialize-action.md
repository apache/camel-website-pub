# ![json serialize action](_images/kamelets/json-serialize-action.svg) Json Serialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Serialize payload to JSON.

## Configuration Options

The `json-serialize-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `json-serialize-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    
-   camel:jackson
    

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
            uri: "kamelet:json-serialize-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/json-serialize-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/json-serialize-action.kamelet.yaml)
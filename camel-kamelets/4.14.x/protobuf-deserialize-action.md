# ![protobuf deserialize action](_images/kamelets/protobuf-deserialize-action.svg) Protobuf Deserialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Deserialize payload to Protobuf.

## Configuration Options

The following table summarizes the configuration options available for the `protobuf-deserialize-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **schema** | Schema | The Protobuf schema to use during serialization (as single-line). | string |  | message Person { required string first = 1; required string last = 2; } |

## Dependencies

At runtime, the `protobuf-deserialize-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    
-   camel:jackson-protobuf
    

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
            uri: "kamelet:protobuf-deserialize-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/protobuf-deserialize-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/protobuf-deserialize-action.kamelet.yaml)
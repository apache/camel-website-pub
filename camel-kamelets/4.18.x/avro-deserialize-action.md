# ![avro deserialize action](_images/kamelets/avro-deserialize-action.svg) Avro Deserialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Deserialize payload to Avro.

## Configuration Options

The following table summarizes the configuration options available for the `avro-deserialize-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **schema** | Schema | The Avro schema to use during serialization (as single-line, using JSON format). | string |  | {"type": "record", "namespace": "com.example", "name": "FullName", "fields": \[{"name": "first", "type": "string"},{"name": "last", "type": "string"}\]} |
| **validate** | Validate | Indicates if the content must be validated against the schema. | boolean | true |  |

## Dependencies

At runtime, the `avro-deserialize-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    
-   camel:jackson-avro
    

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
            uri: "kamelet:avro-deserialize-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/avro-deserialize-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/avro-deserialize-action.kamelet.yaml)
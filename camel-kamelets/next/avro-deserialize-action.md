# ![avro deserialize action](_images/kamelets/avro-deserialize-action.svg) Avro Deserialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Turns each message of Avro binary data back into a JSON object, using the Avro schema the data was written with.

Use it to read records that arrive in Avro, a compact binary format described by a schema, for example from a Kafka topic, and work on them as JSON. To turn JSON into Avro, use `avro-serialize-action`; for Protobuf, use `protobuf-deserialize-action`.

Input: Avro binary data, as bytes, without the schema in it, such as `avro-serialize-action` writes.

Output: the body is parsed JSON (a Jackson `JsonNode`) with one field for each field of the schema. The `Content-Type` header is removed. Put `json-serialize-action` after this action to get JSON text.

Good to know: Avro data does not say which schema it was written with, so the schema must be the one the writer used. When `schema` is not set, the schema found by an earlier `resolve-pojo-schema-action` is used.

## Configuration Options

The following table summarizes the configuration options available for the `avro-deserialize-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **schema** | Schema | The Avro schema the data was written with, as JSON text: a record with a name and a list of fields, each with a name and a type. When it is not set, the schema found by an earlier `resolve-pojo-schema-action` is used. | string |  | {"type": "record", "namespace": "com.example", "name": "FullName", "fields": \[{"name": "first", "type": "string"},{"name": "last", "type": "string"}\]} |
| **validate** | Validate | Meant to turn the check of the content against the schema on or off. It has no effect. | boolean | true |  |

## Dependencies

At runtime, the `avro-deserialize-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
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
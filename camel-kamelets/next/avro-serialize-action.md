# ![avro serialize action](_images/kamelets/avro-serialize-action.svg) Avro Serialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Turns each message, a JSON object, into Avro binary data that follows the Avro schema you give.

Use it to send records in Avro, a compact binary format described by a schema, to a system that expects it, such as a Kafka topic whose readers decode Avro. To turn Avro back into JSON, use `avro-deserialize-action`; for Protobuf, use `protobuf-serialize-action`.

Input: parsed JSON (a Map or a Jackson `JsonNode`) whose fields match the schema. JSON text fails: put `json-deserialize-action` before this action to parse it.

Output: the body is the Avro binary data, as bytes, and the `Content-Type` header is set to `application/avro`.

Good to know: the schema is not written into the data, so whoever reads it needs the same schema. A message fails when it lacks a field of the schema, has a field the schema does not know, or has a value of the wrong type. When `schema` is not set, the schema found by an earlier `resolve-pojo-schema-action` is used.

## Configuration Options

The following table summarizes the configuration options available for the `avro-serialize-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **schema** | Schema | The Avro schema of the records, as JSON text: a record with a name and a list of fields, each with a name and a type. When it is not set, the schema found by an earlier `resolve-pojo-schema-action` is used. | string |  | {"type": "record", "namespace": "com.example", "name": "FullName", "fields": \[{"name": "first", "type": "string"},{"name": "last", "type": "string"}\]} |
| **validate** | Validate | Meant to turn the check of the content against the schema on or off. It has no effect: a message that does not match the schema always fails. | boolean | true |  |

## Dependencies

At runtime, the `avro-serialize-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:jackson3-avro
    

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
            uri: "kamelet:avro-serialize-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/avro-serialize-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/avro-serialize-action.kamelet.yaml)
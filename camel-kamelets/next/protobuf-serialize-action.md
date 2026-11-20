# ![protobuf serialize action](_images/kamelets/protobuf-serialize-action.svg) Protobuf Serialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Turns each message, a JSON object, into Protobuf binary data that follows the Protobuf schema you give.

Use it to send records in Protocol Buffers (Protobuf), a compact binary format described by a schema, to a system that expects it, such as a Kafka topic whose readers decode Protobuf. To turn Protobuf back into JSON, use `protobuf-deserialize-action`; for Avro, use `avro-serialize-action`.

Input: parsed JSON (a Map or a Jackson `JsonNode`) whose fields match the schema. JSON text fails: put `json-deserialize-action` before this action to parse it.

Output: the body is the Protobuf binary data, as a stream, and the `Content-Type` header is set to `application/protobuf`.

Good to know: a message fails when it has a field the schema does not know or a value of the wrong type; a field of the schema that the message lacks is left out, even when it is marked `required`. When `schema` is not set, the schema found by an earlier `resolve-pojo-schema-action` is used.

## Configuration Options

The following table summarizes the configuration options available for the `protobuf-serialize-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **schema** | Schema | The Protobuf schema of the records, in the `.proto` language: a `message` with its fields, each with a type, a name and a number. When it is not set, the schema found by an earlier `resolve-pojo-schema-action` is used. | string |  | message Person { required string first = 1; required string last = 2; } |

## Dependencies

At runtime, the `protobuf-serialize-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:jackson3-protobuf
    

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
            uri: "kamelet:protobuf-serialize-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/protobuf-serialize-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/protobuf-serialize-action.kamelet.yaml)
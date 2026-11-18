# ![protobuf deserialize action](_images/kamelets/protobuf-deserialize-action.svg) Protobuf Deserialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Turns each message of Protobuf binary data back into a JSON object, using the Protobuf schema the data was written with.

Use it to read records that arrive in Protocol Buffers (Protobuf), a compact binary format described by a schema, and work on them as JSON. To turn JSON into Protobuf, use `protobuf-serialize-action`; for Avro, use `avro-deserialize-action`.

Input: Protobuf binary data, as bytes, such as `protobuf-serialize-action` writes.

Output: the body is parsed JSON (a Jackson `JsonNode`) with the fields found in the data. The `Content-Type` header is removed. Put `json-serialize-action` after this action to get JSON text.

Good to know: a body that is not Protobuf data, such as JSON text, fails. When `schema` is not set, the schema found by an earlier `resolve-pojo-schema-action` is used.

## Configuration Options

The following table summarizes the configuration options available for the `protobuf-deserialize-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **schema** | Schema | The Protobuf schema the data was written with, in the `.proto` language: a `message` with its fields, each with a type, a name and a number. When it is not set, the schema found by an earlier `resolve-pojo-schema-action` is used. | string |  | message Person { required string first = 1; required string last = 2; } |

## Dependencies

At runtime, the `protobuf-deserialize-action` Kamelet relies upon the presence of the following dependencies:

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
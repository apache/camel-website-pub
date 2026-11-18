# ![resolve pojo schema action](_images/kamelets/resolve-pojo-schema-action.svg) Resolve Schema Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Attaches an Avro, Protobuf or JSON schema to each message, for the later steps that need one, and leaves the body unchanged.

Use it to give the schema once, before `data-type-action` with a format such as `avro-binary` or `protobuf-binary`, which takes its schema only from here. `avro-serialize-action`, `avro-deserialize-action`, `protobuf-serialize-action` and `protobuf-deserialize-action` use it too when their own `schema` is not set.

Input: any body. The schema comes from `schema`, or else from the Java class named by `contentClass`.

Output: the body and the headers are unchanged. The schema is kept with the message in the properties `X-Content-Schema` and `X-Content-Schema-Type` (`avsc`, `proto` or `json`), which are not headers and are not sent to other systems.

Good to know: with the default `mimeType`, `application/json`, and no `schema` or `contentClass`, it does nothing. A `mimeType` it does not know makes every message fail with "Unsupported type".

## Configuration Options

The following table summarizes the configuration options available for the `resolve-pojo-schema-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **contentClass** | Content Class | The full name of a Java class in the application whose fields define the schema. Only used when `schema` is not set. | string |  | com.example.Order |
| **mimeType** | MIME Type | Which kind of schema `schema` holds and later steps need: `avro/binary`, `application/avro` or `avro/x-struct` for Avro; `protobuf/binary`, `application/protobuf` or `protobuf/x-struct` for Protobuf; `application/json` or `application/x-struct` for JSON Schema. With `application/x-java-object`, the kind is taken from `targetMimeType`. | string | application/json | avro/binary |
| **schema** | Schema | The schema itself: for Avro, JSON text such as the example; for Protobuf, a `message` in the `.proto` language; for JSON, a JSON Schema as JSON text. When it is not set, the schema is made from `contentClass`. | string |  | {"type": "record", "namespace": "com.example", "name": "FullName", "fields": \[{"name": "first", "type": "string"},{"name": "last", "type": "string"}\]} |
| **targetMimeType** | Target MIME Type | The kind of schema to find, as in `mimeType`, such as `avro/binary`. Only used when `mimeType` is `application/x-java-object`. | string |  | avro/binary |

## Dependencies

At runtime, the `resolve-pojo-schema-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:jackson3-avro
    
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
            uri: "kamelet:resolve-pojo-schema-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/resolve-pojo-schema-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/resolve-pojo-schema-action.kamelet.yaml)
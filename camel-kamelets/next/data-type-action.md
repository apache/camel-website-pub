# ![data type action](_images/kamelets/data-type-action.svg) Data Type Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Converts the body of each message into the data type you name, such as plain text, bytes, JSON, Avro or Protobuf, and sets the `Content-Type` header to match.

Use it to give the next step the kind of body it needs, such as bytes for a sink that writes files, or to turn JSON into Avro binary data after `resolve-pojo-schema-action` has found the schema. A data type is a name for a kind of body together with the conversion into it; `camel catalog transformer` lists the names.

Input: `text-plain` and `application-octet-stream` take any text; `application-json` and `application-x-struct` take JSON text; `avro-binary` and `protobuf-binary` take a JSON object, as JSON text or a Jackson `JsonNode` but not a Map; `avro-x-struct` and `protobuf-x-struct` take Avro or Protobuf binary data.

Output: `text-plain` gives text (`Content-Type` `text/plain`); `application-octet-stream` bytes (`application/octet-stream`); `application-json` JSON text as bytes (`application/json`); the `x-struct` ones parsed JSON, a Jackson `JsonNode` (`application/x-struct`); `avro-binary` and `protobuf-binary` binary data (`avro/binary`, `protobuf/binary`). `application-cloudevents+json` wraps the body, under `data`, in a CloudEvents JSON envelope.

Good to know: a name that does not exist makes every message fail, and so do the Avro and Protobuf data types without a schema from an earlier `resolve-pojo-schema-action`. With `text-plain`, a Map becomes text such as `{id=1, name=Ann}`, not JSON.

## Configuration Options

The following table summarizes the configuration options available for the `data-type-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **format** | Data Type Format | **Required** The name of the data type to convert the body into, such as `text-plain`, `application-octet-stream`, `application-json`, `application-x-struct`, `avro-binary`, `avro-x-struct`, `protobuf-binary`, `protobuf-x-struct` or `application-cloudevents+json`. `camel catalog transformer` lists them all; for the names written `scheme:format`, such as `aws2-s3:application-cloudevents`, put the part before the colon in `scheme`. | string |  | application-json |
| **scheme** | Component Scheme | The name of a system, as Camel names it, such as `aws2-s3`, to use the data type made for that system instead of the general one. With `aws2-s3` and the format `application-cloudevents`, the data type `aws2-s3:application-cloudevents` is used. Leave it empty for the general data types. | string |  | aws2-s3 |

## Dependencies

At runtime, the `data-type-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:data-type-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/data-type-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/data-type-action.kamelet.yaml)
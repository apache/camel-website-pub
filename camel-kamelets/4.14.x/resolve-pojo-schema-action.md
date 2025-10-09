# ![resolve pojo schema action](_images/kamelets/resolve-pojo-schema-action.svg) Resolve Schema Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Resolves schema from given mime type and payload. Sets the resolved schema, the schema type and its content class as properties for later reference.

## Configuration Options

The following table summarizes the configuration options available for the `resolve-pojo-schema-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **contentClass** | Content Class | Type information of the content object. Fully qualified class name. | string |  | org.apache.camel.content.Foo |
| **mimeType** | Mime Type | The mime type to determine the schema resolver implementation that should perform the operation. | string | application/json | application/json |
| **schema** | Schema | Optional schema content (as single-line, using JSON format). | string |  |  |
| **targetMimeType** | Target Mime Type | Additional mime type information used to determine the schema resolver. Usually only used in combination with mime type "application/x-java-object". | string |  | application/json |

## Dependencies

At runtime, the `resolve-pojo-schema-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    
-   camel:jackson-avro
    
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
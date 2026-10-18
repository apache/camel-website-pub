# JSonApi

**Since Camel 3.0**

The JSonApi dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **dataFormatTypes** (common) |  | `String` | The classes to take into account for the marshalling. Multiple classes can be separated by comma. |
| **mainFormatType** (common) |  | `String` | The class to take into account while unmarshalling. |

## Usage

The `dataFormatTypes` are the resource classes, separated by commas. They are annotated with `@Type` and `@Id` of the JSONAPI-Converter library. On unmarshal, `mainFormatType` is the class of the primary data of the document:

```yaml
- route:
    from:
      uri: direct:marshal
      steps:
        - marshal:
            jsonApi:
              dataFormatTypes: com.example.Book,com.example.Author
        - to:
            uri: mock:marshal
- route:
    from:
      uri: direct:unmarshal
      steps:
        - unmarshal:
            jsonApi:
              dataFormatTypes: com.example.Book,com.example.Author
              mainFormatType: com.example.Book
        - to:
            uri: mock:unmarshal
```

## Dependencies

To use JsonAPI in your Camel routes, you need to add the dependency on **camel-jsonapi** which implements this data format.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-jsonapi</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```
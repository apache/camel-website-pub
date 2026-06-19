# JSON Gson

**Since Camel 2.10**

Gson is a Data Format that uses the [Gson Library](https://github.com/google/gson)

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .marshal().json(JsonLibrary.Gson)
    .to("mqseries:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <marshal><json library="Gson"/></marshal>
  <to uri="mqseries:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - marshal:
            json:
              library: Gson
        - to:
            uri: mqseries:Another.Queue
```

## Gson Options

The JSON Gson dataformat supports 4 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **prettyPrint** (common) | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |
| **contentTypeHeader** (common) | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |
| **dateFormatPattern** (common) |  | `String` | To configure the date format while marshall or unmarshall Date fields in JSON using Gson. |

## Dependencies

To use Gson in your camel routes, you need to add the dependency on **camel-gson** which implements this data format.

If you use maven, you could add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-gson</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```
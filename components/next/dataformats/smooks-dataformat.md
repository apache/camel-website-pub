# Smooks

**Since Camel 4.9**

The Smooks Data Format uses [Smooks](https://www.smooks.org/) to transform from one data format to another and back again. A configuration for a Smooks Data Format should not allocate system resources because the data format does not close those resources. Use this data format when you are primarily interested in transformation and binding; not other Smooks features like routing. The latter should be done with the [Smooks component](../../4.22.x/smooks-component.md).

Maven users will need to add the following dependency to their `pom.xml` for this data format:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-smooks</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Usage

Below is an example of using the Smooks Data Format to unmarshal a CSV into a `java.util.List` of `org.smooks.example.Customer` instances:

-   Java
    
-   YAML
    

```java
from("direct:unmarshal")
    .unmarshal().smooks("csv-smooks-unmarshal-config.xml")
    .log("Unmarshalled customers: ${body}");
```

```yaml
- route:
    from:
      uri: direct:unmarshal
      steps:
        - unmarshal:
            smooks:
              smooksConfig: csv-smooks-unmarshal-config.xml
        - log:
            message: "Unmarshalled customers: ${body}"
```

The Smooks configuration in `csv-smooks-unmarshal-config.xml` is as follows:

```xml
<smooks-resource-list xmlns="https://www.smooks.org/xsd/smooks-2.0.xsd"
	xmlns:core="https://www.smooks.org/xsd/smooks/smooks-core-1.6.xsd"
	xmlns:csv="https://www.smooks.org/xsd/smooks/csv-1.7.xsd">

    <core:exports>
        <core:result type="org.smooks.io.sink.JavaSink" extract="result"/>
    </core:exports>

    <csv:reader fields="firstName,lastName,gender,age,country">
        <csv:listBinding beanId="result" class="org.smooks.example.Customer"/>
    </csv:reader>

</smooks-resource-list>
```

## Smooks Data Format Options

The Smooks dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **smooksConfig** (common) |  | `String` | **Required** Path to the Smooks configuration file. |
| **allowExternalEntities** (security) | `false` | `Boolean` | Whether to allow the XML reader used by Smooks to resolve external XML entities (external general and parameter entities) when parsing XML input. This is disabled by default so that external entities in the message body are not resolved; enable it only for trusted legacy configurations that rely on external entity resolution. |

## Message Body

The message body at each side of the Smooks data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `map`, `list` or `pojo` | A Java object graph, such as the beans unmarshal gives, which Smooks reads as a JavaSource. Text, bytes or a stream are not parsed: Smooks reads them as a Java object too. |
| **Marshal output** | `stream` | The text Smooks writes in UTF-8, such as the XML of the object graph or the output of a template of the config, in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file` | The data the reader of the smooks config reads: XML by default, or EDI, CSV or JSON with a reader. |
| **Unmarshal output** | `unknown` | What the exports of the smooks config give: the bean a JavaSink export extracts (a Map of the beans when it extracts several or none), the text of a StringSink, or a List of the results of several exports (empty without exports). |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../../manual/body-types.md).
# Smooks

**Since Camel 4.9**

The Smooks Data Format uses [Smooks](https://www.smooks.org/) to transform from one data format to another and back again. A configuration for a Smooks Data Format should not allocate system resources because the data format does not close those resources. Use this data format when you are primarily interested in transformation and binding; not other Smooks features like routing. The latter should be done with the [Smooks component](../smooks-component.md).

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
- from:
    uri: direct:unmarshal
    steps:
      - unmarshal:
          smooks:
            smooksConfig: csv-smooks-unmarshal-config.xml
      - log: "Unmarshalled customers: ${body}"
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

The Smooks dataformat supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **smooksConfig** (common) |  | `String` | **Required** Path to the Smooks configuration file. |

## Spring Boot Auto-Configuration

When using smooks with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-smooks-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.smooks.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.smooks.enabled** | Whether to enable auto configuration of the smooks component. This is enabled by default. |  | Boolean |
| **camel.component.smooks.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.smooks.smooks-factory** | To use a custom factory for creating Smooks. The option is a org.smooks.SmooksFactory type. |  | SmooksFactory |
| **camel.dataformat.smooks.enabled** | Whether to enable auto configuration of the smooks data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.smooks.smooks-config** | Path to the Smooks configuration file. |  | String |
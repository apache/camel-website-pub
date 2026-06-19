# Smooks

**Since Camel 4.9**

The Smooks Data Format uses [Smooks](https://www.smooks.org/) to transform from one data format to another and back again. A configuration for a Smooks Data Format should not allocate system resources because the data format does not close those resources. Use this data format when you are primarily interested in transformation and binding; not other Smooks features like routing. The latter should be done with the [Smooks component](../../4.18.x/smooks-component.md).

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

The Smooks dataformat supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **smooksConfig** (common) |  | `String` | **Required** Path to the Smooks configuration file. |
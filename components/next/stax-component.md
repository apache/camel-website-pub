# StAX

**Since Camel 2.9**

**Only producer is supported**

The StAX component allows messages to be processed through a SAX [ContentHandler](http://download.oracle.com/javase/6/docs/api/org/xml/sax/ContentHandler.md).  
Another feature of this component is to allow iterating over JAXB records using StAX, for example, using the [Split EIP](eips/split-eip.md).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-stax</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

stax:content-handler-class

example:

stax:org.superbiz.FooContentHandler

You can look up a `org.xml.sax.ContentHandler` bean from the Registry using the # syntax as shown:

stax:#myHandler

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The StAX component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The StAX endpoint is configured using URI syntax:

stax:contentHandlerClass

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **contentHandlerClass** (producer) | **Required** The FQN class name for the ContentHandler implementation to use. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Usage

### Usage of a content handler as StAX parser

The message body after the handling is the handler itself.

Here is an example:

_Java-only: inline Processor class_

```java
from("file:target/in")
  .to("stax:org.superbiz.handler.CountingHandler")
  // CountingHandler implements org.xml.sax.ContentHandler or extends org.xml.sax.helpers.DefaultHandler
  .process(exchange -> {
      CountingHandler handler = exchange.getIn().getBody(CountingHandler.class);
      // do some great work with the handler
  });
```

### Iterate over a collection using JAXB and StAX

First, we suppose you have JAXB objects.

For instance, a list of records in a wrapper object:

_Java-only: Java JAXB annotated class_

```java
import java.util.ArrayList;
import java.util.List;
import javax.xml.bind.annotation.XmlAccessType;
import javax.xml.bind.annotation.XmlAccessorType;
import javax.xml.bind.annotation.XmlElement;
import javax.xml.bind.annotation.XmlRootElement;

@XmlAccessorType(XmlAccessType.FIELD)
@XmlRootElement(name = "records")
public class Records {
    @XmlElement(required = true)
    protected List<Record> record;

    public List<Record> getRecord() {
        if (record == null) {
            record = new ArrayList<Record>();
        }
        return record;
    }
}
```

and

_Java-only: Java JAXB annotated class_

```java
import javax.xml.bind.annotation.XmlAccessType;
import javax.xml.bind.annotation.XmlAccessorType;
import javax.xml.bind.annotation.XmlAttribute;
import javax.xml.bind.annotation.XmlType;

@XmlAccessorType(XmlAccessType.FIELD)
@XmlType(name = "record", propOrder = { "key", "value" })
public class Record {
    @XmlAttribute(required = true)
    protected String key;

    @XmlAttribute(required = true)
    protected String value;

    public String getKey() {
        return key;
    }

    public void setKey(String key) {
        this.key = key;
    }

    public String getValue() {
        return value;
    }

    public void setValue(String value) {
        this.value = value;
    }
}
```

Then you get an XML file to process:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<records>
  <record value="v0" key="0"/>
  <record value="v1" key="1"/>
  <record value="v2" key="2"/>
  <record value="v3" key="3"/>
  <record value="v4" key="4"/>
  <record value="v5" key="5"/>
</record>
```

The StAX component provides an `StAXBuilder` which can be used when iterating XML elements with the Camel Splitter

_Java-only: Java static method with class literal_

```java
from("file:target/in")
    .split(stax(Record.class)).streaming()
        .to("mock:records");
```

Where `stax` is a static method on `org.apache.camel.component.stax.StAXBuilder` which you can have static import in the Java code. The stax builder is by default namespace aware on the XMLReader it uses. You can turn this off by setting the boolean parameter to false, as shown below:

_Java-only: Java static method with class literal_

```java
from("file:target/in")
    .split(stax(Record.class, false)).streaming()
        .to("mock:records");
```

Alternatively, the example above could be implemented as follows in Spring XML

_XML-only: Spring bean configuration with StAXBuilder factory method_

```xml
  <!-- use STaXBuilder to create the expression we want to use in the route below for splitting the XML file -->
  <!-- notice we use the factory-method to define the stax method, and to pass in the parameter as a constructor-arg -->
  <bean id="staxRecord" class="org.apache.camel.component.stax.StAXBuilder" factory-method="stax">
    <!-- FQN class name of the POJO with the JAXB annotations -->
    <constructor-arg index="0" value="org.apache.camel.component.stax.model.Record"/>
  </bean>

  <camelContext xmlns="http://camel.apache.org/schema/spring">
    <route>
      <!-- pickup XML files -->
      <from uri="file:target/in"/>
      <split streaming="true">
        <!-- split the file using StAX (ref to bean above) -->
        <!-- and use streaming mode in the splitter -->
        <ref>staxRecord</ref>
        <!-- and send each split to a mock endpoint, which will be a Record POJO instance -->
        <to uri="mock:records"/>
      </split>
    </route>
  </camelContext>
```
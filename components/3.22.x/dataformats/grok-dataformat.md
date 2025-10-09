# Grok

**Since Camel 3.0**

This component provides dataformat for processing inputs with grok patterns. Grok patterns are used to process unstructured data into structured objects - `List<Map<String, Object>>`.

This component is based on [Java Grok library](https://github.com/thekrakken/java-grok)

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-grok</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Basic usage

Extract all IP adresses from input

```java
from("direct:in")
    .unmarshal().grok("%{IP:ip}")
    .to("log:out");
```

Parse Apache logs and process only 4xx responses

```java
from("file://apacheLogs")
    .unmarshal().grok("%{COMBINEDAPACHELOG")
    .split(body()).filter(simple("${body[response]} starts with '4'"))
    .to("log:4xx")
```

## Preregistered patterns

This component comes with preregistered patterns, which are based on Logstash patterns. All [Java Grok Default Patterns](https://github.com/thekrakken/java-grok/tree/master/src/main/resources/patterns/patterns) are preregistered and as such could be used without manual registration.

## Custom patterns

Camel Grok DataFormat supports plugable patterns, which are auto loaded from Camel Registry. You can register patterns with Java DSL and Spring DSL

Spring DSL:

```xml
<beans>
    <bean id="myCustomPatternBean" class="org.apache.camel.component.grok.GrokPattern">
        <constructor-arg value="FOOBAR"/>
        <constructor-arg value="foo|bar"/>
    </bean>
<beans>
<camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
    <route>
        <from uri="direct:in"/>
        <unmarshal>
            <grok pattern="%{FOOBAR:fooBar}"/>
        </unmarshal>
        <to uri="log:out"/>
    </route>
</camelContext>
```

Java DSL:

```java
public class MyRouteBuilder extends RouteBuilder {

    @Override
    public void configure() throws Exception {
        bindToRegistry("myCustomPatternBean", new GrokPattern("FOOBAR", "foo|bar"));

        from("direct:in")
            .unmarshal().grok("%{FOOBAR:fooBar}")
            .to("log:out");
    }
}
```

## Grok Dataformat Options

The Grok dataformat supports 4 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **pattern** |  | `String` | The grok pattern to match lines of input. |
| **flattened** | `false` | `Boolean` | Turns on flattened mode. In flattened mode the exception is thrown when there are multiple pattern matches with same key. |
| **allowMultipleMatchesPerLine** | `true` | `Boolean` | If false, every line of input is matched for pattern only once. Otherwise the line can be scanned multiple times when non-terminal pattern is used. |
| **namedOnly** | `false` | `Boolean` | Whether to capture named expressions only or not (i.e. %\\{IP:ip} but not ${IP}). |

## Spring Boot Auto-Configuration

When using grok with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-grok-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.grok.allow-multiple-matches-per-line** | If false, every line of input is matched for pattern only once. Otherwise the line can be scanned multiple times when non-terminal pattern is used. | true | Boolean |
| **camel.dataformat.grok.enabled** | Whether to enable auto configuration of the grok data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.grok.flattened** | Turns on flattened mode. In flattened mode the exception is thrown when there are multiple pattern matches with same key. | false | Boolean |
| **camel.dataformat.grok.named-only** | Whether to capture named expressions only or not (i.e. %\\{IP:ip} but not ${IP}). | false | Boolean |
| **camel.dataformat.grok.pattern** | The grok pattern to match lines of input. |  | String |
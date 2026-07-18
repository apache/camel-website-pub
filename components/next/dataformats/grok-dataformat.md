# Grok

**Since Camel 3.0**

This component provides dataformat for processing inputs with grok patterns. Grok patterns are used to process unstructured data into structured objects - `List<Map<String, Object>>`.

This component is based on the [Java Grok library](https://github.com/thekrakken/java-grok)

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-grok</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Usage

Extract all IP addresses from input

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .unmarshal().grok("%{IP:ip}")
    .to("log:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <unmarshal><grok pattern="%{IP:ip}"/></unmarshal>
  <to uri="log:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - unmarshal:
            grok:
              pattern: "%{IP:ip}"
        - to:
            uri: log:out
```

Parse Apache logs and process only 4xx responses

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://apacheLogs")
    .unmarshal().grok("%{COMBINEDAPACHELOG")
    .split(body()).filter(simple("${body[response]} starts with '4'"))
    .to("log:4xx");
```

```xml
<route>
  <from uri="file://apacheLogs"/>
  <unmarshal><grok pattern="%{COMBINEDAPACHELOG"/></unmarshal>
  <split>
    <simple>${body}</simple>
    <filter>
      <simple>${body[response]} starts with '4'</simple>
      <to uri="log:4xx"/>
    </filter>
  </split>
</route>
```

```yaml
- route:
    from:
      uri: file://apacheLogs
      steps:
        - unmarshal:
            grok:
              pattern: "%{COMBINEDAPACHELOG"
        - split:
            simple: "${body}"
            steps:
              - filter:
                  simple: "${body[response]} starts with '4'"
                  steps:
                    - to:
                        uri: log:4xx
```

### Preregistered patterns

This component comes with preregistered patterns, which are based on Logstash patterns. All [Java Grok Default Patterns](https://github.com/thekrakken/java-grok/tree/master/src/main/resources/patterns/patterns) are preregistered and as such could be used without manual registration.

### Custom patterns

Camel Grok DataFormat supports plugable patterns, which are auto loaded from Camel Registry. You can register patterns with Java DSL and Spring DSL:

_Java-only: registering a custom Grok pattern_

```java
bindToRegistry("myCustomPatternBean", new GrokPattern("FOOBAR", "foo|bar"));

from("direct:in")
    .unmarshal().grok("%{FOOBAR:fooBar}")
    .to("log:out");
```

In Spring XML, you register the custom pattern as a bean:

_XML-only: Spring XML bean registration_

```xml
<beans>
    <bean id="myCustomPatternBean" class="org.apache.camel.component.grok.GrokPattern">
        <constructor-arg value="FOOBAR"/>
        <constructor-arg value="foo|bar"/>
    </bean>
</beans>
```

## Grok Data format Options

The Grok dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **pattern** (common) |  | `String` | The grok pattern to match lines of input. |
| **flattened** (common) | `false` | `Boolean` | Whether to use flattened mode. In flattened mode an exception is thrown when there are multiple pattern matches with the same key. |
| **allowMultipleMatchesPerLine** (common) | `true` | `Boolean` | Whether to allow multiple matches per line. If false, every line of input is matched for the pattern only once. Otherwise the line can be scanned multiple times when a non-terminal pattern is used. |
| **namedOnly** (common) | `false` | `Boolean` | Whether to capture named expressions only or not (i.e. %\\{IP:ip} but not ${IP}). |
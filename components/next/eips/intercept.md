# Intercept

The intercept feature in Camel supports intercepting [Exchange](../../../manual/exchange.md)'s' while they are being routed.

## Kinds of interceptors

Camel supports three kinds of interceptors:

-   [`intercept`](#Intercept-Intercept) that intercepts every processing step as they happen during routing
    
-   [`interceptFrom`](#Intercept-InterceptFrom) that intercepts only the incoming step (i.e., [from](from-eip.md))
    
-   [`interceptSendToEndpoint`](#Intercept-InterceptSendToEndpoint) that intercepts only when an [Exchange](../../../manual/exchange.md) is about to be sent to the given [endpoint](message-endpoint.md).
    

The `interceptSendToEndpoint` is dynamic hence it will also trigger if a dynamic URI is constructed that Camel was not aware of at startup time.

The `interceptFrom` is not dynamic, and will only intercept all the known routes when Camel is starting. So if you construct a `Consumer` using the Camel Java API and consumes messages from this endpoint, then the `interceptFrom` is not triggered.

### Interceptor scopes

All the interceptors can be configured on global, or with [Route Configuration](../../../manual/route-configuration.md).

### Common features of the interceptors

All these interceptors support the following features:

-   [Predicate](../../../manual/predicate.md) using `onWhen` to only trigger the interceptor in certain conditions
    
-   `stop` forces stopping continue routing the Exchange and mark it as completed successful (it’s actually the [Stop](stop-eip.md) EIP).
    
-   `skip` when used with `interceptSendToEndpoint` will **skip** sending the message to the original intended endpoint.
    
-   `afterUri` when used with `interceptSendToEndpoint` allows to send the message to an [endpoint](message-endpoint.md) afterward.
    
-   `interceptFrom` and `interceptSendToEndpoint` support endpoint URI pattern matching by exact uri, wildcard and regular expression. See further below for more details.
    
-   The intercepted endpoint uri is stored as exchange property with the key `Exchange.INTERCEPTED_ENDPOINT`.
    

### Interceptors metadata

When using Apache Camel interceptors, the framework automatically populates exchange properties with contextual information about where the interception occurred:

-   `Exchange.INTERCEPTED_ROUTE_ENDPOINT`: The route’s endpoint URI that was intercepted.
    
-   `Exchange.INTERCEPTED_ROUTE_ID`: The intercepted route’s ID.
    
-   `Exchange.INTERCEPTED_NODE_ID`: The intercepted route’s node ID.
    

## Using `intercept`

The `Intercept` is intercepting the [Exchange](../../../manual/exchange.md) on every processing step during routing.

Given the following example:

-   Java
    
-   XML
    
-   YAML
    

```java
// global interceptor for all routes
intercept().to("log:hello");

from("jms:queue:order")
  .to("bean:validateOrder")
  .to("bean:processOrder");
```

```xml
  <!-- global interceptor for all routes -->
  <intercept>
    <to uri="log:hello"/>
  </intercept>

  <route>
    <from uri="jms:queue:order"/>
    <to uri="bean:validateOrder"/>
    <to uri="bean:processOrder"/>
  </route>
```

```yaml
- intercept:
    steps:
      - to: "log:hello"
- route:
    from:
      uri: jms:queue:order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: bean:processOrder
```

What happens is that the `Exchange` is intercepted before each processing step, that means that it will be intercepted before

-   `.to("bean:validateOrder")`
    
-   `.to("bean:processOrder")`
    

So in this example we intercept the `Exchange` twice.

### Controlling when to intercept using a predicate

If you only want to intercept "sometimes", then you can use a [predicate](../../../manual/predicate.md).

For instance, in the sample below, we only intercept if the message body contains the string word Hello:

-   Java
    
-   XML
    
-   YAML
    

```java
intercept().onWhen(body().contains("Hello")).to("mock:intercepted");

from("jms:queue:order")
  .to("bean:validateOrder")
  .to("bean:processOrder");
```

```xml
<intercept>
  <onWhen>
      <simple>${body} contains 'Hello'</simple>
  </onWhen>
  <to uri="mock:intercepted"/>
</intercept>

<route>
  <from uri="jms:queue:order"/>
  <to uri="bean:validateOrder"/>
  <to uri="bean:processOrder"/>
</route>
```

```yaml
- intercept:
    onWhen:
      simple: "${body} contains 'Hello'"
    steps:
      - to: "log:hello"
- route:
    from:
      uri: jms:queue:order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: bean:processOrder
```

### Controlling when to intercept using contextual information

-   Java
    
-   XML
    
-   YAML
    

```java
intercept().choice()
    .when(header(Exchange.INTERCEPTED_ROUTE_ID).isEqualTo("criticalRoute"))
        .to("direct:specialHandling")
    .otherwise()
        .to("direct:standardHandling");
```

```xml
<intercept>
    <choice>
      <when>
        <simple>${header.CamelInterceptedRouteId} == 'criticalRoute'</simple>
        <to uri="direct:specialHandling"/>
      </when>
      <otherwise>
        <to uri="direct:standardHandling"/>
      </otherwise>
    </choice>
</intercept>
```

```yaml
- intercept:
    steps:
      - choice:
          when:
            - expression:
                simple:
                  expression: "${header.CamelInterceptedRouteId} == 'criticalRoute'"
              steps:
                - to:
                    uri: direct:specialHandling
          otherwise:
            steps:
              - to:
                  uri: direct:standardHandling
```

### Stop routing after being intercepted

It is also possible to stop routing after being intercepted. Now suppose that if the message body contains the word Hello we want to log and stop, then we can do:

-   Java
    
-   XML
    
-   YAML
    

```java
intercept().onWhen(body().contains("Hello"))
  .to("log:test")
  .stop(); // stop continue routing

from("jms:queue:order")
  .to("bean:validateOrder")
  .to("bean:processOrder");
```

```xml
  <intercept>
      <onWhen>
        <simple>${body} contains 'Hello'</simple>
        <to uri="log:test"/>
        <stop/> <!-- stop continue routing -->
      </onWhen>
  </intercept>

  <route>
    <from uri="jms:queue:order"/>
    <to uri="bean:validateOrder"/>
    <to uri="bean:processOrder"/>
  </route>
```

```yaml
- intercept:
    onWhen:
      simple: "${body} contains 'Hello'"
    steps:
      - to: "log:test"
      - stop: {}
- route:
    from:
      uri: jms:queue:order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: bean:processOrder
```

## Using `interceptFrom`

The `interceptFrom` is for intercepting any incoming Exchange, in any route (it intercepts all the [`from`](from-eip.md) EIPs)

This allows you to do some custom behavior for received Exchanges. You can provide a specific uri for a given Endpoint then it only applies for that particular route.

So let’s start with the logging example. We want to log all the incoming messages, so we use `interceptFrom` to route to the [Log](../log-component.md) component.

-   Java
    
-   XML
    
-   YAML
    

```java
interceptFrom()
  .to("log:incoming");

from("jms:queue:order")
  .to("bean:validateOrder")
  .to("bean:processOrder");
```

```xml
  <interceptFrom>
    <to uri="log:incoming"/>
  </interceptFrom>

  <route>
    <from uri="jms:queue:order"/>
    <to uri="bean:validateOrder"/>
    <to uri="bean:processOrder"/>
  </route>
```

```yaml
- interceptFrom:
    steps:
      - to: "log:incoming"
- route:
    from:
      uri: jms:queue:order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: bean:processOrder
```

If you want to only apply a specific endpoint, such as all jms endpoints, you can do:

-   Java
    
-   XML
    
-   YAML
    

```java
interceptFrom("jms*")
  .to("log:incoming");

from("jms:queue:order")
  .to("bean:validateOrder")
  .to("bean:processOrder");

from("file:inbox")
  .to("ftp:someserver/backup")
```

```xml
  <interceptFrom uri="jms*">
    <to uri="log:incoming"/>
  </intercept>

  <route>
    <from uri="jms:queue:order"/>
    <to uri="bean:validateOrder"/>
    <to uri="bean:processOrder"/>
  </route>
  <route>
    <from uri="file:inbox"/>
    <to uri="ftp:someserver/backup"/>
  </route>
```

```yaml
- interceptFrom:
    uri: "jms*"
    steps:
      - to: "log:incoming"
- route:
    from:
      uri: jms:queue:order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: bean:processOrder
- route:
    from:
      uri: file:inbox
      steps:
        - to:
            uri: ftp:someserver/backup
```

In this example then only messages from the JMS route are intercepted, because we specified a pattern in the `interceptFrom` as `jms*` (uses a wildcard).

The pattern syntax is documented in more details later.

## Using `interceptSendToEndpoint`

You can also intercept when Apache Camel is sending a message to an [endpoint](message-endpoint.md).

This can be used to do some custom processing before the message is sent to the intended destination.

The interceptor can also be configured to not send to the destination (`skip`) which means the message is detoured instead.

A [Predicate](../../../manual/predicate.md) can also be used to control when to intercept, which has been previously covered.

The `afterUri` option, is used when you need to process the response message from the intended destination. This functionality was added later to the interceptor, in a way of sending to yet another [endpoint](message-endpoint.md).

Let’s start with a basic example, where we want to intercept when a message is being sent to [kafka](../kafka-component.md):

-   Java
    
-   XML
    
-   YAML
    

```java
interceptSendToEndpoint("kafka*")
  .to("bean:beforeKafka");

from("jms:queue:order")
  .to("bean:validateOrder")
  .to("bean:processOrder")
  .to("kafka:order");
```

```xml
  <interceptSendToEndpoint uri="kafka*">
    <to uri="bean:beforeKafka"/>
  </interceptSendToEndpoint>

  <route>
    <from uri="jms:queue:order"/>
    <to uri="bean:validateOrder"/>
    <to uri="bean:processOrder"/>
    <to uri="kafka:order"/>
  </route>
```

```yaml
- interceptSendToEndpoint:
    uri: "kafka*"
    steps:
      - to: "bean:beforeKafka"
- route:
    from:
      uri: jms:queue:order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: bean:processOrder
        - to:
            uri: kafka:order
```

When you also want to process the message after it has been sent to the intended destination, then the example is slightly _odd_ because you have to use the `afterUri` as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
interceptSendToEndpoint("kafka*")
  .to("bean:beforeKafka")
  .afterUri("bean:afterKafka");

from("jms:queue:order")
  .to("bean:validateOrder")
  .to("bean:processOrder")
  .to("kafka:order");
```

```xml
  <interceptSendToEndpoint uri="kafka*" afterUri="bean:afterKafka">
    <to uri="bean:beforeKafka"/>
  </interceptSendToEndpoint>

  <route>
    <from uri="jms:queue:order"/>
    <to uri="bean:validateOrder"/>
    <to uri="bean:processOrder"/>
    <to uri="kafka:order"/>
  </route>
```

```yaml
- interceptSendToEndpoint:
    uri: "kafka*"
    afterUri: "bean:afterKafka"
    steps:
      - to: "bean:beforeKafka"
- route:
    from:
      uri: jms:queue:order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: bean:processOrder
        - to:
            uri: kafka:order
```

### Skip sending to original endpoint

Sometimes you want to **intercept and skip** sending messages to a specific endpoint.

For example, to avoid sending any message to kafka, but detour them to a [mock](../mock-component.md) endpoint, it can be done as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
interceptSendToEndpoint("kafka*").skipSendToOriginalEndpoint()
  .to("mock:kafka");

from("jms:queue:order")
  .to("bean:validateOrder")
  .to("bean:processOrder")
  .to("kafka:order");
```

```xml
  <interceptSendToEndpoint uri="kafka*" skipSendToOriginalEndpoint="true">
    <to uri="mock:kafka"/>
  </interceptSendToEndpoint>

  <route>
    <from uri="jms:queue:order"/>
    <to uri="bean:validateOrder"/>
    <to uri="bean:processOrder"/>
    <to uri="kafka:order"/>
  </route>
```

```yaml
- interceptSendToEndpoint:
    uri: "kafka*"
    skipSendToOriginalEndpoint: true
    steps:
      - to: "mock:kafka"
- route:
    from:
      uri: jms:queue:order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: bean:processOrder
        - to:
            uri: kafka:order
```

### Conditional skipping sending to endpoint

You can combine both a [predicate](../../../manual/predicate.md) and skip sending to the original endpoint. For example, suppose you have some "test" messages that sometimes occur, and that you want to avoid sending these messages to a downstream kafka system, then this can be done as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
interceptSendToEndpoint("kafka*").skipSendToOriginalEndpoint()
  .onWhen(simple("${header.biztype} == 'TEST'")
  .log("TEST message detected - is NOT send to kafka");

from("jms:queue:order")
  .to("bean:validateOrder")
  .to("bean:processOrder")
  .to("kafka:order");
```

```xml
  <interceptSendToEndpoint uri="kafka*" skipSendToOriginalEndpoint="true">
    <onWhen><simple>${header.biztype} == 'TEST'</simple></onWhen>
    <log message="TEST message detected - is NOT send to kafka"/>
  </interceptSendToEndpoint>

  <route>
    <from uri="jms:queue:order"/>
    <to uri="bean:validateOrder"/>
    <to uri="bean:processOrder"/>
    <to uri="kafka:order"/>
  </route>
```

```yaml
- interceptSendToEndpoint:
    uri: "kafka*"
    skipSendToOriginalEndpoint: true
    onWhen:
      simple: "${header.biztype} == 'TEST'"
    steps:
      - log:
          message: "TEST message detected - is NOT send to kafka"
- route:
    from:
      uri: jms:queue:order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: bean:processOrder
        - to:
            uri: kafka:order
```

## Intercepting endpoints using pattern matching

The `interceptFrom` and `interceptSendToEndpoint` support endpoint pattern matching by the following rules in the given order:

-   match by exact URI name
    
-   match by wildcard
    
-   match by regular expression
    

### Intercepting when matching by exact URI

This matches only a specific endpoint with exactly the same URI.

For example, to intercept messages being sent to a specific JMS queue, you can do:

-   Java
    
-   XML
    
-   YAML
    

```java
interceptSendToEndpoint("jms:queue:cheese")
  .to("log:smelly");
```

```xml
  <interceptSendToEndpoint uri="jms:queue:cheese">
    <to uri="log:smelly"/>
  </interceptSendToEndpoint>
```

```yaml
- interceptSendToEndpoint:
    uri: "jms:queue:cheese"
    steps:
      - to: "log:smelly"
```

### Intercepting when matching endpoints by wildcard

Match by wildcard allows you to match a range of endpoints or all of a given type. For instance use `file:*` will match all [file-based](../file-component.md) endpoints.

-   Java
    
-   XML
    
-   YAML
    

```java
interceptFrom("file:*")
  .to("log:from-file");
```

```xml
  <interceptFrom uri="file:*">
    <to uri="log:from-file"/>
  </interceptFrom>
```

```yaml
- interceptFrom:
    uri: "file:*"
    steps:
      - to: "log:from-file"
```

Match by wildcard works so that the pattern ends with a `\*` and that the uri matches if it starts with the same pattern.

For example, you can be more specific, to only match for files from specific folders like:

-   Java
    
-   XML
    
-   YAML
    

```java
interceptFrom("file:order/inbox/*")
  .to("log:new-file-orders");
```

```xml
  <interceptFrom uri="file:order/inbox/*">
    <to uri="log:new-file-orders"/>
  </interceptFrom>
```

```yaml
- interceptFrom:
    uri: "file:order/inbox/*"
    steps:
      - to: "log:new-file-orders"
```

### Intercepting when matching endpoints by regular expression

Match by regular expression is just like match by wildcard but using regex instead. So if we want to intercept incoming messages from gold and silver JMS queues, we can do:

-   Java
    
-   XML
    
-   YAML
    

```java
interceptFrom("jms:queue:(gold|silver)")
  .to("seda:handleFast");
```

```xml
  <interceptFrom uri="jms:queue:(gold|silver)">
    <to uri="seda:handleFast"/>
  </interceptFrom>
```

```yaml
- interceptFrom:
    uri: "jms:queue:(gold|silver)"
    steps:
      - to: "seda:handleFast"
```
# Mock

**Since Camel 1.0**

**Only producer is supported**

Testing of distributed and asynchronous processing is notoriously difficult. The [Mock](#), and [DataSet](dataset-component.md) endpoints work great with the Camel Testing Framework to simplify your unit and integration testing using [Enterprise Integration Patterns](eips/enterprise-integration-patterns.md) and Camel’s large range of Components together with the powerful Bean Integration.

The Mock component provides a powerful declarative testing mechanism, which is similar to [jMock](http://www.jmock.org) in that it allows declarative expectations to be created on any Mock endpoint before a test begins. Then the test is run, which typically fires messages to one or more endpoints, and finally the expectations can be asserted in a test case to ensure the system worked as expected.

This allows you to test various things like:

-   The correct number of messages are received on each endpoint,
    
-   The correct payloads are received, in the right order,
    
-   Messages arrive on an endpoint in order, using some Expression to create an order testing function,
    
-   Messages arrive match some kind of Predicate such as that specific headers have certain values, or that parts of the messages match some predicate, such as by evaluating an [XPath](languages/xpath-language.md) or [XQuery](languages/xquery-language.md) Expression.
    

> **Note**
> There is also the [Test endpoint](others/test.md) which is a Mock endpoint, but which uses a second endpoint to provide the list of expected message bodies and automatically sets up the Mock endpoint assertions. In other words, it’s a Mock endpoint that automatically sets up its assertions from some sample messages in a File or [database](jpa-component.md), for example.

> **Caution**
> **Mock endpoints keep received Exchanges in memory indefinitely.**
>
> Remember that Mock is designed for testing. When you add Mock endpoints to a route, each Exchange sent to the endpoint will be stored (to allow for later validation) in memory until explicitly reset or the JVM is restarted. If you are sending high volume and/or large messages, this may cause excessive memory use. If your goal is to test deployable routes inline, consider using NotifyBuilder or AdviceWith in your tests instead of adding Mock endpoints to routes directly. There are two new options `retainFirst`, and `retainLast` that can be used to limit the number of messages the Mock endpoints keep in memory.

## URI format

mock:someName\[?options\]

Where `someName` can be any string that uniquely identifies the endpoint.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Mock component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **log** (producer) | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **exchangeFormatter** (advanced) | **Autowired** Sets a custom ExchangeFormatter to convert the Exchange to a String suitable for logging. If not specified, we default to DefaultExchangeFormatter. |  | ExchangeFormatter |

## Endpoint Options

The Mock endpoint is configured using URI syntax:

mock:name

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (producer) | **Required** Name of mock endpoint. |  | String |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **assertPeriod** (producer) | Sets a grace period after which the mock endpoint will re-assert to ensure the preliminary assertion is still valid. This is used for example to assert that exactly a number of messages arrives. For example if expected count was set to 5, then the assertion is satisfied when 5 or more message arrives. To ensure that exactly 5 messages arrives, then you would need to wait a little period to ensure no further message arrives. This is what you can use this method for. By default this period is disabled. |  | long |
| **expectedCount** (producer) | Specifies the expected number of message exchanges that should be received by this endpoint. Beware: If you want to expect that 0 messages, then take extra care, as 0 matches when the tests starts, so you need to set a assert period time to let the test run for a while to make sure there are still no messages arrived; for that use setAssertPeriod(long). An alternative is to use NotifyBuilder, and use the notifier to know when Camel is done routing some messages, before you call the assertIsSatisfied() method on the mocks. This allows you to not use a fixed assert period, to speedup testing times. If you want to assert that exactly n’th message arrives to this mock endpoint, then see also the setAssertPeriod(long) method for further details. | \-1 | int |
| **failFast** (producer) | Sets whether assertIsSatisfied() should fail fast at the first detected failed expectation while it may otherwise wait for all expected messages to arrive before performing expectations verifications. Is by default true. Set to false to use behavior as in Camel 2.x. | false | boolean |
| **log** (producer) | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | boolean |
| **reportGroup** (producer) | A number that is used to turn on throughput logging based on groups of the size. |  | int |
| **resultMinimumWaitTime** (producer) | Sets the minimum expected amount of time (in millis) the assertIsSatisfied() will wait on a latch until it is satisfied. |  | long |
| **resultWaitTime** (producer) | Sets the maximum amount of time (in millis) the assertIsSatisfied() will wait on a latch until it is satisfied. |  | long |
| **retainFirst** (producer) | Specifies to only retain the first n’th number of received Exchanges. This is used when testing with big data, to reduce memory consumption by not storing copies of every Exchange this mock endpoint receives. Important: When using this limitation, then the getReceivedCounter() will still return the actual number of received Exchanges. For example if we have received 5000 Exchanges, and have configured to only retain the first 10 Exchanges, then the getReceivedCounter() will still return 5000 but there is only the first 10 Exchanges in the getExchanges() and getReceivedExchanges() methods. When using this method, then some of the other expectation methods is not supported, for example the expectedBodiesReceived(Object…​) sets a expectation on the first number of bodies received. You can configure both setRetainFirst(int) and setRetainLast(int) methods, to limit both the first and last received. | \-1 | int |
| **retainLast** (producer) | Specifies to only retain the last n’th number of received Exchanges. This is used when testing with big data, to reduce memory consumption by not storing copies of every Exchange this mock endpoint receives. Important: When using this limitation, then the getReceivedCounter() will still return the actual number of received Exchanges. For example if we have received 5000 Exchanges, and have configured to only retain the last 20 Exchanges, then the getReceivedCounter() will still return 5000 but there is only the last 20 Exchanges in the getExchanges() and getReceivedExchanges() methods. When using this method, then some of the other expectation methods is not supported, for example the expectedBodiesReceived(Object…​) sets a expectation on the first number of bodies received. You can configure both setRetainFirst(int) and setRetainLast(int) methods, to limit both the first and last received. | \-1 | int |
| **sleepForEmptyTest** (producer) | Allows a sleep to be specified to wait to check that this endpoint really is empty when expectedMessageCount(int) is called with zero. |  | long |
| **copyOnExchange** (producer (advanced)) | Sets whether to make a deep copy of the incoming Exchange when received at this mock endpoint. Is by default true. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Simple Example

Here’s a simple example of Mock endpoint in use. First, the endpoint is resolved on the context. Then we set an expectation, and then, after the test has run, we assert that our expectations have been met:

```java
MockEndpoint resultEndpoint = context.getEndpoint("mock:foo", MockEndpoint.class);

// set expectations
resultEndpoint.expectedMessageCount(2);

// send some messages

// now lets assert that the mock:foo endpoint received 2 messages
resultEndpoint.assertIsSatisfied();
```

You typically always call the [`assertIsSatisfied()`](https://www.javadoc.io/doc/org.apache.camel/camel-mock/latest/org/apache/camel/component/mock/MockEndpoint.html#assertIsSatisfied--) method to test that the expectations were met after running a test.

Camel will by default wait 10 seconds when the `assertIsSatisfied()` is invoked. This can be configured by setting the `setResultWaitTime(millis)` method.

## Using assertPeriod

When the assertion is satisfied then Camel will stop waiting and continue from the `assertIsSatisfied` method. That means if a new message arrives on the mock endpoint, just a bit later, that arrival will not affect the outcome of the assertion. Suppose you do want to test that no new messages arrives after a period thereafter, then you can do that by setting the `setAssertPeriod` method, for example:

```java
MockEndpoint resultEndpoint = context.getEndpoint("mock:foo", MockEndpoint.class);
resultEndpoint.setAssertPeriod(5000);
resultEndpoint.expectedMessageCount(2);

// send some messages

// now lets assert that the mock:foo endpoint received 2 messages
resultEndpoint.assertIsSatisfied();
```

## Setting expectations

You can see from the Javadoc of [MockEndpoint](https://www.javadoc.io/doc/org.apache.camel/camel-mock/current/org/apache/camel/component/mock/MockEndpoint.md) the various helper methods you can use to set expectations. The main methods are as follows:

 
| Method | Description |
| --- | --- |
| `[expectedMessageCount(int)](https://www.javadoc.io/doc/org.apache.camel/camel-mock/current/org/apache/camel/component/mock/MockEndpoint.html#expectedMessageCount\(int\))` | To define the expected message count on the endpoint. |
| `[expectedMinimumMessageCount(int)](https://www.javadoc.io/doc/org.apache.camel/camel-mock/current/org/apache/camel/component/mock/MockEndpoint.html#expectedMinimumMessageCount\(int\))` | To define the minimum number of expected messages on the endpoint. |
| `[expectedBodiesReceived(…​)](https://www.javadoc.io/doc/org.apache.camel/camel-mock/latest/org/apache/camel/component/mock/MockEndpoint.html#expectedBodiesReceived\(java.util.List\))` | To define the expected bodies that should be received (in order). |
| `[expectedHeaderReceived(…​)](https://www.javadoc.io/doc/org.apache.camel/camel-mock/latest/org/apache/camel/component/mock/MockEndpoint.html#expectedHeaderReceived\(java.lang.String,java.lang.Object\))` | To define the expected header that should be received |
| `[expectsAscending(Expression)](https://www.javadoc.io/doc/org.apache.camel/camel-mock/current/org/apache/camel/component/mock/MockEndpoint.html#expectsAscending\(org.apache.camel.Expression\))` | To add an expectation that messages are received in order, using the given Expression to compare messages. |
| `[expectsDescending(Expression)](https://www.javadoc.io/doc/org.apache.camel/camel-mock/current/org/apache/camel/component/mock/MockEndpoint.html#expectsDescending\(org.apache.camel.Expression\))` | To add an expectation that messages are received in order, using the given Expression to compare messages. |
| `[expectsNoDuplicates(Expression)](https://www.javadoc.io/doc/org.apache.camel/camel-mock/current/org/apache/camel/component/mock/MockEndpoint.html#expectsNoDuplicates\(org.apache.camel.Expression\))` | To add an expectation that no duplicate messages are received; using an Expression to calculate a unique identifier for each message. This could be something like the `JMSMessageID` if using JMS, or some unique reference number within the message. |

Here’s another example:

```java
resultEndpoint.expectedBodiesReceived("firstMessageBody", "secondMessageBody", "thirdMessageBody");
```

## Adding expectations to specific messages

In addition, you can use the [`message(int messageIndex)`](https://javadoc.io/doc/org.apache.camel/camel-mock/latest/org/apache/camel/component/mock/MockEndpoint.md) method to add assertions about a specific message that is received.

For example, to add expectations of the headers or body of the first message (using zero-based indexing like `java.util.List`), you can use the following code:

```java
resultEndpoint.message(0).header("foo").isEqualTo("bar");
```

There are some examples of the Mock endpoint in use in the [`camel-core` processor tests](https://github.com/apache/camel/tree/main/core/camel-core/src/test/java/org/apache/camel/processor).

## Mocking existing endpoints

Camel now allows you to automatically mock existing endpoints in your Camel routes.

> **Note**
> **How it works** The endpoints are still in action. What happens differently is that a [Mock](#) endpoint is injected and receives the message first and then delegates the message to the target endpoint. You can view this as a kind of intercept and delegate or endpoint listener.

Suppose you have the given route below:

**Route**

```java
    @Override
    protected RouteBuilder createRouteBuilder() throws Exception {
        return new RouteBuilder() {
            @Override
            public void configure() throws Exception {
                from("direct:start").routeId("start")
                        .to("direct:foo").to("log:foo").to("mock:result");

                from("direct:foo").routeId("foo")
                        .transform(constant("Bye World"));
            }
        };
    }
```

You can then use the `adviceWith` feature in Camel to mock all the endpoints in a given route from your unit test, as shown below:

**`adviceWith` mocking all endpoints**

```java
    @Test
    public void testAdvisedMockEndpoints() throws Exception {
        // advice the start route using the inlined AdviceWith lambda style route builder
        // which has extended capabilities than the regular route builder
        AdviceWith.adviceWith(context, "start", a ->
        // mock all endpoints
        a.mockEndpoints());

        getMockEndpoint("mock:direct:start").expectedBodiesReceived("Hello World");
        getMockEndpoint("mock:direct:foo").expectedBodiesReceived("Hello World");
        getMockEndpoint("mock:log:foo").expectedBodiesReceived("Bye World");
        getMockEndpoint("mock:result").expectedBodiesReceived("Bye World");

        template.sendBody("direct:start", "Hello World");

        assertMockEndpointsSatisfied();

        // additional test to ensure correct endpoints in registry
        assertNotNull(context.hasEndpoint("direct:start"));
        assertNotNull(context.hasEndpoint("direct:foo"));
        assertNotNull(context.hasEndpoint("log:foo"));
        assertNotNull(context.hasEndpoint("mock:result"));
        // all the endpoints was mocked
        assertNotNull(context.hasEndpoint("mock:direct:start"));
        assertNotNull(context.hasEndpoint("mock:direct:foo"));
        assertNotNull(context.hasEndpoint("mock:log:foo"));
    }
```

Notice that the mock endpoints is given the URI `mock:<endpoint>`, for example `mock:direct:foo`. Camel logs at `INFO` level the endpoints being mocked:

INFO  Adviced endpoint \[direct://foo\] with mock endpoint \[mock:direct:foo\]

> **Note**
> **Mocked endpoints are without parameters**  
> Endpoints which are mocked will have their parameters stripped off. For example the endpoint `log:foo?showAll=true` will be mocked to the following endpoint `mock:log:foo`. Notice the parameters have been removed.

Its also possible to only mock certain endpoints using a pattern. For example to mock all `log` endpoints you do as shown:

**`adviceWith` mocking only log endpoints using a pattern**

```java
    @Test
    public void testAdvisedMockEndpointsWithPattern() throws Exception {
        // advice the start route using the inlined AdviceWith lambda style route builder
        // which has extended capabilities than the regular route builder
        AdviceWith.adviceWith(context, "start", a ->
        // mock only log endpoints
        a.mockEndpoints("log*"));

        // now we can refer to log:foo as a mock and set our expectations
        getMockEndpoint("mock:log:foo").expectedBodiesReceived("Bye World");

        getMockEndpoint("mock:result").expectedBodiesReceived("Bye World");

        template.sendBody("direct:start", "Hello World");

        assertMockEndpointsSatisfied();

        // additional test to ensure correct endpoints in registry
        assertNotNull(context.hasEndpoint("direct:start"));
        assertNotNull(context.hasEndpoint("direct:foo"));
        assertNotNull(context.hasEndpoint("log:foo"));
        assertNotNull(context.hasEndpoint("mock:result"));
        // only the log:foo endpoint was mocked
        assertNotNull(context.hasEndpoint("mock:log:foo"));
        assertNull(context.hasEndpoint("mock:direct:start"));
        assertNull(context.hasEndpoint("mock:direct:foo"));
    }
```

The pattern supported can be a wildcard or a regular expression. See more details about this at Intercept as its the same matching function used by Camel.

> **Note**
> Mind that mocking endpoints causes the messages to be copied when they arrive on the mock.  
> That means Camel will use more memory. This may not be suitable when you send in a lot of messages.

## Mocking existing endpoints using the `camel-test` component

Instead of using the `adviceWith` to instruct Camel to mock endpoints, you can easily enable this behavior when using the `camel-test` Test Kit.

The same route can be tested as follows. Notice that we return `"*"` from the `isMockEndpoints` method, which tells Camel to mock all endpoints.

If you only want to mock all `log` endpoints you can return `"log*"` instead.

**`isMockEndpoints` using camel-test kit**

```java
public class IsMockEndpointsJUnit4Test extends CamelTestSupport {

    @Override
    public String isMockEndpoints() {
        // override this method and return the pattern for which endpoints to mock.
        // use * to indicate all
        return "*";
    }

    @Test
    public void testMockAllEndpoints() throws Exception {
        // notice we have automatic mocked all endpoints and the name of the endpoints is "mock:uri"
        getMockEndpoint("mock:direct:start").expectedBodiesReceived("Hello World");
        getMockEndpoint("mock:direct:foo").expectedBodiesReceived("Hello World");
        getMockEndpoint("mock:log:foo").expectedBodiesReceived("Bye World");
        getMockEndpoint("mock:result").expectedBodiesReceived("Bye World");

        template.sendBody("direct:start", "Hello World");

        assertMockEndpointsSatisfied();

        // additional test to ensure correct endpoints in registry
        assertNotNull(context.hasEndpoint("direct:start"));
        assertNotNull(context.hasEndpoint("direct:foo"));
        assertNotNull(context.hasEndpoint("log:foo"));
        assertNotNull(context.hasEndpoint("mock:result"));
        // all the endpoints was mocked
        assertNotNull(context.hasEndpoint("mock:direct:start"));
        assertNotNull(context.hasEndpoint("mock:direct:foo"));
        assertNotNull(context.hasEndpoint("mock:log:foo"));
    }

    @Override
    protected RouteBuilder createRouteBuilder() throws Exception {
        return new RouteBuilder() {
            @Override
            public void configure() throws Exception {
                from("direct:start").to("direct:foo").to("log:foo").to("mock:result");

                from("direct:foo").transform(constant("Bye World"));
            }
        };
    }
}
```

## Mocking existing endpoints with XML DSL

If you do not use the `camel-test` component for unit testing (as shown above) you can use a different approach when using XML files for routes.  
The solution is to create a new XML file used by the unit test and then include the intended XML file which has the route you want to test.

Suppose we have the route in the `camel-route.xml` file:

**camel-route.xml**

```xml
    <!-- this camel route is in the camel-route.xml file -->
    <camelContext xmlns="http://camel.apache.org/schema/spring">

        <route>
            <from uri="direct:start"/>
            <to uri="direct:foo"/>
            <to uri="log:foo"/>
            <to uri="mock:result"/>
        </route>

        <route>
            <from uri="direct:foo"/>
            <transform>
                <constant>Bye World</constant>
            </transform>
        </route>

    </camelContext>
```

Then we create a new XML file as follows, where we include the `camel-route.xml` file and define a spring bean with the class `org.apache.camel.impl.InterceptSendToMockEndpointStrategy` which tells Camel to mock all endpoints:

**test-camel-route.xml**

```xml
    <!-- the Camel route is defined in another XML file -->
    <import resource="camel-route.xml"/>

    <!-- bean which enables mocking all endpoints -->
    <bean id="mockAllEndpoints" class="org.apache.camel.component.mock.InterceptSendToMockEndpointStrategy"/>
```

Then in your unit test you load the new XML file (`test-camel-route.xml`) instead of `camel-route.xml`.

To only mock all [Log](log-component.md) endpoints you can define the pattern in the constructor for the bean:

```xml
<bean id="mockAllEndpoints" class="org.apache.camel.impl.InterceptSendToMockEndpointStrategy">
    <constructor-arg index="0" value="log*"/>
</bean>
```

## Mocking endpoints and skip sending to original endpoint

Sometimes you want to easily mock and skip sending to a certain endpoints. So the message is detoured and send to the mock endpoint only. You can now use the `mockEndpointsAndSkip` method using AdviceWith. The example below will skip sending to the two endpoints `"direct:foo"`, and `"direct:bar"`.

**adviceWith mock and skip sending to endpoints**

```java
    @Test
    public void testAdvisedMockEndpointsWithSkip() throws Exception {
        // advice the first route using the inlined AdviceWith route builder
        // which has extended capabilities than the regular route builder
        AdviceWith.adviceWith(context.getRouteDefinitions().get(0), context, new AdviceWithRouteBuilder() {
            @Override
            public void configure() throws Exception {
                // mock sending to direct:foo and direct:bar and skip send to it
                mockEndpointsAndSkip("direct:foo", "direct:bar");
            }
        });

        getMockEndpoint("mock:result").expectedBodiesReceived("Hello World");
        getMockEndpoint("mock:direct:foo").expectedMessageCount(1);
        getMockEndpoint("mock:direct:bar").expectedMessageCount(1);

        template.sendBody("direct:start", "Hello World");

        assertMockEndpointsSatisfied();

        // the message was not send to the direct:foo route and thus not sent to
        // the seda endpoint
        SedaEndpoint seda = context.getEndpoint("seda:foo", SedaEndpoint.class);
        assertEquals(0, seda.getCurrentQueueSize());
    }
```

The same example using the Test Kit

**isMockEndpointsAndSkip using camel-test kit**

```java
public class IsMockEndpointsAndSkipJUnit4Test extends CamelTestSupport {

    @Override
    public String isMockEndpointsAndSkip() {
        // override this method and return the pattern for which endpoints to mock,
        // and skip sending to the original endpoint.
        return "direct:foo";
    }

    @Test
    public void testMockEndpointAndSkip() throws Exception {
        // notice we have automatic mocked the direct:foo endpoints and the name of the endpoints is "mock:uri"
        getMockEndpoint("mock:result").expectedBodiesReceived("Hello World");
        getMockEndpoint("mock:direct:foo").expectedMessageCount(1);

        template.sendBody("direct:start", "Hello World");

        assertMockEndpointsSatisfied();

        // the message was not send to the direct:foo route and thus not sent to the seda endpoint
        SedaEndpoint seda = context.getEndpoint("seda:foo", SedaEndpoint.class);
        assertEquals(0, seda.getCurrentQueueSize());
    }

    @Override
    protected RouteBuilder createRouteBuilder() throws Exception {
        return new RouteBuilder() {
            @Override
            public void configure() throws Exception {
                from("direct:start").to("direct:foo").to("mock:result");

                from("direct:foo").transform(constant("Bye World")).to("seda:foo");
            }
        };
    }
}
```

## Limiting the number of messages to keep

The [Mock](#) endpoints will by default keep a copy of every Exchange that it received. So if you test with a lot of messages, then it will consume memory.  
We have introduced two options `retainFirst` and `retainLast` that can be used to specify to only keep N’th of the first and/or last Exchanges.

For example in the code below, we only want to retain a copy of the first 5 and last 5 Exchanges the mock receives.

```java
  MockEndpoint mock = getMockEndpoint("mock:data");
  mock.setRetainFirst(5);
  mock.setRetainLast(5);
  mock.expectedMessageCount(2000);

  mock.assertIsSatisfied();
```

Using this has some limitations. The `getExchanges()` and `getReceivedExchanges()` methods on the `MockEndpoint` will return only the retained copies of the Exchanges. So in the example above, the list will contain 10 Exchanges; the first five, and the last five.  
The `retainFirst` and `retainLast` options also have limitations on which expectation methods you can use. For example the `expectedXXX` methods that work on message bodies, headers, etc. will only operate on the retained messages. In the example above they can test only the expectations on the 10 retained messages.

## Testing with arrival times

The [Mock](#) endpoint stores the arrival time of the message as a property on the Exchange.

```java
Date time = exchange.getProperty(Exchange.RECEIVED_TIMESTAMP, Date.class);
```

You can use this information to know when the message arrived on the mock. But it also provides foundation to know the time interval between the previous and next message arrived on the mock. You can use this to set expectations using the `arrives` DSL on the [Mock](#) endpoint.

For example to say that the first message should arrive between 0-2 seconds before the next you can do:

```java
mock.message(0).arrives().noLaterThan(2).seconds().beforeNext();
```

You can also define this as that 2nd message (0 index based) should arrive no later than 0-2 seconds after the previous:

```java
mock.message(1).arrives().noLaterThan(2).seconds().afterPrevious();
```

You can also use between to set a lower bound. For example suppose that it should be between 1-4 seconds:

```java
mock.message(1).arrives().between(1, 4).seconds().afterPrevious();
```

You can also set the expectation on all messages, for example to say that the gap between them should be at most 1 second:

```java
mock.allMessages().arrives().noLaterThan(1).seconds().beforeNext();
```

> **Tip**
> **Time units**
>
> In the example above we use `seconds` as the time unit, but Camel offers `milliseconds`, and `minutes` as well.

## Spring Boot Auto-Configuration

When using mock with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-mock-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.mock.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.mock.enabled** | Whether to enable auto configuration of the mock component. This is enabled by default. |  | Boolean |
| **camel.component.mock.exchange-formatter** | Sets a custom ExchangeFormatter to convert the Exchange to a String suitable for logging. If not specified, we default to DefaultExchangeFormatter. The option is a org.apache.camel.spi.ExchangeFormatter type. |  | ExchangeFormatter |
| **camel.component.mock.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.mock.log** | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | Boolean |
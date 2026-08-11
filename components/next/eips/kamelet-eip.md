# Kamelet

Kamelets (Kamel route snippets) allow users to connect to external systems via a simplified interface, hiding all the low-level details about how those connections are implemented.

> **Important**
> By default, calling kamelets should be done as [endpoints](message-endpoint.md) with the [kamelet](../../4.22.x/kamelet-component.md) component, such as `to("kamelet:mykamelet")`.

The Kamelet EIP allows calling Kamelets (i.e., [Route Template](../../../manual/route-template.md)), **for special use-cases**.

When a Kamelet is designed for a special use-case such as aggregating messages, and returning a response message only when a group of aggregated messages is completed. In other words, kamelet does not return a response message for every incoming message.

In special situations like these, then you **must** use this Kamelet EIP instead of using the [kamelet](../../4.22.x/kamelet-component.md) component.

Given the following Kamelet (as a route template):

_Java-only: defining a route template (Kamelet) with an aggregation strategy_

```java
routeTemplate("my-aggregate")
        .templateParameter("count")
        .from("kamelet:source")
        .aggregate(constant(true))
            .completionSize("{{count}}")
            .aggregationStrategy(AggregationStrategies.string(","))
            .to("log:aggregate")
            .to("kamelet:sink")
        .end();
```

> **Note**
> Note how the route template above uses _kamelet:sink_ as a special endpoint to send out a result message. This is only done when the [Aggregate EIP](aggregate-eip.md) has completed a group of messages.

And the following route using the kamelet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    // this is not possible, you must use Kamelet EIP instead
    .to("kamelet:my-aggregate?count=5")
    .to("log:info")
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="kamelet:my-aggregate?count=5"/>
    <to uri="log:info"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: kamelet:my-aggregate
            parameters:
              count: 5
        - to:
            uri: log:info
        - to:
            uri: mock:result
```

Then this does not work, instead you **must** use Kamelet EIP instead:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .kamelet("my-aggregate?count=5")
    .to("log:info")
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:start"/>
    <kamelet name="my-aggregate?count=5">
        <to uri="log:info"/>
        <to uri="mock:result"/>
    </kamelet>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - kamelet:
            name: my-aggregate?count=5
            steps:
              - to:
                  uri: log:info
              - to:
                  uri: mock:result
```

When calling a Kamelet, you may refer to the name (template id) of the Kamelet in the EIP as shown below:

## Options

The Kamelet eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **name** | **Required** Name of the Kamelet (templateId/routeId) to call. Options for the kamelet can be specified using uri syntax, eg mynamecount=4&type=gold. |  | String |
| **outputs** | **Required** |  | List |

## Exchange properties

The Kamelet eip has no exchange properties.

## Using Kamelet EIP

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .kamelet("foo")
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:start"/>
    <kamelet name="foo"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - kamelet:
            name: foo
            steps:
              - to:
                  uri: mock:result
```

Camel will then, when starting:

-   Lookup the [Route Template](../../../manual/route-template.md) with the given id (in the example above its foo) from the `CamelContext`
    
-   Create a new route based on the [Route Template](../../../manual/route-template.md)
    

## Dependency

The implementation of the Kamelet EIP is located in the `camel-kamelet` JAR, so you should add the following dependency:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-kamelet</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.y.z</version>
</dependency>
```

## See Also

See the example [camel-example-kamelet](https://github.com/apache/camel-examples/tree/main/kamelet).
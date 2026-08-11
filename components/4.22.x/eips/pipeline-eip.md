# Pipeline

Camel supports the [Pipes and Filters](http://www.enterpriseintegrationpatterns.com/PipesAndFilters.md) from the [EIP patterns](enterprise-integration-patterns.md) in various ways.

![image](_images/eip/PipesAndFilters.gif)

With Camel, you can separate your processing across multiple independent [Endpoints](../../../manual/endpoint.md) which can then be chained together.

## Options

The Pipeline eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **outputs** | **Required** |  | List |

## Exchange properties

The Pipeline eip has no exchange properties.

## Using pipeline

You can create pipelines of logic using multiple [Endpoint](../../../manual/endpoint.md) or [Message Translator](message-translator.md) instances as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:cheese")
    .pipeline()
        .to("bean:foo")
        .to("bean:bar")
        .to("activemq:wine");
```

```xml
<route>
    <from uri="activemq:cheese"/>
    <pipeline>
        <to uri="bean:foo"/>
        <to uri="bean:bar"/>
        <to uri="activemq:wine"/>
    </pipeline>
</route>
```

```yaml
- route:
    from:
      uri: activemq:cheese
      steps:
        - pipeline:
            steps:
              - to:
                  uri: bean:foo
              - to:
                  uri: bean:bar
              - to:
                  uri: activemq:wine
```

Though a pipeline is the default mode of operation when you specify multiple outputs in Camel. Therefore, it’s much more common to see this with Camel:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:SomeQueue")
    .to("bean:foo")
    .to("bean:bar")
    .to("activemq:OutputQueue");
```

```xml
<route>
    <from uri="activemq:cheese"/>
    <to uri="bean:foo"/>
    <to uri="bean:bar"/>
    <to uri="activemq:wine"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:SomeQueue
      steps:
        - to:
            uri: bean:foo
        - to:
            uri: bean:bar
        - to:
            uri: activemq:OutputQueue
```

### Pipeline vs Multicast

The opposite to `pipeline` is [`multicast`](multicast-eip.md). A [Multicast](multicast-eip.md) EIP routes a copy of the same message into each of its outputs, where these messages are processed independently. Pipeline EIP, however, will route the same message sequentially in the pipeline where the output from the previous step is input to the next. The same principle from the Linux shell with chaining commands together with pipe (`|`).

### When using a pipeline is necessary

Using a pipeline becomes necessary when you need to group together a series of steps into a single logical step. For example, in the example below where [Multicast](multicast-eip.md) EIP is in use, to process the same message in two different pipelines. The first pipeline calls the something bean, and the second pipeline calls the foo and bar beans and then routes the message to another queue.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:SomeQueue")
    .multicast()
        .pipeline()
            .to("bean:something")
            .to("log:something")
        .end()
        .pipeline()
            .to("bean:foo")
            .to("bean:bar")
            .to("activemq:OutputQueue")
        .end()
    .end() // ends multicast
    .to("log:result");
```

Notice how we have to use `end()` to mark the end of the blocks.

```xml
<route>
  <from uri="activemq:SomeQueue"/>
  <multicast>
    <pipeline>
      <to uri="bean:something"/>
      <to uri="log:Something"/>
    </pipeline>
    <pipeline>
      <to uri="bean:foo"/>
      <to uri="bean:bar"/>
      <to uri="activemq:OutputQueue"/>
    </pipeline>
  </multicast>
  <to uri="log:result"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:SomeQueue
      steps:
        - multicast:
            steps:
              - pipeline:
                  steps:
                    - to:
                        uri: bean:something
                    - to:
                        uri: log:something
              - pipeline:
                  steps:
                    - to:
                        uri: bean:foo
                    - to:
                        uri: bean:bar
                    - to:
                        uri: activemq:OutputQueue
        - to:
            uri: log:result
```
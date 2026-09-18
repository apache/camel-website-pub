# To

Camel supports the [Message Endpoint](http://www.enterpriseintegrationpatterns.com/MessageEndpoint.md) from the [EIP patterns](enterprise-integration-patterns.md) using the [Endpoint](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.md) interface.

How does an application connect to a messaging channel to send and receive messages?

![image](_images/eip/MessageEndpointSolution.gif)

Connect an application to a messaging channel using a Message Endpoint, a client of the messaging system that the application can then use to send or receive messages.

In Camel the To EIP is used for sending [messages](message.md) to static [endpoints](message-endpoint.md).

The To and [ToD](toD-eip.md) EIPs are the most common patterns to use in Camel [routes](../../../manual/routes.md).

## Options

The To eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **variableSend** | To use a variable as the source for the message body to send. This makes it handy to use variables for user data and to easily control what data to use for sending and receiving. |  | String |
| **variableReceive** | To use a variable to store the received message body (only body, not headers). This makes it handy to use variables for user data and to easily control what data to use for sending and receiving. |  | String |
| **uri** | **Required** The uri of the endpoint to send to. |  | String |
| **pattern** | 
Sets the optional ExchangePattern to use. If not specified the default exchange pattern is used.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

## Exchange properties

The To eip supports the following exchange properties which are listed below.

The exchange properties are set on the `Exchange` by the EIP, unless otherwise specified in the description. This means those properties are available after this EIP has completed processing the `Exchange`.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelToEndpoint** | Endpoint URI where this Exchange is being sent to. |  | String |

## Different between To and ToD

The `to` is used for sending messages to a static [endpoint](message-endpoint.md). In other words `to` sends messages only to the **same** endpoint.

The `toD` is used for sending messages to a dynamic [endpoint](message-endpoint.md). The dynamic endpoint is evaluated _on-demand_ by an [Expression](../../../manual/expression.md). By default, the [Simple](../../4.22.x/languages/simple-language.md) expression is used to compute the dynamic endpoint URI.

> **Note**
> the Java DSL also provides a `toF` EIP, which can be used to avoid concatenating route parameters and making the code harder to read.

## Using To

The following example route demonstrates the use of a [File](../file-component.md) consumer endpoint and a [JMS](../jms-component.md) producer endpoint, by their [URIs](../../../manual/uris.md):

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:messages/foo")
    .to("jms:queue:foo");
```

```xml
<route>
    <from uri="file:messages/foo"/>
    <to uri="jms:queue:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: file:messages/foo
      steps:
        - to:
            uri: jms:queue:foo
```

## How to use a dynamic URI in to

A dynamic URI is an endpoint URI that varies depending on inflight routing information, such as Exchange properties, message headers, the body, the Camel Context, etc.

For example, if you’re using a Freemarker producer and the template location is provided inside the current message, you might expect the following code to work, **but it will not**.

> **Warning**
> **This is not valid code**
>
> This snippet is not valid code. Read on.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:messages/foo")
    .to("freemarker://templateHome/${body.templateName}.ftl")
    .to("jms:queue:foo");
```

```xml
<route>
    <from uri="file:messages/foo"/>
    <to uri="freemarker://templateHome/${body.templateName}.ftl"/>
    <to uri="jms:queue:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: file:messages/foo
      steps:
        - to:
            uri: "freemarker://templateHome/${body.templateName}.ftl"
        - to:
            uri: jms:queue:foo
```

In this case, you must use an EIP (Enterprise Integration Pattern) that is capable of computing a dynamic URI using an [Expression](../../../manual/expression.md), such as the [toD](../../4.22.x/eips/toD-eip.md) or [Recipient List](../../4.22.x/eips/recipientList-eip.md) EIP pattern.

> **Tip**
> **This is valid code**
>
> This snippet is valid code.

To fix the above problem we can use either toD or recipientList. Using toD is easier as shown below:

-   Java
    
-   XML
    
-   YAML
    

Use `toD` for dynamic URIs

```java
from("file:messages/foo")
    .toD("freemarker://templateHome/${body.templateName}.ftl")
    .to("jms:queue:foo");
```

Use `<toD>` for dynamic URIs

```xml
<route>
    <from uri="file:messages/foo"/>
    <toD uri="freemarker://templateHome/${body.templateName}.ftl"/>
    <to uri="jms:queue:foo"/>
</route>
```

Use `- toD:` for dynamic URIs

```yaml
- route:
    from:
      uri: file:messages/foo
      steps:
        - toD:
            uri: "freemarker://templateHome/${body.templateName}.ftl"
        - to:
            uri: jms:queue:foo
```

When using recipient list:

```java
.recipientList(simple("freemarker://templateHome/${body.templateName}.ftl"))
```

-   Java
    
-   XML
    
-   YAML
    

Use `recipientList` for more flexible and dynamic URIs

```java
from("file:messages/foo")
    .recipientList(simple("freemarker://templateHome/${body.templateName}.ftl"))
    .to("jms:queue:foo");
```

Use `<recipientList>` for more flexible and dynamic URIs

```xml
<route>
    <from uri="file:messages/foo"/>
    <recipientList>
        <simple>freemarker://templateHome/${body.templateName}.ftl</simple>
    </recipientList>
    <to uri="jms:queue:foo"/>
</route>
```

Use `- recipientList:` for more flexible and dynamic URIs

```yaml
- route:
    from:
      uri: file:messages/foo
      steps:
        - recipientList:
            expression:
              simple:
                expression: "freemarker://templateHome/${body.templateName}.ftl"
        - to:
            uri: jms:queue:foo
```
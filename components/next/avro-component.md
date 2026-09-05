# Avro RPC

**Since Camel 2.10**

**Both producer and consumer are supported**

This component provides support for Apache Avro’s rpc, by providing producers and consumers endpoint for using avro over netty or http. Before Camel 3.2 this functionality was a part of camel-avro component.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-avro-rpc</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The Avro RPC component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **protocol** (common) | Avro protocol to use. |  | Protocol |
| **protocolClassName** (common) | Avro protocol to use defined by the FQN class name. |  | String |
| **protocolLocation** (common) | Avro protocol location. |  | String |
| **reflectionProtocol** (common) | If the protocol object provided is reflection protocol. Should be used only with protocol parameter because for protocolClassName protocol type will be auto-detected. | false | boolean |
| **singleParameter** (common) | If true, consumer parameter won’t be wrapped into an array. Will fail if protocol specifies more than one parameter for the message. | false | boolean |
| **uriAuthority** (common) | Authority to use (username and password). |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | To use a shared AvroConfiguration to configure options once. |  | AvroConfiguration |
| **serializablePackages** (security) | Comma-separated list of additional packages that contain trusted Avro model classes. Avro 1.12 validates classes resolved from schemas; Camel automatically trusts org.apache.avro for IPC and packages derived from the configured protocol. Use this option for any additional model packages not inferred from the protocol. |  | String |

## Endpoint Options

The Avro RPC endpoint is configured using URI syntax:

avro:transport:host:port/messageName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **transport** (common) | 
**Required** Transport to use, can be either http or netty.

Enum values:

-   http
    
-   netty
    





 |  | AvroTransport |
| **port** (common) | **Required** Port number to use. |  | int |
| **host** (common) | **Required** Hostname to use. |  | String |
| **messageName** (common) | The name of the message to send. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **protocol** (common) | Avro protocol to use. |  | Protocol |
| **protocolClassName** (common) | Avro protocol to use defined by the FQN class name. |  | String |
| **protocolLocation** (common) | Avro protocol location. |  | String |
| **reflectionProtocol** (common) | If the protocol object provided is reflection protocol. Should be used only with protocol parameter because for protocolClassName protocol type will be auto-detected. | false | boolean |
| **singleParameter** (common) | If true, consumer parameter won’t be wrapped into an array. Will fail if protocol specifies more than one parameter for the message. | false | boolean |
| **uriAuthority** (common) | Authority to use (username and password). |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **serializablePackages** (security) | Comma-separated list of additional packages that contain trusted Avro model classes. Avro 1.12 validates classes resolved from schemas; Camel automatically trusts org.apache.avro for IPC and packages derived from the configured protocol. Use this option for any additional model packages not inferred from the protocol. |  | String |

## Message Headers

The Avro RPC component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAvroMessageName** (common) Constant: [`AVRO_MESSAGE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-avro-rpc/latest/org/apache/camel/component/avro/AvroConstants.html#AVRO_MESSAGE_NAME) | The name of the message to send. In consumer overrides message name from URI (if any). |  | String |

## Apache Avro Overview

Avro allows you to define message types and a protocol using a json like format and then generate java code for the specified types and messages. An example of how a schema looks like is below.

```json
{"namespace": "org.apache.camel.avro.generated",
 "protocol": "KeyValueProtocol",

 "types": [
     {"name": "Key", "type": "record",
      "fields": [
          {"name": "key",   "type": "string"}
      ]
     },
     {"name": "Value", "type": "record",
      "fields": [
          {"name": "value",   "type": "string"}
      ]
     }
 ],

 "messages": {
     "put": {
         "request": [{"name": "key", "type": "Key"}, {"name": "value", "type": "Value"} ],
         "response": "null"
     },
     "get": {
         "request": [{"name": "key", "type": "Key"}],
         "response": "Value"
     }
 }
}
```

You can easily generate classes from a schema, using maven, ant etc. More details can be found at the [Apache Avro documentation](http://avro.apache.org/docs/current/).

However, it doesn’t enforce a schema-first approach, and you can create schema for your existing classes. You can use existing protocol interfaces to make RCP calls. You should use interface for the protocol itself and POJO beans or primitive/String classes for parameter and result types. Here is an example of the class that corresponds to the schema above:

_Java-only: protocol interface and POJO class definition for Avro RPC_

```java
package org.apache.camel.avro.reflection;

public interface KeyValueProtocol {
    void put(String key, Value value);
    Value get(String key);
}

class Value {
    private String value;
    public String getValue() { return value; }
    public void setValue(String value) { this.value = value; }
}
```

_Note: Existing classes can be used only for RPC (see below), not in data format._

## Usage

### Using Avro RPC in Camel

As mentioned above, Avro also provides RPC support over multiple transports such as http and netty. Camel provides consumers and producers for these two transports.

avro:\[transport\]:\[host\]:\[port\]\[?options\]

The supported transport values are currently http or netty.

> **Note**
> You can specify the message name right in the URI:
>
> avro:\[transport\]:\[host\]:\[port\]\[/messageName\]\[?options\]

For consumers, this allows you to have multiple routes attached to the same socket. Dispatching to the correct route will be done by the avro component automatically. Route with no messageName specified (if any) will be used as default.

When using camel producers for avro ipc, the "in" message body needs to contain the parameters of the operation specified in the avro protocol. The response will be added in the body of the "out" message.

In a similar manner when using camel avro consumers for avro ipc, the request parameters will be placed inside the "in" message body of the created exchange. Once the exchange is processed, the body of the "out" message will be sent as a response.

**Note:** By default, consumer parameters are wrapped into an array. If you’ve got only one parameter, **since 2.12** you can use `singleParameter` URI option to receive it directly in the "in" message body without array wrapping.

## Examples

An example of using camel avro producers via http:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("avro:http:localhost:{{avroport}}?protocolClassName=org.apache.camel.avro.generated.KeyValueProtocol")
    .to("log:avro");
```

```xml
        <route>
            <from uri="direct:start"/>
            <to uri="avro:http:localhost:{{avroport}}?protocolClassName=org.apache.camel.avro.generated.KeyValueProtocol"/>
            <to uri="log:avro"/>
        </route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: avro:http:localhost:{{avroport}}
            parameters:
              protocolClassName: org.apache.camel.avro.generated.KeyValueProtocol
        - to:
            uri: log:avro
```

In the example above you need to fill `CamelAvroMessageName` header.

You can use the following syntax to call constant messages:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("avro:http:localhost:{{avroport}}/put?protocolClassName=org.apache.camel.avro.generated.KeyValueProtocol")
    .to("log:avro");
```

```xml
        <route>
            <from uri="direct:start"/>
            <to uri="avro:http:localhost:{{avroport}}/put?protocolClassName=org.apache.camel.avro.generated.KeyValueProtocol"/>
            <to uri="log:avro"/>
        </route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: avro:http:localhost:{{avroport}}/put
            parameters:
              protocolClassName: org.apache.camel.avro.generated.KeyValueProtocol
        - to:
            uri: log:avro
```

An example of consuming messages using camel avro consumers via netty:

-   Java
    
-   XML
    
-   YAML
    

```java
from("avro:netty:localhost:{{avroport}}?protocolClassName=org.apache.camel.avro.generated.KeyValueProtocol")
    .choice()
        .when().el("${in.headers.CamelAvroMessageName == 'put'}")
            .process("putProcessor")
        .when().el("${in.headers.CamelAvroMessageName == 'get'}")
            .process("getProcessor");
```

```xml
        <route>
            <from uri="avro:netty:localhost:{{avroport}}?protocolClassName=org.apache.camel.avro.generated.KeyValueProtocol"/>
            <choice>
                <when>
                    <el>${in.headers.CamelAvroMessageName == 'put'}</el>
                    <process ref="putProcessor"/>
                </when>
                <when>
                    <el>${in.headers.CamelAvroMessageName == 'get'}</el>
                    <process ref="getProcessor"/>
                </when>
            </choice>
        </route>
```

```yaml
- route:
    from:
      uri: avro:netty:localhost:{{avroport}}
      parameters:
        protocolClassName: org.apache.camel.avro.generated.KeyValueProtocol
      steps:
        - choice:
            when:
              - el: "${in.headers.CamelAvroMessageName == 'put'}"
                steps:
                  - process:
                      ref: putProcessor
              - el: "${in.headers.CamelAvroMessageName == 'get'}"
                steps:
                  - process:
                      ref: getProcessor
```

You can set up two distinct routes to perform the same task:

-   Java
    
-   XML
    
-   YAML
    

```java
from("avro:netty:localhost:{{avroport}}/put?protocolClassName=org.apache.camel.avro.generated.KeyValueProtocol")
    .process("putProcessor");

from("avro:netty:localhost:{{avroport}}/get?protocolClassName=org.apache.camel.avro.generated.KeyValueProtocol&singleParameter=true")
    .process("getProcessor");
```

```xml
        <route>
            <from uri="avro:netty:localhost:{{avroport}}/put?protocolClassName=org.apache.camel.avro.generated.KeyValueProtocol">
            <process ref="putProcessor"/>
        </route>
        <route>
            <from uri="avro:netty:localhost:{{avroport}}/get?protocolClassName=org.apache.camel.avro.generated.KeyValueProtocol&singleParameter=true"/>
            <process ref="getProcessor"/>
        </route>
```

```yaml
- route:
    from:
      uri: avro:netty:localhost:{{avroport}}/put
      parameters:
        protocolClassName: org.apache.camel.avro.generated.KeyValueProtocol
      steps:
        - process:
            ref: putProcessor
- route:
    from:
      uri: avro:netty:localhost:{{avroport}}/get
      parameters:
        protocolClassName: org.apache.camel.avro.generated.KeyValueProtocol
        singleParameter: true
      steps:
        - process:
            ref: getProcessor
```

In the example above, get takes only one parameter, so `singleParameter` is used and `getProcessor` will receive Value class directly in body, while `putProcessor` will receive an array of size 2 with `String` key and `Value` value filled as array contents.

### Avro via HTTP SPI

The Avro RPC component offers the `org.apache.camel.component.avro.spi.AvroRpcHttpServerFactory` service provider interface (SPI) so that various platforms can provide their own implementation based on their native HTTP server.

The default implementation available in `org.apache.camel:camel-avro-jetty` is based on `org.apache.avro:avro-ipc-jetty`.
# XMPP

**Since Camel 1.0**

**Both producer and consumer are supported**

The XMPP component implements an XMPP (Jabber) transport.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-xmpp</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

xmpp://\[login@\]hostname\[:port\]\[/participant\]\[?Options\]

The component supports both room based and private person-person conversations.  
The component supports both producer and consumer (you can get messages from XMPP or send messages to XMPP). Consumer mode supports rooms starting.

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

The XMPP component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The XMPP endpoint is configured using URI syntax:

xmpp:host:port/participant

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | **Required** Hostname for the chat server. |  | String |
| **port** (common) | **Required** Port number for the chat server. |  | int |
| **participant** (common) | JID (Jabber ID) of person to receive messages. room parameter has precedence over participant. |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **login** (common) | Whether to login the user. | true | boolean |
| **nickname** (common) | Use nickname when joining room. If room is specified and nickname is not, user will be used for the nickname. |  | String |
| **pubsub** (common) | Accept pubsub packets on input, default is false. | false | boolean |
| **room** (common) | If this option is specified, the component will connect to MUC (Multi User Chat). Usually, the domain name for MUC is different from the login domain. For example, if you are supermanjabber.org and want to join the krypton room, then the room URL is kryptonconference.jabber.org. Note the conference part. It is not a requirement to provide the full room JID. If the room parameter does not contain the symbol, the domain part will be discovered and added by Camel. |  | String |
| **serviceName** (common) | The name of the service you are connecting to. For Google Talk, this would be gmail.com. |  | String |
| **testConnectionOnStartup** (common) | Specifies whether to test the connection on startup. This is used to ensure that the XMPP client has a valid connection to the XMPP server when the route starts. Camel throws an exception on startup if a connection cannot be established. When this option is set to false, Camel will attempt to establish a lazy connection when needed by a producer, and will poll for a consumer connection until the connection is established. Default is true. | true | boolean |
| **createAccount** (common (advanced)) | If true, an attempt to create an account will be made. Default is false. | false | boolean |
| **resource** (common (advanced)) | XMPP resource. The default is Camel. | Camel | String |
| **connectionPollDelay** (consumer) | The amount of time in seconds between polls (in seconds) to verify the health of the XMPP connection, or between attempts to establish an initial consumer connection. Camel will try to re-establish a connection if it has become inactive. Default is 10 seconds. | 10 | int |
| **doc** (consumer) | Set a doc header on the IN message containing a Document form of the incoming packet; default is true if presence or pubsub are true, otherwise false. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connectionConfig** (advanced) | To use an existing connection configuration. Currently org.jivesoftware.smack.tcp.XMPPTCPConnectionConfiguration is only supported (XMPP over TCP). |  | ConnectionConfiguration |
| **headerFilterStrategy** (filter) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **password** (security) | Password for login. |  | String |
| **roomPassword** (security) | Password for room. |  | String |
| **user** (security) | User name (without server name). If not specified, anonymous login will be attempted. |  | String |

## Message Headers

The XMPP component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelXmppDoc** (consumer) Constant: [`DOC_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-xmpp/latest/org/apache/camel/component/xmpp/XmppConstants.html#DOC_HEADER) | The XMPP message. |  | Message |

## Usage

### Headers and setting Subject or Language

Camel sets the message IN headers as properties on the XMPP message. You can configure a `HeaderFilterStategy` if you need custom filtering of headers. The **Subject** and **Language** of the XMPP message are also set if they are provided as IN headers.

## Examples

User `superman` to join room `krypton` at `jabber` server with password, `secret`:

xmpp://superman@jabber.org/?room=krypton@conference.jabber.org&password=secret

User `superman` to send messages to `joker`:

xmpp://superman@jabber.org/joker@jabber.org?password=secret

Routing example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("timer://kickoff?period=10000")
    .setBody(constant("I will win! Your Superman."))
    .to("xmpp://superman@jabber.org/joker@jabber.org?password=secret");
```

```xml
<route>
  <from uri="timer://kickoff?period=10000"/>
  <setBody>
    <constant>I will win! Your Superman.</constant>
  </setBody>
  <to uri="xmpp://superman@jabber.org/joker@jabber.org?password=secret"/>
</route>
```

```yaml
- route:
    from:
      uri: timer:kickoff
      parameters:
        period: 10000
      steps:
        - setBody:
            constant: "I will win! Your Superman."
        - to:
            uri: xmpp://superman@jabber.org/joker@jabber.org
            parameters:
              password: secret
```

Consumer configuration, which writes all messages from `joker` into the queue, `evil.talk`.

-   Java
    
-   XML
    
-   YAML
    

```java
from("xmpp://superman@jabber.org/joker@jabber.org?password=secret")
    .to("activemq:evil.talk");
```

```xml
<route>
  <from uri="xmpp://superman@jabber.org/joker@jabber.org?password=secret"/>
  <to uri="activemq:evil.talk"/>
</route>
```

```yaml
- route:
    from:
      uri: xmpp://superman@jabber.org/joker@jabber.org
      parameters:
        password: secret
      steps:
        - to:
            uri: activemq:evil.talk
```

Consumer configuration, which listens to room messages:

-   Java
    
-   XML
    
-   YAML
    

```java
from("xmpp://superman@jabber.org/?password=secret&room=krypton@conference.jabber.org")
    .to("activemq:krypton.talk");
```

```xml
<route>
  <from uri="xmpp://superman@jabber.org/?password=secret&amp;room=krypton@conference.jabber.org"/>
  <to uri="activemq:krypton.talk"/>
</route>
```

```yaml
- route:
    from:
      uri: xmpp://superman@jabber.org/
      parameters:
        password: secret
        room: "krypton@conference.jabber.org"
      steps:
        - to:
            uri: activemq:krypton.talk
```

Room in short notation (no domain part):

-   Java
    
-   XML
    
-   YAML
    

```java
from("xmpp://superman@jabber.org/?password=secret&room=krypton")
    .to("activemq:krypton.talk");
```

```xml
<route>
  <from uri="xmpp://superman@jabber.org/?password=secret&amp;room=krypton"/>
  <to uri="activemq:krypton.talk"/>
</route>
```

```yaml
- route:
    from:
      uri: xmpp://superman@jabber.org/
      parameters:
        password: secret
        room: krypton
      steps:
        - to:
            uri: activemq:krypton.talk
```

When connecting to the Google Chat service, you’ll need to specify the `serviceName` as well as your credentials:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("xmpp://talk.google.com:5222/touser@gmail.com?serviceName=gmail.com&user=fromuser&password=secret")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="xmpp://talk.google.com:5222/touser@gmail.com?serviceName=gmail.com&amp;user=fromuser&amp;password=secret"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: xmpp://talk.google.com:5222/touser@gmail.com
            parameters:
              serviceName: gmail.com
              user: fromuser
              password: secret
        - to:
            uri: mock:result
```
# Shell

**Since Camel 4.21**

**Only consumer is supported**

The Shell component provides an interactive terminal prompt using [JLine](https://github.com/jline/jline3). It allows Camel routes to read user input line-by-line (consumer) and write output back to the terminal.

Each line typed by the user becomes the body of a Camel `Exchange` that is routed normally. The response (exchange body after routing) is printed back to the terminal. Typing `exit` or sending EOF (Ctrl+D) shuts down the Camel context.

## Dependencies

Maven users need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-shell</artifactId>
    <version>${camel-version}</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

```none
shell:prompt[?options]
```

Where `prompt` is the label displayed before the `>` cursor. For example, `shell:myapp` displays \`myapp> \`.

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

The Shell component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **bannerResource** (advanced) | Classpath resource path to a custom banner text file. | camel-shell-banner.txt | String |
| **showBanner** (advanced) | Whether to print the Camel banner on startup. | true | boolean |

## Endpoint Options

The Shell endpoint is configured using URI syntax:

shell:prompt

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **prompt** (consumer) | **Required** Shell prompt. |  | String |

### Query Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **color** (consumer) | Prompt color: black, red, green, yellow, blue, magenta, cyan, white. | cyan | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

## Usage

### Consumer

The shell consumer starts an interactive terminal session. Each line typed by the user is set as the body of a new `Exchange` and sent through the route. The route result body is then printed back to the terminal.

Errors occurring in the route are displayed in red.

## Examples

### Chat with an LLM

-   Java
    
-   XML
    
-   YAML
    

```java
from("shell:myapp?color=green")
    .to("huggingface:chat?modelId=Qwen/Qwen2.5-3B-Instruct");
```

```xml
<route>
  <from uri="shell:myapp?color=green"/>
  <to uri="huggingface:chat?modelId=Qwen/Qwen2.5-3B-Instruct"/>
</route>
```

```yaml
- route:
    from:
      uri: shell:myapp
      parameters:
        color: green
      steps:
        - to:
            uri: huggingface:chat
            parameters:
              modelId: Qwen/Qwen2.5-3B-Instruct
```

### Call a REST API

-   Java
    
-   XML
    
-   YAML
    

```java
from("shell:myapp")
    .toD("http://api.example.com/chat?query=${body}");
```

```xml
<route>
  <from uri="shell:myapp"/>
  <toD uri="http://api.example.com/chat?query=${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: shell:myapp
      steps:
        - toD:
            uri: "http://api.example.com/chat?query=${body}"
```

### Route to JMS (fire-and-forget)

_Java-only: using ExchangePattern.InOnly with shell consumer_

```java
from("shell:myapp")
    .setProperty("input", body())
    .to(ExchangePattern.InOnly, "activemq:queue:myqueue")
    .setBody(simple("Sent '${exchangeProperty.input}' to queue"));
```
# Cron

**Since Camel 3.1**

**Only consumer is supported**

The Cron component is a generic interface component that allows triggering events at a specific time interval specified using the Unix cron syntax (e.g. `0/2 * * * * ?` to trigger an event every two seconds).

As an interface component, the Cron component does not contain a default implementation. Instead, it requires that the users plug the implementation of their choice.

The following standard Camel components support the Cron endpoints:

-   [Camel Quartz](quartz-component.md)
    
-   [Camel Spring](spring-summary.md)
    

The Cron component is also supported in **Camel K**, which can use the Kubernetes scheduler to trigger the routes when required by the cron expression. Camel K does not require additional libraries to be plugged when using cron expressions compatible with Kubernetes cron syntax.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-cron</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

Additional libraries may be needed to plug a specific implementation.

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

The Cron component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **cronService** (advanced) | The id of the CamelCronService to use when multiple implementations are provided. |  | String |

## Endpoint Options

The Cron endpoint is configured using URI syntax:

cron:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (consumer) | **Required** The name of the cron trigger. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **schedule** (consumer) | **Required** A cron expression that will be used to generate events. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

## Usage

The component can be used to trigger events at specified times, as in the following example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("cron:tab?schedule=0/1+*+*+*+*+?")
.setBody().constant("event")
.log("${body}");
```

```xml
<route>
    <from uri="cron:tab?schedule=0/1+*+*+*+*+?"/>
    <setBody>
      <constant>event</constant>
    </setBody>
    <to uri="log:info"/>
</route>
```

```yaml
- route:
    from:
      uri: cron:tab
      parameters:
        schedule: "0/1+*+*+*+*+?"
      steps:
        - setBody:
            constant:
              expression: event
        - to:
            uri: log:info
```

The schedule expression `0/3+10+*+*+*+?` can be also written as `0/3 10 * * * ?` and triggers an event every three seconds only in the tenth minute of each hour.

Breaking down the parts in the schedule expression(in order):

-   Seconds (optional)
    
-   Minutes
    
-   Hours
    
-   Day of month
    
-   Month
    
-   Day of the week
    
-   Year (optional)
    

Schedule expressions can be made of five to seven parts. When expressions are composed of six parts, the first items is the _Seconds_ part (and year is considered missing).

Other valid examples of schedule expressions are:

-   `0/2 * * * ?` (Five parts, an event every two minutes)
    
-   `0 0/2 * * * MON-FRI 2030` (Seven parts, an event every two minutes only in the year 2030)
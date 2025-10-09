# OSGi PAX Logging Component (deprecated)

**Since Camel 2.6**

**Only consumer is supported**

The PAX Logging component can be used in an OSGi environment to receive [PaxLogging](http://wiki.ops4j.org/display/paxlogging/Pax+Logging) events and process them.

## Dependencies

Maven users need to add the following dependency to their `pom.xml`

```xml
<dependency>
  <groupId>org.apache.camel.karaf</groupId>
  <artifactId>camel-paxlogging</artifactId>
  <version>${camel-version}</version>
</dependency>
```

where `${camel-version`} must be replaced by the actual version of Camel.

## URI format

```xml
paxlogging:appender[?options]
```

where `appender` is the name of the pax appender that need to be configured in the PaxLogging service configuration.

## URI options

The OSGi PAX Logging component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **bundleContext** (consumer) | The OSGi BundleContext is automatic injected by Camel |  | BundleContext |
| **basicPropertyBinding** (advanced) | Whether the component should use basic property binding (Camel 2.x) or the newer property binding with additional capabilities | false | boolean |

The OSGi PAX Logging endpoint is configured using URI syntax:

paxlogging:appender

with the following path and query parameters:

### Path Parameters (1 parameters):

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **appender** | **Required** Appender is the name of the pax appender that need to be configured in the PaxLogging service configuration. |  | String |

### Query Parameters (5 parameters):

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer) | Sets the exchange pattern when the consumer creates an exchange. The value can be one of: InOnly, InOut, InOptionalOut |  | ExchangePattern |
| **basicPropertyBinding** (advanced) | Whether the endpoint should use basic property binding (Camel 2.x) or the newer property binding with additional capabilities | false | boolean |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used, or Camel is allowed to use asynchronous processing (if supported). | false | boolean |

## Message body

The `in` message body will be set to the received PaxLoggingEvent.

## Example usage

```xml
<route>
    <from uri="paxlogging:camel"/>
    <to uri="stream:out"/>
</route>
```

Configuration:

```java
log4j.rootLogger=INFO, out, osgi:VmLogAppender, osgi:camel
```
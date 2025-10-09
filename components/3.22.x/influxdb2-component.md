# InfluxDB2

**Since Camel 3.20**

**Only producer is supported**

This component allows you to interact with InfluxDB 2.x [https://influxdata.com/time-series-platform/influxdb/](https://influxdata.com/time-series-platform/influxdb/) a time series database. The native body type for this component is Point (the native influxdb class), but it can also accept Map<String, Object> as message body and it will get converted to Point.class, please note that the map must contain an element with InfluxDbConstants.MEASUREMENT\_NAME as key.

Additionally, of course you may register your own Converters to your data type to Point, or use the (un)marshalling tools provided by camel.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-influxdb2</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

influxdb2://connectionBean?\[options\]

The producer allows sending messages to a influxdb configured in the registry, using the native java driver.

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

The InfluxDB2 component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **influxDBClient** (producer) | **Autowired** The shared Influx DB to use for all endpoints. |  | InfluxDBClient |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The InfluxDB2 endpoint is configured using URI syntax:

influxdb2:connectionBean

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionBean** (producer) | **Required** Connection to the Influx database, of class com.influxdb.client.InfluxDBClient.class. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateBucket** (producer) | Define if we want to auto create the bucket if it’s not present. | true | boolean |
| **autoCreateOrg** (producer) | Define if we want to auto create the organization if it’s not present. | true | boolean |
| **bucket** (producer) | **Required** The name of the bucket where the time series will be stored. |  | String |
| **operation** (producer) | 
Define if this operation is an insert of ping.

Enum values:

-   INSERT
    
-   PING
    





 | INSERT | Operation |
| **org** (producer) | **Required** The name of the organization where the time series will be stored. |  | String |
| **retentionPolicy** (producer) | Define the retention policy to the data created by the endpoint. | default | String |
| **writePrecision** (producer) | 

The format or precision of time series timestamps.

Enum values:

-   ms
    
-   s
    
-   us
    
-   ns
    





 | ms | WritePrecision |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The InfluxDB2 component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelInfluxDB2MeasurementName** (producer) Constant: [`MEASUREMENT`](https://javadoc.io/doc/org.apache.camel/camel-influxdb2/latest/org/apache/camel/component/influxdb2/InfluxDb2Constants.html#MEASUREMENT) | The name of measurement. |  | String |
| **camelInfluxDB.RetentionPolicy** (producer) Constant: [`RETENTION_POLICY`](https://javadoc.io/doc/org.apache.camel/camel-influxdb2/latest/org/apache/camel/component/influxdb2/InfluxDb2Constants.html#RETENTION_POLICY) | The string that defines the retention policy to the data created by the endpoint. |  | String |
| **CamelInfluxDB2WritePrecision** (producer) Constant: [`WRITE_PRECISION`](https://javadoc.io/doc/org.apache.camel/camel-influxdb2/latest/org/apache/camel/component/influxdb2/InfluxDb2Constants.html#WRITE_PRECISION) | 
InfluxDb Write precision.

Enum values:

-   ms
    
-   s
    
-   us
    
-   ns
    





 |  | WritePrecision |

## Example

Below is an example route that stores a point into the db (taking the db name from the URI) specific key:

```java
from("direct:start")
        .to("influxdb2://connectionBean?org=<org>&bucket=<bucket>");
```

```java
from("direct:start")
        .setHeader(InfluxDbConstants.ORG, "myTestOrg")
        .setHeader(InfluxDbConstants.BUCKET, "myTestBucket")
        .to("influxdb2://connectionBean?");
```

## Spring Boot Auto-Configuration

When using influxdb2 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-influxdb2-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.influxdb2.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.influxdb2.enabled** | Whether to enable auto configuration of the influxdb2 component. This is enabled by default. |  | Boolean |
| **camel.component.influxdb2.influx-d-b-client** | The shared Influx DB to use for all endpoints. The option is a com.influxdb.client.InfluxDBClient type. |  | InfluxDBClient |
| **camel.component.influxdb2.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
# InfluxDB

**Since Camel 2.18**

**Only producer is supported**

This component allows you to interact with [InfluxDB](https://influxdata.com/time-series-platform/influxdb/) v1, a time series database.

The native body type for this component is `Point` (the native influxdb class). However, it can also accept `Map<String, Object>` as message body, and it will get converted to `Point.class`, please note that the map must contain an element with `camelInfluxDB.MeasurementName` as key.

Additionally, you may register your own Converters to your data type to `Point`, or use the (un)marshalling tools provided by Camel.

> **Note**
> For InfluxDB v2 check the [InfluxDB2 component](influxdb2-component.md).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-influxdb</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

influxdb://beanName?\[options\]

The producer allows sending messages to an InfluxDB configured in the registry, using the native java driver.

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

The InfluxDB component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **influxDB** (producer) | **Autowired** The shared Influx DB to use for all endpoints. |  | InfluxDB |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The InfluxDB endpoint is configured using URI syntax:

influxdb:connectionBean

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionBean** (producer) | **Required** Connection to the influx database, of class InfluxDB.class. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateDatabase** (producer) | Define if we want to auto create the database if it’s not present. | false | boolean |
| **batch** (producer) | Define if this operation is a batch operation or not. | false | boolean |
| **checkDatabaseExistence** (producer) | Define if we want to check the database existence while starting the endpoint. | false | boolean |
| **databaseName** (producer) | The name of the database where the time series will be stored. |  | String |
| **operation** (producer) | Define if this operation is an insert or a query. | insert | String |
| **query** (producer) | Define the query in case of operation query. |  | String |
| **retentionPolicy** (producer) | The string that defines the retention policy to the data created by the endpoint. | default | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The InfluxDB component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camelInfluxDB.RetentionPolicy** (producer) Constant: [`RETENTION_POLICY_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-influxdb/latest/org/apache/camel/component/influxdb/InfluxDbConstants.html#RETENTION_POLICY_HEADER) | The string that defines the retention policy to the data created by the endpoint. |  | String |
| **camelInfluxDB.databaseName** (producer) Constant: [`DBNAME_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-influxdb/latest/org/apache/camel/component/influxdb/InfluxDbConstants.html#DBNAME_HEADER) | The name of the database where the time series will be stored. |  | String |
| **camelInfluxDB.query** (producer) Constant: [`INFLUXDB_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-influxdb/latest/org/apache/camel/component/influxdb/InfluxDbConstants.html#INFLUXDB_QUERY) | Define the query in case of operation query. |  | String |

## Example

Below is an example route that stores a point into the db (taking the db name from the URI) specific key:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
        .to("influxdb://connectionBean?databaseName=myTimeSeriesDB");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="influxdb://connectionBean?databaseName=myTimeSeriesDB"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: influxdb://connectionBean
            parameters:
              databaseName: myTimeSeriesDB
```
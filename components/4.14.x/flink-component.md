# Flink

**Since Camel 2.18**

**Only producer is supported**

This documentation page covers the [Apache Flink](https://flink.apache.org) component for the Apache Camel. The **camel-flink** component provides a bridge between Camel components and Flink tasks. This component provides a way to route a message from various transports, dynamically choosing a flink task to execute, use an incoming message as input data for the task and finally deliver the results back to the Camel pipeline.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-flink</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

Currently, the Flink Component supports only Producers. One can create DataSet, DataStream jobs.

flink:dataset?dataset=#myDataSet&dataSetCallback=#dataSetCallback
flink:datastream?datastream=#myDataStream&dataStreamCallback=#dataStreamCallback

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

The Flink component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataSetCallback** (producer) | Function performing action against a DataSet. |  | DataSetCallback |
| **dataStream** (producer) | DataStream to compute against. |  | DataStream |
| **dataStreamCallback** (producer) | Function performing action against a DataStream. |  | DataStreamCallback |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Flink endpoint is configured using URI syntax:

flink:endpointType

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpointType** (producer) | 
**Required** Type of the endpoint (dataset, datastream).

Enum values:

-   dataset
    
-   datastream
    





 |  | EndpointType |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collect** (producer) | Indicates if results should be collected or counted. | true | boolean |
| **dataSet** (producer) | DataSet to compute against. |  | DataSet |
| **dataSetCallback** (producer) | Function performing action against a DataSet. |  | DataSetCallback |
| **dataStream** (producer) | DataStream to compute against. |  | DataStream |
| **dataStreamCallback** (producer) | Function performing action against a DataStream. |  | DataStreamCallback |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Flink component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelFlinkDataSet** (producer) Constant: [`FLINK_DATASET_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-flink/latest/org/apache/camel/component/flink/FlinkConstants.html#FLINK_DATASET_HEADER) | The dataset. |  | Object |
| **CamelFlinkDataSetCallback** (producer) Constant: [`FLINK_DATASET_CALLBACK_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-flink/latest/org/apache/camel/component/flink/FlinkConstants.html#FLINK_DATASET_CALLBACK_HEADER) | The dataset callback. |  | DataSetCallback |
| **CamelFlinkDataStream** (producer) Constant: [`FLINK_DATASTREAM_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-flink/latest/org/apache/camel/component/flink/FlinkConstants.html#FLINK_DATASTREAM_HEADER) | The data stream. |  | Object |
| **CamelFlinkDataStreamCallback** (producer) Constant: [`FLINK_DATASTREAM_CALLBACK_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-flink/latest/org/apache/camel/component/flink/FlinkConstants.html#FLINK_DATASTREAM_CALLBACK_HEADER) | The data stream callback. |  | DataStreamCallback |

## Examples

### Flink DataSet Callback

```java
@Bean
public DataSetCallback<Long> dataSetCallback() {
    return new DataSetCallback<Long>() {
        public Long onDataSet(DataSet dataSet, Object... objects) {
            try {
                 dataSet.print();
                 return new Long(0);
            } catch (Exception e) {
                 return new Long(-1);
            }
        }
    };
}
```

### Flink DataStream Callback

```java
@Bean
public VoidDataStreamCallback dataStreamCallback() {
    return new VoidDataStreamCallback() {
        @Override
        public void doOnDataStream(DataStream dataStream, Object... objects) throws Exception {
            dataStream.flatMap(new Splitter()).print();

            environment.execute("data stream test");
        }
    };
}
```

### Camel-Flink Producer call

```java
CamelContext camelContext = new SpringCamelContext(context);

String pattern = "foo";

try {
    ProducerTemplate template = camelContext.createProducerTemplate();
    camelContext.start();
    Long count = template.requestBody("flink:dataSet?dataSet=#myDataSet&dataSetCallback=#countLinesContaining", pattern, Long.class);
    } finally {
        camelContext.stop();
    }
```

## Spring Boot Auto-Configuration

When using flink with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-flink-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.flink.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.flink.data-set-callback** | Function performing action against a DataSet. The option is a org.apache.camel.component.flink.DataSetCallback type. |  | DataSetCallback |
| **camel.component.flink.data-stream** | DataStream to compute against. The option is a org.apache.flink.streaming.api.datastream.DataStream type. |  | DataStream |
| **camel.component.flink.data-stream-callback** | Function performing action against a DataStream. The option is a org.apache.camel.component.flink.DataStreamCallback type. |  | DataStreamCallback |
| **camel.component.flink.enabled** | Whether to enable auto configuration of the flink component. This is enabled by default. |  | Boolean |
| **camel.component.flink.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
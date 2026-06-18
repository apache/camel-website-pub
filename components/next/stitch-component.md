# Stitch

**Since Camel 3.8**

**Only producer is supported**

Stitch is a cloud ETL service, a developer-focused platform for rapidly moving and replicates data from more than 90 applications and databases. It integrates various data sources into a central data warehouse. Stitch has integrations for many enterprise software data sources, and can receive data via WebHooks and an API (Stitch Import API) which Camel Stitch Component uses to produce the data to Stitch ETL.

For more info, feel free to visit their [website](https://www.stitchdata.com/)

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-stitch</artifactId>
    <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

stitch:\[tableName\]//\[?options\]

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

The Stitch component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The component configurations. |  | StitchConfiguration |
| **keyNames** (producer) | A collection of comma separated strings representing the Primary Key fields in the source table. Stitch use these Primary Keys to de-dupe data during loading If not provided, the table will be loaded in an append-only manner. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **region** (producer) | 
Stitch account region, e.g: europe.

Enum values:

-   NORTH\_AMERICA
    
-   EUROPE
    





 | EUROPE | StitchRegion |
| **stitchSchema** (producer) | **Autowired** A schema that describes the record(s). |  | StitchSchema |
| **connectionProvider** (producer (advanced)) | **Autowired** ConnectionProvider contain configuration for the HttpClient like Maximum connection limit .. etc, you can inject this ConnectionProvider and the StitchClient will initialize HttpClient with this ConnectionProvider. |  | ConnectionProvider |
| **httpClient** (producer (advanced)) | **Autowired** Reactor Netty HttpClient, you can injected it if you want to have custom HttpClient. |  | HttpClient |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **stitchClient** (advanced) | **Autowired** Set a custom StitchClient that implements org.apache.camel.component.stitch.client.StitchClient interface. |  | StitchClient |
| **token** (security) | **Required** Stitch access token for the Stitch Import API. |  | String |

## Endpoint Options

The Stitch endpoint is configured using URI syntax:

stitch:tableName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **tableName** (producer) | The name of the destination table the data is being pushed to. Table names must be unique in each destination schema, or loading issues will occur. Note: The number of characters in the table name should be within the destination’s allowed limits or data will rejected. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **keyNames** (producer) | A collection of comma separated strings representing the Primary Key fields in the source table. Stitch use these Primary Keys to de-dupe data during loading If not provided, the table will be loaded in an append-only manner. |  | String |
| **region** (producer) | 
Stitch account region, e.g: europe.

Enum values:

-   NORTH\_AMERICA
    
-   EUROPE
    





 | EUROPE | StitchRegion |
| **stitchSchema** (producer) | **Autowired** A schema that describes the record(s). |  | StitchSchema |
| **connectionProvider** (producer (advanced)) | **Autowired** ConnectionProvider contain configuration for the HttpClient like Maximum connection limit .. etc, you can inject this ConnectionProvider and the StitchClient will initialize HttpClient with this ConnectionProvider. |  | ConnectionProvider |
| **httpClient** (producer (advanced)) | **Autowired** Reactor Netty HttpClient, you can injected it if you want to have custom HttpClient. |  | HttpClient |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **stitchClient** (advanced) | **Autowired** Set a custom StitchClient that implements org.apache.camel.component.stitch.client.StitchClient interface. |  | StitchClient |
| **token** (security) | **Required** Stitch access token for the Stitch Import API. |  | String |

## Message Headers

The Stitch component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelStitchTableName** (producer) Constant: [`TABLE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-stitch/latest/org/apache/camel/component/stitch/StitchConstants.html#TABLE_NAME) | The name of the destination table the data is being pushed to. Table names must be unique in each destination schema, or loading issues will occur. Note: The number of characters in the table name should be within the destinations allowed limits or data will rejected. |  | String |
| **CamelStitchSchema** (producer) Constant: [`SCHEMA`](https://javadoc.io/doc/org.apache.camel/camel-stitch/latest/org/apache/camel/component/stitch/StitchConstants.html#SCHEMA) | The schema that describes the Stitch message. |  | StitchSchema or Map |
| **CamelStitchKeyNames** (producer) Constant: [`KEY_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-stitch/latest/org/apache/camel/component/stitch/StitchConstants.html#KEY_NAMES) | A collection of strings representing the Primary Key fields in the source table. Stitch use these Primary Keys to de-dupe data during loading If not provided, the table will be loaded in an append-only manner. |  | Collection |
| **CamelStitchCode** (producer) Constant: [`CODE`](https://javadoc.io/doc/org.apache.camel/camel-stitch/latest/org/apache/camel/component/stitch/StitchConstants.html#CODE) | HTTP Status code that is returned from Stitch Import HTTP API. |  | Integer |
| **CamelStitchHeaders** (producer) Constant: [`HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-stitch/latest/org/apache/camel/component/stitch/StitchConstants.html#HEADERS) | HTTP headers that are returned from Stitch Import HTTP API. |  | Map |
| **CamelStitchStatus** (producer) Constant: [`STATUS`](https://javadoc.io/doc/org.apache.camel/camel-stitch/latest/org/apache/camel/component/stitch/StitchConstants.html#STATUS) | The status message that Stitch returns after sending the data through Stitch Import API. |  | String |

## Usage

### Prerequisites

You must have a valid Stitch account, you will need to enable Stitch Import API and generate a token for the integration, for more info, please find more info [here](https://www.stitchdata.com/docs/developers/import-api/guides/quick-start).

### Async Producer

This component implements the async Consumer and producer.

This allows camel route to consume and produce events asynchronously without blocking any threads.

Example showing how to produce data to Stitch from a custom processor:

```java
from("direct:sendStitch")
     .process(exchange -> {
         final StitchMessage stitchMessage = StitchMessage.builder()
               .withData("field_1", "stitchMessage2-1")
               .build();

         final StitchRequestBody stitchRequestBody = StitchRequestBody.builder()
                .addMessage(stitchMessage)
                .withSchema(StitchSchema.builder().addKeyword("field_1", "string").build())
                .withTableName("table_1")
                .withKeyNames(Collections.singleton("field_1"))
                .build();

                exchange.getMessage().setBody(stitchRequestBody);
     })
.to("stitch:table_1?token=RAW({{token}})");
```

### Message body type

Currently, the component supports the following types for the body message on the producer side when producing a message to Stitch component:

-   `org.apache.camel.component.stitch.client.models.StitchRequestBody`: This represents this Stitch [JSON Message](https://www.stitchdata.com/docs/developers/import-api/api#batch-data—​arguments). However, `StitchRequestBody` includes a type safe builder that helps on building the request body. Please note that, `tableName`, `keyNames` and `schema` options are no longer required if you send the data with `StitchRequestBody`, if you still set these options, they override whatever being set in message body `StitchRequestBody`.
    
-   `org.apache.camel.component.stitch.client.models.StitchMessage`: This represents [this Stitch message structure](https://www.stitchdata.com/docs/developers/import-api/api#message-object). If you choose to send your message as `StitchMessage`, **you will need** to add `tableName`, `keyNames` and `schema` options to either the Exchange headers or through the endpoint options.
    
-   `Map`: You can also send the data as `Map`, the data structure must follow this [JSON Message](https://www.stitchdata.com/docs/developers/import-api/api#batch-data—​arguments) structure which is similar to `StitchRequestBody` but with drawback losing on all the type safety builder that is included with `StitchRequestBody`.
    
-   `Iterable`: You can send multiple Stitch messages that are aggregated by Camel or aggregated through custom processor. These aggregated messages can be type of `StitchMessage`, `StitchRequestBody` or `Map` but this Map here is similar to `StitchMessage`.
    

### Examples

Here is list of examples showing data that can be proceeded to Stitch:

#### Input body type `org.apache.camel.component.stitch.client.models.StitchRequestBody`:

_Java-only: Java lambda Processor with Stitch SDK builders_

```java
from("direct:sendStitch")
     .process(exchange -> {
         final StitchMessage stitchMessage = StitchMessage.builder()
               .withData("field_1", "stitchMessage2-1")
               .build();

         final StitchRequestBody stitchRequestBody = StitchRequestBody.builder()
                .addMessage(stitchMessage)
                .withSchema(StitchSchema.builder().addKeyword("field_1", "string").build())
                .withTableName("table_1")
                .withKeyNames(Collections.singleton("field_1"))
                .build();

                exchange.getMessage().setBody(stitchRequestBody);
     })
.to("stitch:table_1?token=RAW({{token}})");
```

#### Input body type `org.apache.camel.component.stitch.client.models.StitchMessage`:

_Java-only: Java lambda Processor with Stitch SDK API_

```java
from("direct:sendStitch")
     .process(exchange -> {
         exchange.getMessage().setHeader(StitchConstants.SCHEMA, StitchSchema.builder().addKeyword("field_1", "string").build());
         exchange.getMessage().setHeader(StitchConstants.KEY_NAMES, "field_1");
         exchange.getMessage().setHeader(StitchConstants.TABLE_NAME, "table_1");

         final StitchMessage stitchMessage = StitchMessage.builder()
               .withData("field_1", "stitchMessage2-1")
               .build();

                exchange.getMessage().setBody(stitchMessage);
     })
.to("stitch:table_1?token=RAW({{token}})");
```

#### Input body type `Map`:

_Java-only: Java lambda Processor with Map construction_

```java
from("direct:sendStitch")
     .process(exchange -> {
        final Map<String, Object> properties = new LinkedHashMap<>();
        properties.put("id", Collections.singletonMap("type", "integer"));
        properties.put("name", Collections.singletonMap("type", "string"));
        properties.put("age", Collections.singletonMap("type", "integer"));
        properties.put("has_magic", Collections.singletonMap("type", "boolean"));

        final Map<String, Object> data = new LinkedHashMap<>();
        data.put(StitchRequestBody.TABLE_NAME, "my_table");
        data.put(StitchRequestBody.SCHEMA, Collections.singletonMap("properties", properties));
        data.put(StitchRequestBody.MESSAGES,
                Collections.singletonList(Collections.singletonMap("data", Collections.singletonMap("id", 2))));
        data.put(StitchRequestBody.KEY_NAMES, "test_key");

        exchange.getMessage().setBody(data);
     })
.to("stitch:table_1?token=RAW({{token}})");
```

#### Input body type `Iterable`:

_Java-only: Java lambda Processor with Iterable construction_

```java
from("direct:sendStitch")
     .process(exchange -> {
         exchange.getMessage().setHeader(StitchConstants.SCHEMA, StitchSchema.builder().addKeyword("field_1", "string").build());
         exchange.getMessage().setHeader(StitchConstants.KEY_NAMES, "field_1");
         exchange.getMessage().setHeader(StitchConstants.TABLE_NAME, "table_1");

        final StitchMessage stitchMessage1 = StitchMessage.builder()
                .withData("field_1", "stitchMessage1")
                .build();

        final StitchMessage stitchMessage2 = StitchMessage.builder()
                .withData("field_1", "stitchMessage2-1")
                .build();

        final StitchRequestBody stitchMessage2RequestBody = StitchRequestBody.builder()
                .addMessage(stitchMessage2)
                .withSchema(StitchSchema.builder().addKeyword("field_1", "integer").build())
                .withTableName("table_1")
                .withKeyNames(Collections.singleton("field_1"))
                .build();

        final Map<String, Object> stitchMessage3 = new LinkedHashMap<>();
        stitchMessage3.put(StitchMessage.DATA, Collections.singletonMap("field_1", "stitchMessage3"));

        final StitchMessage stitchMessage4 = StitchMessage.builder()
                .withData("field_1", "stitchMessage4")
                .build();

        final Exchange stitchMessage4Exchange = new DefaultExchange(context);
        stitchMessage4Exchange.getMessage().setBody(stitchMessage4);

        final StitchMessage stitchMessage5 = StitchMessage.builder()
                .withData("field_1", "stitchMessage5")
                .build();

        final Message stitchMessage5Message = new DefaultExchange(context).getMessage();
        stitchMessage5Message.setBody(stitchMessage5);

        final List<Object> inputMessages = new LinkedList<>();
        inputMessages.add(stitchMessage1);
        inputMessages.add(stitchMessage2RequestBody);
        inputMessages.add(stitchMessage3);
        inputMessages.add(stitchMessage4Exchange);
        inputMessages.add(stitchMessage5Message);

        exchange.getMessage().setBody(inputMessages);
     })
.to("stitch:table_1?token=RAW({{token}})");
```

## Development Notes (Important)

When developing on this component, you will need to obtain a Stitch token to run the integration tests. In addition to the mocked unit tests, you **will need to run the integration tests with every change you make** To run the integration tests, in this component directory, run the following maven command:

```bash
mvn verify -Dtoken=stitchToken
```

Whereby `token` is your Stitch token generated for Stitch Import API integration.

## Spring Boot Auto-Configuration

When using stitch with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-stitch-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.stitch.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.stitch.configuration** | The component configurations. The option is a org.apache.camel.component.stitch.StitchConfiguration type. |  | StitchConfiguration |
| **camel.component.stitch.connection-provider** | ConnectionProvider contain configuration for the HttpClient like Maximum connection limit .. etc, you can inject this ConnectionProvider and the StitchClient will initialize HttpClient with this ConnectionProvider. The option is a reactor.netty.resources.ConnectionProvider type. |  | ConnectionProvider |
| **camel.component.stitch.enabled** | Whether to enable auto configuration of the stitch component. This is enabled by default. |  | Boolean |
| **camel.component.stitch.http-client** | Reactor Netty HttpClient, you can injected it if you want to have custom HttpClient. The option is a reactor.netty.http.client.HttpClient type. |  | HttpClient |
| **camel.component.stitch.key-names** | A collection of comma separated strings representing the Primary Key fields in the source table. Stitch use these Primary Keys to de-dupe data during loading If not provided, the table will be loaded in an append-only manner. |  | String |
| **camel.component.stitch.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.stitch.region** | Stitch account region, e.g: europe. | europe | StitchRegion |
| **camel.component.stitch.stitch-client** | Set a custom StitchClient that implements org.apache.camel.component.stitch.client.StitchClient interface. The option is a org.apache.camel.component.stitch.client.StitchClient type. |  | StitchClient |
| **camel.component.stitch.stitch-schema** | A schema that describes the record(s). The option is a org.apache.camel.component.stitch.client.models.StitchSchema type. |  | StitchSchema |
| **camel.component.stitch.token** | Stitch access token for the Stitch Import API. |  | String |
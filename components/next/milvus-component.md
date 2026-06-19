# Milvus

**Since Camel 4.5**

**Only producer is supported**

The Milvus Component provides support for interacting with the [Milvus Vector Database](https://milvus.io/).

## URI format

milvus:collection\[?options\]

Where **collection** represents a named set of points (vectors with a payload) defined in your database.

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

The Milvus component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration;. |  | MilvusConfiguration |
| **host** (producer) | The host to connect to. | localhost | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **port** (producer) | The port to connect to. | 19530 | int |
| **timeout** (producer) | Sets a default timeout for all requests. |  | long |
| **token** (producer) | Sets the API key to use for authentication. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Milvus endpoint is configured using URI syntax:

milvus:collection

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collection** (producer) | **Required** The collection Name. |  | String |

### Query Parameters (5 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (producer) | The host to connect to. | localhost | String |
| **port** (producer) | The port to connect to. | 19530 | int |
| **timeout** (producer) | Sets a default timeout for all requests. |  | long |
| **token** (producer) | Sets the API key to use for authentication. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Milvus component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMilvusAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-milvus/latest/org/apache/camel/component/milvus/MilvusHeaders.html#ACTION) | 
The action to be performed.

Enum values:

-   CREATE\_COLLECTION
    
-   CREATE\_INDEX
    
-   UPSERT
    
-   INSERT
    
-   SEARCH
    
-   QUERY
    
-   DELETE
    





 |  | String |
| **CamelMilvusOperationStatus** (producer) Constant: [`OPERATION_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-milvus/latest/org/apache/camel/component/milvus/MilvusHeaders.html#OPERATION_STATUS) | Operation Status. |  | String |
| **CamelMilvusOperationStatusValue** (producer) Constant: [`OPERATION_STATUS_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-milvus/latest/org/apache/camel/component/milvus/MilvusHeaders.html#OPERATION_STATUS_VALUE) | Operation Status Value. |  | int |
| **CamelMilvusTextFieldName** (producer) Constant: [`TEXT_FIELD_NAME`](https://javadoc.io/doc/org.apache.camel/camel-milvus/latest/org/apache/camel/component/milvus/MilvusHeaders.html#TEXT_FIELD_NAME) | Text Field Name for Insert/Upsert operation. |  | String |
| **CamelMilvusVectorFieldName** (producer) Constant: [`VECTOR_FIELD_NAME`](https://javadoc.io/doc/org.apache.camel/camel-milvus/latest/org/apache/camel/component/milvus/MilvusHeaders.html#VECTOR_FIELD_NAME) | Vector Field Name for Insert/Upsert operation. |  | String |
| **CamelMilvusCollectionName** (producer) Constant: [`COLLECTION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-milvus/latest/org/apache/camel/component/milvus/MilvusHeaders.html#COLLECTION_NAME) | Collection Name for Insert/Upsert operation. |  | String |
| **CamelMilvusKeyName** (producer) Constant: [`KEY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-milvus/latest/org/apache/camel/component/milvus/MilvusHeaders.html#KEY_NAME) | Key Name for Insert/Upsert operation. |  | String |
| **CamelMilvusKeyValue** (producer) Constant: [`KEY_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-milvus/latest/org/apache/camel/component/milvus/MilvusHeaders.html#KEY_VALUE) | Key Value for Insert/Upsert operation. |  | String |

## Examples

### Collection Examples

In the route below, we use the milvus component to create a collection named _test_ with the given parameters:

-   Java
    

```java
FieldType fieldType1 = FieldType.newBuilder()
                .withName("userID")
                .withDescription("user identification")
                .withDataType(DataType.Int64)
                .withPrimaryKey(true)
                .withAutoID(true)
                .build();

FieldType fieldType2 = FieldType.newBuilder()
                .withName("userFace")
                .withDescription("face embedding")
                .withDataType(DataType.FloatVector)
                .withDimension(64)
                .build();

FieldType fieldType3 = FieldType.newBuilder()
                .withName("userAge")
                .withDescription("user age")
                .withDataType(DataType.Int8)
                .build();

from("direct:in")
    .setHeader(Milvus.Headers.ACTION)
        .constant(MilvusAction.CREATE_COLLECTION)
    .setBody()
        .constant(
                CreateCollectionParam.newBuilder()
                    .withCollectionName("test")
                    .withDescription("customer info")
                    .withShardsNum(2)
                    .withEnableDynamicField(false)
                    .addFieldType(fieldType1)
                    .addFieldType(fieldType2)
                    .addFieldType(fieldType3)
                    .build())
    .to("milvus:test");
```

### Points Examples

#### Insert

In the route below we use the milvus component to perform insert on points in the collection named _test_:

-   Java
    

```java
private List<List<Float>> generateFloatVectors(int count) {
        Random ran = new Random();
        List<List<Float>> vectors = new ArrayList<>();
        for (int n = 0; n < count; ++n) {
            List<Float> vector = new ArrayList<>();
            for (int i = 0; i < 64; ++i) {
                vector.add(ran.nextFloat());
            }
            vectors.add(vector);
        }

        return vectors;
}


Random ran = new Random();
List<Integer> ages = new ArrayList<>();
for (long i = 0L; i < 2; ++i) {
    ages.add(ran.nextInt(99));
}
List<InsertParam.Field> fields = new ArrayList<>();
fields.add(new InsertParam.Field("userAge", ages));
fields.add(new InsertParam.Field("userFace", generateFloatVectors(2)));

from("direct:in")
    .setHeader(Milvus.Headers.ACTION)
        .constant(MilvusAction.INSERT)
    .setBody()
        .constant(
            InsertParam.newBuilder()
                .withCollectionName("test")
                .withFields(fields)
                .build())
    .to("milvus:test");
```

### Search

In the route below, we use the milvus component to retrieve information by query from the collection named _test_:

-   Java
    

```java
private List<Float> generateFloatVector() {
        Random ran = new Random();
        List<Float> vector = new ArrayList<>();
        for (int i = 0; i < 64; ++i) {
            vector.add(ran.nextFloat());
        }
        return vector;
}

from("direct:in")
    .setHeader(Milvus.Headers.ACTION)
        .constant(MilvusAction.SEARCH)
    .setBody()
        .constant(SearchSimpleParam.newBuilder()
                .withCollectionName("test")
                .withVectors(generateFloatVector())
                .withFilter("userAge>0")
                .withLimit(100L)
                .withOffset(0L)
                .withOutputFields(Lists.newArrayList("userAge"))
                .withConsistencyLevel(ConsistencyLevelEnum.STRONG)
                .build())
    .to("milvus:myCollection");
```

### Relation with Langchain4j-Embeddings component

The Milvus component provides a datatype transformer, from langchain4j-embeddings to an insert/upsert object compatible with Milvus.

As an example, you could think about these routes:

Java

```java
    protected RoutesBuilder createRouteBuilder() {
        return new RouteBuilder() {
            public void configure() {
                from("direct:in")
                        .to("langchain4j-embeddings:test")
                        .setHeader(Milvus.Headers.ACTION).constant(MilvusAction.INSERT)
                        .setHeader(Milvus.Headers.KEY_NAME).constant("userID")
                        .setHeader(Milvus.Headers.KEY_VALUE).constant(Long.valueOf("3"))
                        .transform(new org.apache.camel.spi.DataType("milvus:embeddings"))
                        .to(MILVUS_URI);

                from("direct:up")
                        .to("langchain4j-embeddings:test")
                        .setHeader(Milvus.Headers.ACTION).constant(MilvusAction.UPSERT)
                        .setHeader(Milvus.Headers.KEY_NAME).constant("userID")
                        .setHeader(Milvus.Headers.KEY_VALUE).constant(Long.valueOf("3"))
                        .transform(new org.apache.camel.spi.DataType("milvus:embeddings"))
                        .to(MILVUS_URI);
            }
        };
    }
```

It’s important to note that Milvus SDK doesn’t support upsert for autoID fields. This means if you set a field as key, and you set the autoID to true, the upsert won’t be possible.

That’s the reason why, in the example, we are setting the userID as keyName with a keyValue of 3. This is particularly important when you design your Milvus database.

The transformer only supports insert/upsert objects, so the only operation you can set via header are INSERT and UPSERT, otherwise the transformer will fail with an error log.
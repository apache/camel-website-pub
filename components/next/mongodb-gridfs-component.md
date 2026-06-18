# MongoDB GridFS

**Since Camel 2.18**

**Both producer and consumer are supported**

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-mongodb-gridfs</artifactId>
    <version>x.y.z</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

mongodb-gridfs:connectionBean?database=databaseName&bucket=bucketName\[&moreOptions...\]

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

The MongoDB GridFS component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The MongoDB GridFS endpoint is configured using URI syntax:

mongodb-gridfs:connectionBean

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionBean** (common) | **Required** Name of com.mongodb.client.MongoClient to use. |  | String |

### Query Parameters (16 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bucket** (common) | Sets the name of the GridFS bucket within the database. Default is fs. | fs | String |
| **database** (common) | **Required** Sets the name of the MongoDB database to target. |  | String |
| **readPreference** (common) | Sets a MongoDB ReadPreference on the Mongo connection. Read preferences set directly on the connection will be overridden by this setting. The com.mongodb.ReadPreference#valueOf(String) utility method is used to resolve the passed readPreference value. Some examples for the possible values are nearest, primary or secondary etc. |  | ReadPreference |
| **writeConcern** (common) | 
Set the WriteConcern for write operations on MongoDB using the standard ones. Resolved from the fields of the WriteConcern class by calling the WriteConcern#valueOf(String) method.

Enum values:

-   ACKNOWLEDGED
    
-   W1
    
-   W2
    
-   W3
    
-   UNACKNOWLEDGED
    
-   JOURNALED
    
-   MAJORITY
    





 |  | WriteConcern |
| **delay** (consumer) | Sets the delay between polls within the Consumer. Default is 500ms. | 500 | long |
| **fileAttributeName** (consumer) | If the QueryType uses a FileAttribute, this sets the name of the attribute that is used. Default is camel-processed. | camel-processed | String |
| **initialDelay** (consumer) | Sets the initialDelay before the consumer will start polling. Default is 1000ms. | 1000 | long |
| **persistentTSCollection** (consumer) | If the QueryType uses a persistent timestamp, this sets the name of the collection within the DB to store the timestamp. | camel-timestamps | String |
| **persistentTSObject** (consumer) | If the QueryType uses a persistent timestamp, this is the ID of the object in the collection to store the timestamp. | camel-timestamp | String |
| **query** (consumer) | Additional query parameters (in JSON) that are used to configure the query used for finding files in the GridFsConsumer. |  | String |
| **queryStrategy** (consumer) | 

Sets the QueryStrategy that is used for polling for new files. Default is Timestamp.

Enum values:

-   TimeStamp
    
-   PersistentTimestamp
    
-   FileAttribute
    
-   TimeStampAndFileAttribute
    
-   PersistentTimestampAndFileAttribute
    





 | TimeStamp | QueryStrategy |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **operation** (producer) | Sets the operation this endpoint will execute against GridFs. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The MongoDB GridFS component supports 11 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelFileContentType** (consumer) Constant: [`FILE_CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#FILE_CONTENT_TYPE) | The content type of the file. |  | String |
| **CamelFileLength** (consumer) Constant: [`FILE_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#FILE_LENGTH) | The size of the file. |  | long |
| **CamelFileLastModified** (consumer) Constant: [`FILE_LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#FILE_LAST_MODIFIED) | The size of the file. |  | Date |
| **CamelFileName** (producer) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#FILE_NAME) | The name of the file. |  | String |
| **Content-Type** (producer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#CONTENT_TYPE) | The content type of the file. |  | String |
| **CamelFileNameProduced** (producer) Constant: [`FILE_NAME_PRODUCED`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#FILE_NAME_PRODUCED) | The file name produced. |  | String |
| **CamelGridFsMetadata** (common) Constant: [`GRIDFS_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#GRIDFS_METADATA) | Any additional metadata stored along with the file in JSON format. |  | String |
| **CamelGridFsOperation** (producer) Constant: [`GRIDFS_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#GRIDFS_OPERATION) | The operation to perform. |  | String |
| **CamelGridFsChunkSize** (producer) Constant: [`GRIDFS_CHUNKSIZE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#GRIDFS_CHUNKSIZE) | The number of bytes per chunk for the uploaded file. |  | Integer |
| **CamelGridFsFileId** (producer) Constant: [`GRIDFS_FILE_ID_PRODUCED`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#GRIDFS_FILE_ID_PRODUCED) | The ObjectId of the file produced. |  | ObjectId |
| **CamelGridFsObjectId** (producer) Constant: [`GRIDFS_OBJECT_ID`](https://javadoc.io/doc/org.apache.camel/camel-mongodb-gridfs/latest/org/apache/camel/component/mongodb/gridfs/GridFsConstants.html#GRIDFS_OBJECT_ID) | The ObjectId of the file. |  | ObjectId |

## Usage

### GridFS operations - producer endpoint

#### count

Returns the total number of files in the collection, returning an Integer as the OUT message body.

_Java-only: using ProducerTemplate to invoke the count operation_

```java
// from("direct:count").to("mongodb-gridfs?database=tickets&operation=count");
Integer result = template.requestBodyAndHeader("direct:count", "irrelevantBody");
assertTrue("Result is not of type Long", result instanceof Integer);
```

You can provide a filename header to provide a count of files matching that filename.

_Java-only: using ProducerTemplate with filename header_

```java
Map<String, Object> headers = new HashMap<String, Object>();
headers.put(Exchange.FILE_NAME, "filename.txt");
Integer count = template.requestBodyAndHeaders("direct:count", query, headers);
```

#### listAll

Returns a Reader that lists all the filenames and their IDs in a tab separated stream.

// from("direct:listAll").to("mongodb-gridfs?database=tickets&operation=listAll");
Reader result = template.requestBodyAndHeader("direct:listAll", "irrelevantBody");

filename1.txt   1252314321
filename2.txt   2897651254

#### findOne

Finds a file in the GridFS system and sets the body to an InputStream of the content. Also provides the metadata has headers. It uses `Exchange.FILE_NAME` from the incoming headers to determine the file to find.

_Java-only: using ProducerTemplate to find a file by name_

```java
// from("direct:findOne").to("mongodb-gridfs?database=tickets&operation=findOne");
Map<String, Object> headers = new HashMap<String, Object>();
headers.put(Exchange.FILE_NAME, "filename.txt");
InputStream result = template.requestBodyAndHeaders("direct:findOne", "irrelevantBody", headers);
```

#### create

Create a new file in the GridFs database. It uses the `Exchange.FILE_NAME` from the incoming headers for the name and the body contents (as an InputStream) as the content.

_Java-only: using ProducerTemplate to create a file_

```java
// from("direct:create").to("mongodb-gridfs?database=tickets&operation=create");
Map<String, Object> headers = new HashMap<String, Object>();
headers.put(Exchange.FILE_NAME, "filename.txt");
InputStream stream = ... the data for the file ...
template.requestBodyAndHeaders("direct:create", stream, headers);
```

#### remove

Removes a file from the GridFS database.

_Java-only: using ProducerTemplate to remove a file_

```java
// from("direct:remove").to("mongodb-gridfs?database=tickets&operation=remove");
Map<String, Object> headers = new HashMap<String, Object>();
headers.put(Exchange.FILE_NAME, "filename.txt");
template.requestBodyAndHeaders("direct:remove", "", headers);
```

## Examples

### Example route

The following route defined in Spring XML executes the operation [**findOne**](#) on a collection.

**Get a file from GridFS**

```xml
<route>
  <from uri="direct:start" />
  <!-- using bean 'mongoBean' defined above -->
  <to uri="mongodb-gridfs:mongoBean?database=${mongodb.database}&amp;operation=findOne" />
  <to uri="direct:result" />
</route>
```

### Configuration of a database in Spring XML

The following Spring XML creates a bean defining the connection to a MongoDB instance.

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="mongoBean" class="com.mongodb.Mongo">
        <constructor-arg name="host" value="${mongodb.host}" />
        <constructor-arg name="port" value="${mongodb.port}" />
    </bean>
</beans>
```

## Spring Boot Auto-Configuration

When using mongodb-gridfs with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-mongodb-gridfs-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.mongodb-gridfs.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.mongodb-gridfs.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.mongodb-gridfs.enabled** | Whether to enable auto configuration of the mongodb-gridfs component. This is enabled by default. |  | Boolean |
| **camel.component.mongodb-gridfs.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
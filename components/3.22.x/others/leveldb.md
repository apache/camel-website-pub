# LevelDB

**Since Camel 2.10**

[Leveldb](https://github.com/google/leveldb) is a very lightweight and embedable key value database. It allows together with Camel to provide persistent support for various Camel features such as Aggregator.

Current features it provides:

-   LevelDBAggregationRepository
    

## Using LevelDBAggregationRepository

`LevelDBAggregationRepository` is an `AggregationRepository` which on the fly persists the aggregated messages. This ensures that you will not lose messages, as the default aggregator will use an in memory only `AggregationRepository`.

It has the following options:

  
| Option | Type | Description |
| --- | --- | --- |
| `repositoryName` | String | A mandatory repository name. Allows you to use a shared `LevelDBFile` for multiple repositories. |
| `persistentFileName` | String | Filename for the persistent storage. If no file exists on startup a new file is created. |
| `levelDBFile` | LevelDBFile | Use an existing configured `org.apache.camel.component.leveldb.LevelDBFile` instance. |
| `sync` | boolean | Whether or not the LevelDBFile should sync on write or not. Default is false. By sync on write ensures that its always waiting for all writes to be spooled to disk and thus will not loose updates. See [LevelDB docs](http://leveldb.googlecode.com/svn/trunk/doc/index.md) for more details about async vs sync writes. |
| `returnOldExchange` | boolean | Whether the get operation should return the old existing Exchange if any existed. By default this option is `false` to optimize as we do not need the old exchange when aggregating. |
| `useRecovery` | boolean | Whether or not recovery is enabled. This option is by default `true`. When enabled the Camel Aggregator automatic recover failed aggregated exchange and have them resubmitted. |
| `recoveryInterval` | long | If recovery is enabled then a background task is run every x’th time to scan for failed exchanges to recover and resubmit. By default this interval is 5000 millis. |
| `maximumRedeliveries` | int | Allows you to limit the maximum number of redelivery attempts for a recovered exchange. If enabled then the Exchange will be moved to the dead letter channel if all redelivery attempts failed. By default this option is disabled. If this option is used then the `deadLetterUri` option must also be provided. |
| `deadLetterUri` | String | An endpoint uri for a Dead Letter Channel where exhausted recovered Exchanges will be moved. If this option is used then the `maximumRedeliveries` option must also be provided. |

The `repositoryName` option must be provided. Then either the `persistentFileName` or the `levelDBFile` must be provided.

### What is preserved when persisting

`LevelDBAggregationRepository` will only preserve any `Serializable` compatible message body data types. Message headers must be primitive / string / numbers / etc. If a data type is not such a type its dropped and a `WARN` is logged. And it only persists the `Message` body and the `Message` headers. The `Exchange` properties are **not** persisted.

### Recovery

The `LevelDBAggregationRepository` will by default recover any failed Exchange. It does this by having a background tasks that scans for failed Exchanges in the persistent store. You can use the `checkInterval` option to set how often this task runs. The recovery works as transactional which ensures that Camel will try to recover and redeliver the failed Exchange. Any Exchange which was found to be recovered will be restored from the persistent store and resubmitted and send out again.

The following headers is set when an Exchange is being recovered/redelivered:

  
| Header | Type | Description |
| --- | --- | --- |
| `Exchange.REDELIVERED` | Boolean | Is set to true to indicate the Exchange is being redelivered. |
| `Exchange.REDELIVERY_COUNTER` | Integer | The redelivery attempt, starting from 1. |

Only when an Exchange has been successfully processed it will be marked as complete which happens when the `confirm` method is invoked on the `AggregationRepository`. This means if the same Exchange fails again it will be kept retried until it success.

You can use option `maximumRedeliveries` to limit the maximum number of redelivery attempts for a given recovered Exchange. You must also set the `deadLetterUri` option so Camel knows where to send the Exchange when the `maximumRedeliveries` was hit.

You can see some examples in the unit tests of camel-leveldb, for example [this test](https://svn.apache.org/repos/asf/camel/trunk/components/camel-leveldb/src/test/java/org/apache/camel/component/leveldb/LevelDBAggregateRecoverTest.java).

### Serialization mechanism

Component serializes by using Java serialization mechanism by default.

You can use serialization via Jackson (using json). Jackson serialization brings better performance, but also several limitations.

Example of jackson serialization:

```java
LevelDBAggregationRepository repo = ...; //initialization of repository
repo.setSerializer(new JacksonLevelDBSerializer());
```

Limitation of jackson serializer is caused by binary data:

-   If payload is a raw data (byte\[\]), it is saved into DB without using Jackson
    
-   If payload contains objects with binary fields. Those fields won’t be serialized/deserialized correctly. Customized serializer can be used to solve this problem. Please use custom serializer with Jackson by providing own Module:
    

```java
SimpleModule simpleModule = new SimpleModule();
simpleModule.addSerializer(ObjectWithBinaryField.class, new ObjectWithBinaryFieldSerializer()); //custom serializer
simpleModule.addDeserializer(ObjectWithBinaryField.class, new ObjectWithBinaryFieldDeserializer()); //custom deserializer

repo.setSerializer(new JacksonLevelDBSerializer(simpleModule));
```

## Using LevelDBAggregationRepository in Java DSL

In this example we want to persist aggregated messages in the `target/data/leveldb.dat` file.

## Using LevelDBAggregationRepository in Spring XML

The same example but using Spring XML instead:

## Dependencies

To use LevelDB in your camel routes you need to add the a dependency on **camel-leveldb**.

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-leveldb</artifactId>
  <version>x.y.z</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using leveldb with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-leveldb-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component has no Spring Boot auto configuration options.
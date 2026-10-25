# Idempotent Consumer

The [Idempotent Consumer](http://www.enterpriseintegrationpatterns.com/IdempotentReceiver.md) from the [EIP patterns](enterprise-integration-patterns.md) is used to filter out duplicate messages.

The Idempotent Consumer essentially acts like a [Message Filter](filter-eip.md) to filter out duplicates.

Camel will add the message id eagerly to the repository to detect duplication also for [Exchange](../../../manual/exchange.md)'s' currently in progress. On completion Camel will remove the message id from the repository if the [Exchange](../../../manual/exchange.md) failed, otherwise it stays there.

## Options

The Idempotent Consumer eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **expression** | **Required** The expression to compute the unique message ID used for duplicate detection. Messages with the same ID are treated as duplicates and skipped. |  | ExpressionDefinition |
| **idempotentRepository** | **Required** Sets the reference name of the message id repository to use for storing processed message ids to detect duplicates. |  | IdempotentRepository |
| **eager** | Sets whether to eagerly add the key to the idempotent repository or wait until the exchange is complete. Eager is default enabled. | true | Boolean |
| **completionEager** | Sets whether to complete the idempotent consumer eager or when the exchange is done. | false | Boolean |
| **skipDuplicate** | Sets whether to skip duplicates or not. The default behavior is to skip duplicates. | true | Boolean |
| **removeOnFailure** | Sets whether to remove or keep the key on failure. The default behavior is to remove the key on failure. | true | Boolean |
| **outputs** | **Required** |  | List |

## Message Body

The message body at each side of the Idempotent Consumer EIP: _EIP input_ is the body it needs, _EIP output_ the body after it, and _Steps_ the body its own steps start with.

  
| Side | Body | Description |
| --- | --- | --- |
| **EIP output** | what its steps end with | What its steps end with; the body as it was for a duplicate message. |
| **Steps** | `unchanged` | 
 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Exchange properties

The Idempotent Consumer eip supports the following exchange properties which are listed below.

The exchange properties are set on the `Exchange` by the EIP, unless otherwise specified in the description. This means those properties are available after this EIP has completed processing the `Exchange`.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDuplicateMessage** | Whether this exchange is a duplicate detected by the Idempotent Consumer EIP. |  | boolean |

## Idempotent Consumer implementations

The idempotent consumer provides a pluggable repository which you can implement your own `org.apache.camel.spi.IdempotentRepository`.

Camel provides the following Idempotent Consumer implementations:

-   FileIdempotentRepository from `camel-support` JAR
    
-   MemoryIdempotentRepository from `camel-support` JAR
    
-   [CaffeineIdempotentRepository](../caffeine-cache-component.md)
    
-   [CassandraIdempotentRepository](../cql-component.md) [NamedCassandraIdempotentRepository](../cql-component.md)
    
-   [EHCacheIdempotentRepository](../ehcache-component.md)
    
-   [HazelcastIdempotentRepository](../hazelcast-summary.md)
    
-   [InfinispanIdempotentRepository](../infinispan-component.md) [InfinispanEmbeddedIdempotentRepository](../infinispan-component.md) [InfinispanRemoteIdempotentRepository](../infinispan-component.md)
    
-   [JCacheIdempotentRepository](../jcache-component.md)
    
-   [JpaMessageIdRepository](../jpa-component.md)
    
-   [KafkaIdempotentRepository](../kafka-component.md)
    
-   [MongoDbIdempotentRepository](../mongodb-component.md)
    
-   [RedisIdempotentRepository](../spring-redis-component.md) [RedisStringIdempotentRepository](../spring-redis-component.md)
    
-   [SpringCacheIdempotentRepository](../../../manual/spring.md)
    
-   [JdbcMessageIdRepository](../sql-component.md) [JdbcOrphanLockAwareIdempotentRepository](../sql-component.md)
    

## Example

The idempotent consumer needs an expression that gives the id of each message, and a repository that remembers the ids it has seen. In the example below the id is the `messageId` header, and the repository is a `MemoryIdempotentRepository`, which keeps the last 1000 ids in memory. A message with an id that is already in the repository is skipped, so it does not reach `mock:result`.

In XML and YAML the repository is a bean, and the idempotent consumer refers to it by name.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .idempotentConsumer(header("messageId"), MemoryIdempotentRepository.memoryIdempotentRepository())
        .to("mock:result");
```

```xml
<bean name="myRepo" type="org.apache.camel.support.processor.idempotent.MemoryIdempotentRepository"/>

<route>
    <from uri="direct:start"/>
    <idempotentConsumer idempotentRepository="myRepo">
        <header>messageId</header>
        <to uri="mock:result"/>
    </idempotentConsumer>
</route>
```

```yaml
- beans:
    - name: myRepo
      type: org.apache.camel.support.processor.idempotent.MemoryIdempotentRepository
- route:
    from:
      uri: direct:start
      steps:
        - idempotentConsumer:
            expression:
              header:
                expression: messageId
            idempotentRepository: myRepo
            steps:
              - to:
                  uri: mock:result
```

The memory repository forgets the ids when the application stops. To keep them, use `FileIdempotentRepository` or one of the repositories listed above.

### Handling the duplicates in the route

By default, a duplicate is skipped. When `skipDuplicate` is `false`, a duplicate goes through the idempotent consumer too, and the exchange property `CamelDuplicateMessage` is `true`. The route can then decide what to do with it, for example log it:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .idempotentConsumer(header("messageId"), MemoryIdempotentRepository.memoryIdempotentRepository())
        .skipDuplicate(false)
        .choice()
            .when(simple("${exchangeProperty.CamelDuplicateMessage} == true"))
                .log("Message ${header.messageId} is a duplicate")
            .otherwise()
                .to("mock:result")
        .end()
    .end();
```

```xml
<bean name="myRepo" type="org.apache.camel.support.processor.idempotent.MemoryIdempotentRepository"/>

<route>
    <from uri="direct:start"/>
    <idempotentConsumer idempotentRepository="myRepo" skipDuplicate="false">
        <header>messageId</header>
        <choice>
            <when>
                <simple>${exchangeProperty.CamelDuplicateMessage} == true</simple>
                <log message="Message ${header.messageId} is a duplicate"/>
            </when>
            <otherwise>
                <to uri="mock:result"/>
            </otherwise>
        </choice>
    </idempotentConsumer>
</route>
```

```yaml
- beans:
    - name: myRepo
      type: org.apache.camel.support.processor.idempotent.MemoryIdempotentRepository
- route:
    from:
      uri: direct:start
      steps:
        - idempotentConsumer:
            expression:
              header:
                expression: messageId
            idempotentRepository: myRepo
            skipDuplicate: false
            steps:
              - choice:
                  when:
                    - expression:
                        simple:
                          expression: "${exchangeProperty.CamelDuplicateMessage} == true"
                      steps:
                        - log:
                            message: "Message ${header.messageId} is a duplicate"
                  otherwise:
                    steps:
                      - to:
                          uri: mock:result
```
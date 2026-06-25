# Idempotent Consumer

The [Idempotent Consumer](http://www.enterpriseintegrationpatterns.com/IdempotentReceiver.md) from the [EIP patterns](enterprise-integration-patterns.md) is used to filter out duplicate messages.

The Idempotent Consumer essentially acts like a [Message Filter](filter-eip.md) to filter out duplicates.

Camel will add the message id eagerly to the repository to detect duplication also for [Exchange](../../../manual/exchange.md)'s' currently in progress. On completion Camel will remove the message id from the repository if the [Exchange](../../../manual/exchange.md) failed, otherwise it stays there.

## Options

The Idempotent Consumer eip supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **expression** | **Required** The expression to compute the unique message ID used for duplicate detection. Messages with the same ID are treated as duplicates and skipped. |  | ExpressionDefinition |
| **idempotentRepository** | Sets the reference name of the message id repository to use for storing processed message ids to detect duplicates. |  | IdempotentRepository |
| **eager** | Sets whether to eagerly add the key to the idempotent repository or wait until the exchange is complete. Eager is default enabled. | true | Boolean |
| **completionEager** | Sets whether to complete the idempotent consumer eager or when the exchange is done. | false | Boolean |
| **skipDuplicate** | Sets whether to skip duplicates or not. The default behavior is to skip duplicates. | true | Boolean |
| **removeOnFailure** | Sets whether to remove or keep the key on failure. The default behavior is to remove the key on failure. | true | Boolean |
| **outputs** | **Required** |  | List |

## Exchange properties

The Idempotent Consumer eip supports 1 exchange properties, which are listed below.

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

For example, see the above implementations for more details.
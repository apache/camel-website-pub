# Idempotent Consumer

The [Idempotent Consumer](http://www.enterpriseintegrationpatterns.com/IdempotentReceiver.md) from the [EIP patterns](enterprise-integration-patterns.md) is used to filter out duplicate messages.

The Idempotent Consumer essentially acts like a [Message Filter](filter-eip.md) to filter out duplicates.

Camel will add the message id eagerly to the repository to detect duplication also for [Exchange](../../../manual/exchange.md)'s' currently in progress. On completion Camel will remove the message id from the repository if the [Exchange](../../../manual/exchange.md) failed, otherwise it stays there.

## Options

The Idempotent Consumer eip supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **expression** | **Required** Expression used to calculate the correlation key to use for duplicate check. The Exchange which has the same correlation key is regarded as a duplicate and will be rejected. |  | ExpressionDefinition |
| **idempotentRepository** | Sets the reference name of the message id repository. |  | IdempotentRepository |
| **eager** | Sets whether to eagerly add the key to the idempotent repository or wait until the exchange is complete. Eager is default enabled. | true | Boolean |
| **completionEager** | Sets whether to complete the idempotent consumer eager or when the exchange is done. If this option is true to complete eager, then the idempotent consumer will trigger its completion when the exchange reached the end of the block of the idempotent consumer pattern. So if the exchange is continued routed after the block ends, then whatever happens there does not affect the state. If this option is false (default) to not complete eager, then the idempotent consumer will complete when the exchange is done being routed. So if the exchange is continued routed after the block ends, then whatever happens there also affect the state. For example if the exchange failed due to an exception, then the state of the idempotent consumer will be a rollback. | false | Boolean |
| **skipDuplicate** | Sets whether to skip duplicates or not. The default behavior is to skip duplicates. A duplicate message would have the Exchange property org.apache.camel.Exchange#DUPLICATE\_MESSAGE set to a Boolean#TRUE value. A none duplicate message will not have this property set. | true | Boolean |
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
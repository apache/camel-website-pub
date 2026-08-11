# Rollback

The Rollback EIP is used for marking an [Exchange](../../../manual/exchange.md) to rollback and stop continue routing the message.

## Options

The Rollback eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **message** | The message to set on the exception when rolling back. |  | String |
| **markRollbackOnly** | If enabled then only the current transaction is marked for rollback. No exception is thrown and the route continues to execute. | false | Boolean |
| **markRollbackOnlyLast** | If enabled then only the last sub-transaction (from the last transacted EIP) is marked for rollback. This allows partial rollbacks in nested transaction scenarios. | false | Boolean |

## Exchange properties

The Rollback eip has no exchange properties.

## Using Rollback

We want to test a message for some conditions and force a rollback if a message may be faulty.

In Java DSL we can do:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .choice().when(body().contains("error"))
        .rollback("That do not work")
    .otherwise()
        .to("direct:continue");
```

```xml
<route>
    <from uri="direct:start"/>
    <choice>
        <when>
            <simple>${body} contains 'error'</simple>
            <rollback message="That do not work"/>
        </when>
        <otherwise>
            <to uri="direct:continue"/>
        </otherwise>
    </choice>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - choice:
            when:
              - expression:
                  simple:
                    expression: "${body} contains 'error'"
                steps:
                  - rollback:
                      message: That do not work
            otherwise:
              steps:
                - to:
                    uri: direct:continue
```

When Camel is rolling back, then a `RollbackExchangeException` is thrown with the cause message `_"That do not work"_`.

### Marking for Rollback only

When a message is rolled back, then Camel will by default throw a `RollbackExchangeException` to cause the message to fail and rollback.

This behavior can be modified to only mark for rollback, and not throw the exception.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .choice().when(body().contains("error"))
        .markRollbackOnly()
    .otherwise()
        .to("direct:continue");
```

```xml
<route>
    <from uri="direct:start"/>
    <choice>
        <when>
            <simple>${body} contains 'error'</simple>
            <rollback markRollbackOnly="true"/>
        </when>
        <otherwise>
            <to uri="direct:continue"/>
        </otherwise>
    </choice>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - choice:
            when:
              - expression:
                  simple:
                    expression: "${body} contains 'error'"
                steps:
                  - rollback:
                      markRollbackOnly: "true"
            otherwise:
              steps:
                - to:
                    uri: direct:continue
```

Then no exception is thrown, but the message is marked to rollback and stopped routing.

### Using Rollback with Transactions

Rollback can be used together with [transactions](transactional-client.md). For more details, see [Transaction Client](transactional-client.md) EIP.
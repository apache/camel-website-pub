# JMS

JVM since1.0.0 Native since1.0.0

Send and receive messages to/from JMS message brokers.

## What’s inside

-   [JMS component](../../../../components/4.22.x/jms-component.md), URI syntax: `jms:destinationType:destinationName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jms)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jms</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Message mapping with `org.w3c.dom.Node`

The Camel JMS component supports message mapping between `jakarta.jms.Message` and `org.apache.camel.Message`. When wanting to convert a Camel message body type of `org.w3c.dom.Node`, you must ensure that the `camel-quarkus-xml-jaxp` extension is present on the classpath.

### Native mode support for jakarta.jms.ObjectMessage

When sending JMS message payloads as `jakarta.jms.ObjectMessage`, you must annotate the relevant classes to be registered for serialization with `@RegisterForReflection(serialization = true)`. Note that this extension automatically sets `quarkus.camel.native.reflection.serialization-enabled = true` for you. Refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

### Support for Connection pooling and X/Open XA distributed transactions

You can use the `quarkus-pooled-jms` extension to get pooling and XA support for JMS connections. Refer to the [quarkus-pooled-jms](https://quarkiverse.github.io/quarkiverse-docs/quarkus-pooled-jms/dev/index.md) extension documentation for more information. Currently, it can work with `quarkus-artemis-jms`, `quarkus-qpid-jms` and `ibmmq-client`. Just add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>io.quarkiverse.messaginghub</groupId>
    <artifactId>quarkus-pooled-jms</artifactId>
</dependency>
```

Pooling is enabled by default.

> **Note**
> `clientID` and `durableSubscriptionName` are not supported in pooled connections. If `setClientID` is called on a reused connection from the pool, an `IllegalStateException` will be thrown. You will get error messages like `Cause: setClientID can only be called directly after the connection is created`.

To enable XA, you need to add `quarkus-narayana-jta` extension:

```xml
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-narayana-jta</artifactId>
</dependency>
```

Also add the following configuration to your `application.properties`:

```properties
quarkus.pooled-jms.transaction=xa
quarkus.transaction-manager.enable-recovery=true
```

XA support is only available with `quarkus-artemis-jms` and `ibmmq-client`. We highly recommend to enable transaction recovery.

Since there is no quarkus extension for `ibmmq-client`, you need to create a custom `ConnectionFactory` and wrap it by yourself. Here is an example:

```java
@Produces
public ConnectionFactory createXAConnectionFactory(PooledJmsWrapper wrapper) {
    MQXAConnectionFactory mq = new MQXAConnectionFactory();
    try {
        mq.setHostName(ConfigProvider.getConfig().getValue("ibm.mq.host", String.class));
        mq.setPort(ConfigProvider.getConfig().getValue("ibm.mq.port", Integer.class));
        mq.setChannel(ConfigProvider.getConfig().getValue("ibm.mq.channel", String.class));
        mq.setQueueManager(ConfigProvider.getConfig().getValue("ibm.mq.queueManagerName", String.class));
        mq.setTransportType(WMQConstants.WMQ_CM_CLIENT);
        mq.setStringProperty(WMQConstants.USERID,
            ConfigProvider.getConfig().getValue("ibm.mq.user", String.class));
        mq.setStringProperty(WMQConstants.PASSWORD,
            ConfigProvider.getConfig().getValue("ibm.mq.password", String.class));
    } catch (Exception e) {
        throw new RuntimeException("Unable to create new IBM MQ connection factory", e);
    }
    return wrapper.wrapConnectionFactory(mq);
}
```

> **Note**
> If you use `ibmmq-client` to consume messages and enable XA, you need to configure a `TransactionManager` in the camel route like this:
>
> ```java
> @Inject
> TransactionManager transactionManager;
>
> @Override
> public void configure() throws Exception {
>     from("jms:queue:DEV.QUEUE.XA?transactionManager=#jtaTransactionManager");
> }
>
> @Named("jtaTransactionManager")
> public PlatformTransactionManager getTransactionManager() {
>     return new JtaTransactionManager(transactionManager);
> }
> ```
>
> Otherwise, you will get an exception like `MQRC_SYNCPOINT_NOT_AVAILABLE`.

## transferException option in native mode

To use the `transferException` option in native mode, you must enable support for object serialization. Refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

You will also need to enable serialization for the exception classes that you intend to serialize. For example.

```java
@RegisterForReflection(targets = { IllegalStateException.class, MyCustomException.class }, serialization = true)
```
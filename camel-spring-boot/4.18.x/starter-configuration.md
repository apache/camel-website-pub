# Starter Configuration

Clear and accessible configuration is a crucial part of any application. Camel [starters](list.md) (Components, Data Formats, Languages) fully support Spring Boot’s [external configuration](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config) mechanism. We’ve also added the possibility to configure them through Spring [Beans](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-definition) for more complex uses cases.

## Using External Configuration

Internally, every [starter](list.md) is configured through Spring Boot’s [ConfigurationProperties](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config.typesafe-configuration-properties.java-bean-binding). Each configuration parameter can be set in various [ways](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config) (`application.[properties|json|yaml]` files, command line arguments, environments variables etc…​). Parameters have the form of `camel.[component|language|dataformat].[name].[parameter]`

For example to configure the URL of the MQTT5 broker you can set:

```none
camel.component.paho-mqtt5.broker-url=tcp://localhost:61616
```

Or to configure the `delimeter` of the CSV dataformat to be a semicolon(;) you can set:

```none
camel.dataformat.csv.delimiter=;
```

Camel will use it’s [TypeConverter](spring-boot.html#typeconverter) mechanism when setting properties to the desired type.

You can refer to beans in the Registry using the `#bean:name`:

```none
camel.component.jms.transactionManager=#bean:myjtaTransactionManager
```

The `Bean` would be typically created in Java:

```java
@Bean("myjtaTransactionManager")
public JmsTransactionManager myjtaTransactionManager(PooledConnectionFactory pool) {
    JmsTransactionManager manager = new JmsTransactionManager(pool);
    manager.setDefaultTimeout(45);
    return manager;
}
```

Beans can also be created in [configuration files](../../components/4.22.x/others/main.html#_specifying_custom_beans) but it isn’t recommended for complex use cases.

## Using Beans

Starters can also be created and configured via Spring [Beans](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-definition). Before creating a starter (Component, Dataformat, Language), Camel will first lookup it up in the Registry by it’s name if it already exists. For example to configure a Kafka component:

```java
@Bean("kafka")
public KafkaComponent kafka(KafkaConfiguration kafkaconfiguration){
    return ComponentsBuilderFactory.kafka()
                        .brokers("{{kafka.host}}:{{kafka.port}}")
                        .build();
}
```

The `Bean` name has to be equal to that of the Component, Dataformat or Language your are configuring. If the `Bean` name isn’t specified in the annotation it will be set to the method name.

Typical Camel Spring Boot projects will use a combination of external configuration and Beans to configure their application. For more complete examples on how to configure your Camel Spring Boot project, you can refer to our example [repository](https://github.com/apache/camel-spring-boot-examples).

All contributions are welcome!
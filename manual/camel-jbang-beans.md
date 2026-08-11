# Camel CLI - Java Beans

When running Camel integrations with the CLI, the runtime is `camel-main` based — there is no Spring Boot or Quarkus container. However, annotation-based dependency injection is supported across all three styles: Camel-native, Spring Boot, and Quarkus annotations.

> **Note**
> There is basic support for including regular Java source files together with Camel routes. The CLI compiles them at runtime, so you can include utility classes, POJOs, processors, and other classes your application needs.

## Using Camel dependency injection

Camel-native annotations for standalone use:

-   `@BindToRegistry` on a class — creates an instance and registers it in the [Registry](registry.md)
    
-   `@Configuration` on a class — runs during Camel startup for custom setup code
    
-   `@BeanInject` on a field — injects a bean from the Registry
    
-   `@PropertyInject` on a field — injects a [property placeholder](using-propertyplaceholder.md) value
    
-   `@BindToRegistry` on a method — creates a bean by invoking the method
    
-   `@Converter` on a class — auto-registers [type converters](type-converter.md)
    

> **Important**
> `@BeanInject` can reference beans annotated with `@BindToRegistry`, but the dependency must be registered before the dependent bean.

## Using Spring Boot dependency injection

These Spring annotations work in Camel standalone (no Spring container required):

-   `@Component` or `@Service` on a class — registers an instance in the Registry
    
-   `@Autowired` on a field — injects a bean (`@Qualifier` specifies the bean id)
    
-   `@Value` on a field — injects a property placeholder
    
-   `@Bean` on a method — creates a bean by invoking the method
    

## Using Quarkus dependency injection

These Jakarta/MicroProfile annotations work in Camel standalone (no Quarkus container required):

-   `@ApplicationScoped` or `@Singleton` on a class — registers an instance (`@Named` specifies the bean id)
    
-   `@Inject` on a field — injects a bean (`@Named` specifies the bean id)
    
-   `@ConfigProperty` on a field — injects a property placeholder
    
-   `@Produces` on a method — creates a bean (`@Named` specifies the bean id)
    

## Defining beans in XML DSL

When using [XML DSL](../components/4.22.x/others/java-xml-io-dsl.md), you can declare beans that are added to the [Registry](registry.md):

```xml
<camel>

    <bean name="beanFromMap" type="com.acme.MyBean">
        <properties>
            <property key="foo" value="bar" />
        </properties>
    </bean>

</camel>
```

Properties can use nested `<property>` elements or dotted notation:

```xml
<camel>

    <!-- nested properties style -->
    <bean name="beanFromMap" type="com.acme.MyBean">
        <properties>
            <property key="field1" value="f1_p" />
            <property key="nested">
                <properties>
                    <property key="field1" value="nf1_p" />
                </properties>
            </property>
        </properties>
    </bean>

    <!-- dotted properties style -->
    <bean name="beanFromProps" type="com.acme.MyBean">
        <properties>
            <property key="field1" value="f1_p" />
            <property key="nested.field1" value="nf1_p" />
        </properties>
    </bean>

</camel>
```

## Using Spring Beans XML in Camel XML DSL

You can use Spring Beans XML namespace inside Camel XML DSL. The beans are added to the [Registry](registry.md) — this does not require Spring Framework at runtime.

Supported features:

-   Dependency injection
    
-   Constructor injection
    
-   Dependency cycles
    
-   Wiring existing Camel objects (like `CamelContext`)
    

```xml
<camel>

    <beans xmlns="http://www.springframework.org/schema/beans">
        <bean id="messageString" class="java.lang.String">
            <constructor-arg index="0" value="Hello"/>
        </bean>

        <bean id="greeter" class="org.apache.camel.main.app.Greeter">
            <property name="message">
                <bean class="org.apache.camel.main.app.GreeterMessage">
                    <property name="msg" ref="messageString"/>
                </bean>
            </property>
        </bean>
    </beans>

    <route id="my-route">
        <from uri="direct:start"/>
        <bean ref="greeter"/>
        <to uri="mock:finish"/>
    </route>

</camel>
```

### Predefined Camel beans

These beans can be referenced without declaring them:

-   `CamelContext` — the current `org.apache.camel.CamelContext`
    
-   `MainConfiguration` — the `org.apache.camel.main.MainConfigurationProperties` instance
    

For example:

```xml
<beans xmlns="http://www.springframework.org/schema/beans">
    <bean id="greeter" class="org.apache.camel.main.app.Greeter">
        <property name="camelContext" ref="CamelContext"/>
    </bean>
</beans>
```

### Customizing Camel internals

You can register beans that affect `CamelContext` configuration. For example, to replace the default UUID generator:

```xml
<camel>

    <beans xmlns="http://www.springframework.org/schema/beans">
        <bean id="customUUIDGenerator" class="org.apache.camel.support.ShortUuidGenerator" />
    </beans>

</camel>
```

Camel looks up known SPI types (like `UuidGenerator`) in the Registry and uses them automatically.
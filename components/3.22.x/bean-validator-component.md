# Bean Validator

**Since Camel 2.3**

**Only producer is supported**

The Validator component performs bean validation of the message body using the Java Bean Validation API ([JSR 303](http://jcp.org/en/jsr/detail?id=303)). Camel uses the reference implementation, which is [Hibernate Validator](https://docs.jboss.org/hibernate/validator/6.2/reference/en-US/html_single/).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-bean-validator</artifactId>
    <version>x.y.z</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

bean-validator:label\[?options\]

Where **label** is an arbitrary text value describing the endpoint.  
You can append query options to the URI in the following format, ?option=value&option=value&…​

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Bean Validator component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ignoreXmlConfiguration** (producer) | Whether to ignore data from the META-INF/validation.xml file. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **constraintValidatorFactory** (advanced) | To use a custom ConstraintValidatorFactory. |  | ConstraintValidatorFactory |
| **messageInterpolator** (advanced) | To use a custom MessageInterpolator. |  | MessageInterpolator |
| **traversableResolver** (advanced) | To use a custom TraversableResolver. |  | TraversableResolver |
| **validationProviderResolver** (advanced) | To use a a custom ValidationProviderResolver. |  | ValidationProviderResolver |
| **validatorFactory** (advanced) | **Autowired** To use a custom ValidatorFactory. |  | ValidatorFactory |

## Endpoint Options

The Bean Validator endpoint is configured using URI syntax:

bean-validator:label

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Where label is an arbitrary text value describing the endpoint. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **group** (producer) | To use a custom validation group. | javax.validation.groups.Default | String |
| **ignoreXmlConfiguration** (producer) | Whether to ignore data from the META-INF/validation.xml file. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **constraintValidatorFactory** (advanced) | To use a custom ConstraintValidatorFactory. |  | ConstraintValidatorFactory |
| **messageInterpolator** (advanced) | To use a custom MessageInterpolator. |  | MessageInterpolator |
| **traversableResolver** (advanced) | To use a custom TraversableResolver. |  | TraversableResolver |
| **validationProviderResolver** (advanced) | To use a a custom ValidationProviderResolver. |  | ValidationProviderResolver |
| **validatorFactory** (advanced) | To use a custom ValidatorFactory. |  | ValidatorFactory |

## OSGi deployment

To use Hibernate Validator in the OSGi environment use dedicated `ValidationProviderResolver` implementation, just as `org.apache.camel.component.bean.validator.HibernateValidationProviderResolver`. The snippet below demonstrates this approach. You can also use `HibernateValidationProviderResolver`.

**Using HibernateValidationProviderResolver**

```java
from("direct:test").
  to("bean-validator://ValidationProviderResolverTest?validationProviderResolver=#myValidationProviderResolver");
```

```xml
<bean id="myValidationProviderResolver" class="org.apache.camel.component.bean.validator.HibernateValidationProviderResolver"/>
```

If no custom `ValidationProviderResolver` is defined and the validator component has been deployed into the OSGi environment, the `HibernateValidationProviderResolver` will be automatically used.

## Example

Assumed we have a java bean with the following annotations

**Car.java**

```java
public class Car {

    @NotNull
    private String manufacturer;

    @NotNull
    @Size(min = 5, max = 14, groups = OptionalChecks.class)
    private String licensePlate;

    // getter and setter
}
```

and an interface definition for our custom validation group

**OptionalChecks.java**

```java
public interface OptionalChecks {
}
```

with the following Camel route, only the **@NotNull** constraints on the attributes manufacturer and licensePlate will be validated (Camel uses the default group `javax.validation.groups.Default`).

```java
from("direct:start")
.to("bean-validator://x")
.to("mock:end")
```

If you want to check the constraints from the group `OptionalChecks`, you have to define the route like this

```java
from("direct:start")
.to("bean-validator://x?group=OptionalChecks")
.to("mock:end")
```

If you want to check the constraints from both groups, you have to define a new interface first

**AllChecks.java**

```java
@GroupSequence({Default.class, OptionalChecks.class})
public interface AllChecks {
}
```

and then your route definition should looks like this

```java
from("direct:start")
.to("bean-validator://x?group=AllChecks")
.to("mock:end")
```

And if you have to provide your own message interpolator, traversable resolver and constraint validator factory, you have to write a route like this

```xml
<bean id="myMessageInterpolator" class="my.ConstraintValidatorFactory" />
<bean id="myTraversableResolver" class="my.TraversableResolver" />
<bean id="myConstraintValidatorFactory" class="my.ConstraintValidatorFactory" />
```

```java
from("direct:start")
.to("bean-validator://x?group=AllChecks&messageInterpolator=#myMessageInterpolator
&traversableResolver=#myTraversableResolver&constraintValidatorFactory=#myConstraintValidatorFactory")
.to("mock:end")
```

It’s also possible to describe your constraints as XML and not as Java annotations. In this case, you have to provide the file `META-INF/validation.xml` which could looks like this

**validation.xml**

```xml
<validation-config
    xmlns="http://jboss.org/xml/ns/javax/validation/configuration"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://jboss.org/xml/ns/javax/validation/configuration">

    <default-provider>org.hibernate.validator.HibernateValidator</default-provider>
    <message-interpolator>org.hibernate.validator.engine.ResourceBundleMessageInterpolator</message-interpolator>
    <traversable-resolver>org.hibernate.validator.engine.resolver.DefaultTraversableResolver</traversable-resolver>
    <constraint-validator-factory>org.hibernate.validator.engine.ConstraintValidatorFactoryImpl</constraint-validator-factory>
    <constraint-mapping>/constraints-car.xml</constraint-mapping>

</validation-config>
```

and the `constraints-car.xml` file

**constraints-car.xml**

```xml
<constraint-mappings xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://jboss.org/xml/ns/javax/validation/mapping validation-mapping-1.0.xsd"
    xmlns="http://jboss.org/xml/ns/javax/validation/mapping">

    <default-package>org.apache.camel.component.bean.validator</default-package>

    <bean class="CarWithoutAnnotations" ignore-annotations="true">
        <field name="manufacturer">
            <constraint annotation="javax.validation.constraints.NotNull" />
        </field>

        <field name="licensePlate">
            <constraint annotation="javax.validation.constraints.NotNull" />

            <constraint annotation="javax.validation.constraints.Size">
                <groups>
                    <value>org.apache.camel.component.bean.validator.OptionalChecks</value>
                </groups>
                <element name="min">5</element>
                <element name="max">14</element>
            </constraint>
        </field>
    </bean>
</constraint-mappings>
```

Here is the XML syntax for the example route definition where **OrderedChecks** can be [https://github.com/apache/camel/blob/main/components/camel-bean-validator/src/test/java/org/apache/camel/component/bean/validator/OrderedChecks.java](https://github.com/apache/camel/blob/main/components/camel-bean-validator/src/test/java/org/apache/camel/component/bean/validator/OrderedChecks.java)

Note that the body should include an instance of a class to validate.

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
    http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
    http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">

    <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
        <route>
            <from uri="direct:start"/>
            <to uri="bean-validator://x?group=org.apache.camel.component.bean.validator.OrderedChecks"/>
        </route>
    </camelContext>
</beans>
```

## Spring Boot Auto-Configuration

When using bean-validator with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-bean-validator-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.bean-validator.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.bean-validator.constraint-validator-factory** | To use a custom ConstraintValidatorFactory. The option is a javax.validation.ConstraintValidatorFactory type. |  | ConstraintValidatorFactory |
| **camel.component.bean-validator.enabled** | Whether to enable auto configuration of the bean-validator component. This is enabled by default. |  | Boolean |
| **camel.component.bean-validator.ignore-xml-configuration** | Whether to ignore data from the META-INF/validation.xml file. | false | Boolean |
| **camel.component.bean-validator.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.bean-validator.message-interpolator** | To use a custom MessageInterpolator. The option is a javax.validation.MessageInterpolator type. |  | MessageInterpolator |
| **camel.component.bean-validator.traversable-resolver** | To use a custom TraversableResolver. The option is a javax.validation.TraversableResolver type. |  | TraversableResolver |
| **camel.component.bean-validator.validation-provider-resolver** | To use a a custom ValidationProviderResolver. The option is a javax.validation.ValidationProviderResolver type. |  | ValidationProviderResolver |
| **camel.component.bean-validator.validator-factory** | To use a custom ValidatorFactory. The option is a javax.validation.ValidatorFactory type. |  | ValidatorFactory |
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

Where **label** is an arbitrary text value describing the endpoint. You can append query options to the URI in the following format: `?option=value&option=value&…​`

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

The Bean Validator component supports the following options which are listed below.

   
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

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Where label is an arbitrary text value describing the endpoint. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **group** (producer) | To use a custom validation group. | jakarta.validation.groups.Default | String |
| **ignoreXmlConfiguration** (producer) | Whether to ignore data from the META-INF/validation.xml file. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **constraintValidatorFactory** (advanced) | To use a custom ConstraintValidatorFactory. |  | ConstraintValidatorFactory |
| **messageInterpolator** (advanced) | To use a custom MessageInterpolator. |  | MessageInterpolator |
| **traversableResolver** (advanced) | To use a custom TraversableResolver. |  | TraversableResolver |
| **validationProviderResolver** (advanced) | To use a a custom ValidationProviderResolver. |  | ValidationProviderResolver |
| **validatorFactory** (advanced) | To use a custom ValidatorFactory. |  | ValidatorFactory |

### Using HibernateValidationProviderResolver

-   Java
    
-   XML
    

```java
from("direct:test").
  to("bean-validator://ValidationProviderResolverTest?validationProviderResolver=#myValidationProviderResolver");
```

```xml
<bean id="myValidationProviderResolver" class="org.apache.camel.component.bean.validator.HibernateValidationProviderResolver"/>
```

## Example

Assumed we have a java bean with the following annotations

**Car.java**

_Java-only: Java Bean with validation annotations_

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

_Java-only: custom validation group interface_

```java
public interface OptionalChecks {
}
```

with the following Camel route, only the **@NotNull** constraints on the attributes `manufacturer` and `licensePlate` will be validated (Camel uses the default group `jakarta.validation.groups.Default`).

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("bean-validator://x")
    .to("mock:end");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="bean-validator://x"/>
  <to uri="mock:end"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: bean-validator://x
        - to:
            uri: mock:end
```

If you want to check the constraints from the group `OptionalChecks`, you have to define the route like this

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("bean-validator://x?group=OptionalChecks")
    .to("mock:end");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="bean-validator://x?group=OptionalChecks"/>
  <to uri="mock:end"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: bean-validator://x
            parameters:
              group: OptionalChecks
        - to:
            uri: mock:end
```

If you want to check the constraints from both groups, you have to define a new interface first:

**AllChecks.java**

_Java-only: combined validation group interface using @GroupSequence_

```java
@GroupSequence({Default.class, OptionalChecks.class})
public interface AllChecks {
}
```

And then your route definition should look like this:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("bean-validator://x?group=AllChecks")
    .to("mock:end");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="bean-validator://x?group=AllChecks"/>
  <to uri="mock:end"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: bean-validator://x
            parameters:
              group: AllChecks
        - to:
            uri: mock:end
```

And if you have to provide your own message interpolator, traversable resolver and constraint validator factory, you have to write a route like this:

-   Java
    
-   XML
    

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

It’s also possible to describe your constraints as XML and not as Java annotations. In this case, you have to provide the files `META-INF/validation.xml` and `constraints-car.xml` which could look like this:

-   validation.xml
    
-   constraints-car.xml
    

```xml
<validation-config
        xmlns="https://jakarta.ee/xml/ns/validation/configuration"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://jakarta.ee/xml/ns/validation/configuration https://jakarta.ee/xml/ns/validation/validation-configuration-3.0.xsd"
        version="3.0">

    <default-provider>org.hibernate.validator.HibernateValidator</default-provider>
    <message-interpolator>org.hibernate.validator.engine.ResourceBundleMessageInterpolator</message-interpolator>
    <traversable-resolver>org.hibernate.validator.engine.resolver.DefaultTraversableResolver</traversable-resolver>
    <constraint-validator-factory>org.hibernate.validator.engine.ConstraintValidatorFactoryImpl</constraint-validator-factory>
    <constraint-mapping>/constraints-car.xml</constraint-mapping>

</validation-config>
```

```xml
<constraint-mappings
        xmlns="https://jakarta.ee/xml/ns/validation/mapping"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://jakarta.ee/xml/ns/validation/mapping
            https://jakarta.ee/xml/ns/validation/validation-mapping-3.0.xsd"
        version="3.0">

    <default-package>org.apache.camel.component.bean.validator</default-package>

    <bean class="CarWithoutAnnotations" ignore-annotations="true">
        <field name="manufacturer">
            <constraint annotation="jakarta.validation.constraints.NotNull" />
        </field>

        <field name="licensePlate">
            <constraint annotation="jakarta.validation.constraints.NotNull" />

            <constraint annotation="jakarta.validation.constraints.Size">
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

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("bean-validator://x?group=org.apache.camel.component.bean.validator.OrderedChecks");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="bean-validator://x?group=org.apache.camel.component.bean.validator.OrderedChecks"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: bean-validator://x
            parameters:
              group: org.apache.camel.component.bean.validator.OrderedChecks
```
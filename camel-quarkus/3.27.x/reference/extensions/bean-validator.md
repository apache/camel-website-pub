# Bean Validator

JVM since1.0.0 Native since1.0.0

Validate the message body using the Java Bean Validation API.

## What’s inside

-   [Bean Validator component](../../../../components/4.14.x/bean-validator-component.md), URI syntax: `bean-validator:label`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-bean-validator)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-bean-validator</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Configuring the ValidatorFactory

Implementation of this extension leverages the [Quarkus Hibernate Validator extension](https://quarkus.io/guides/validation).

Therefore it is not possible to configure the `ValidatorFactory` by Camel’s properties (`constraintValidatorFactory`, `messageInterpolator`, `traversableResolver`, `validationProviderResolver` and `validatorFactory`).

You can configure the `ValidatorFactory` by the creation of beans which will be injected into the default `ValidatorFactory` (created by Quarkus). See the [Quarkus CDI documentation](https://quarkus.io/guides/validation#hibernate-validator-extension-and-cdi) for more information.

### Custom validation groups in native mode

When using custom validation groups in native mode, all the interfaces need to be registered for reflection (see the [documentation](https://quarkus.io/guides/writing-native-applications-tips#register-reflection)).

Example:

```java
@RegisterForReflection
public interface OptionalChecks {
}
```

## Camel Quarkus limitations

It is not possible to describe your constraints as XML (by providing the file META-INF/validation.xml), only Java annotations are supported. This is caused by the limitation of the Quarkus Hibernate Validator extension (see the [issue](https://github.com/quarkusio/quarkus/issues/24027)).
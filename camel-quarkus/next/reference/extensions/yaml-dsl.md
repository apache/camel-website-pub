# YAML DSL

JVM since1.8.0 Native since1.8.0

Camel YAML DSL

## What’s inside

-   [YAML DSL](../../../../components/next/others/yaml-dsl.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-yaml-dsl)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-yaml-dsl</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Native mode

Some constructs defined within Camel YAML DSL markup require classes to be registered for reflection. Refer to the [Native mode](../../user-guide/native-mode.html#reflection) guide for details.

#### Bean definitions

The YAML DSL provides the capability to define beans as follows.

```yaml
- beans:
    - name: "greetingBean"
      type: "org.acme.GreetingBean"
      properties:
        greeting: "Hello World!"
- route:
    id: "my-yaml-route"
    from:
      uri: "timer:from-yaml?period=1000"
      steps:
        - to: "bean:greetingBean"
```

In this example, the `GreetingBean` class needs to be registered for reflection. This applies to any types that you refer to under the `beans` key in your YAML routes.

```java
@RegisterForReflection
public class GreetingBean {
}
```

#### Exception handling

Exception classes referenced by `onException`, `doCatch` and `throwException` in YAML routes are detected at build time and registered for reflection automatically. You only need to register exception classes for reflection yourself if they are referenced in a way that cannot be detected at build time.
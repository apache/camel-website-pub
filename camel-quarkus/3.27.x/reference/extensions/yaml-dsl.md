# YAML DSL

JVM since1.8.0 Native since1.8.0

An YAML stack for parsing YAML route definitions

## What’s inside

-   [YAML DSL](../../../../components/4.14.x/others/yaml-dsl.md)
    

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

The following constructs when defined within Camel YAML DSL markup, require you to register classes for reflection. Refer to the [Native mode](../../user-guide/native-mode.html#reflection) guide for details.

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

Camel provides various methods of handling exceptions. Some of these require that any exception classes referenced in their DSL definitions are registered for reflection.

`**on-exception**`

```yaml
- on-exception:
    handled:
      constant: "true"
    exception:
      - "org.acme.MyHandledException"
    steps:
      - transform:
          constant: "Sorry something went wrong"
```

```java
@RegisterForReflection
public class MyHandledException {
}
```

`**throw-exception**`

```yaml
- route:
    id: "my-yaml-route"
    from:
      uri: "direct:start"
      steps:
        - choice:
            when:
              - simple: "${body} == 'bad value'"
                steps:
                  - throw-exception:
                      exception-type: "org.acme.ForcedException"
                      message: "Forced exception"
            otherwise:
              steps:
                - to: "log:end"
```

```java
@RegisterForReflection
public class ForcedException {
}
```

`**do-catch**`

```yaml
- route:
    id: "my-yaml-route2"
    from:
      uri: "direct:tryCatch"
      steps:
        - do-try:
            steps:
              - to: "direct:readFile"
            do-catch:
              - exception:
                  - "java.io.FileNotFoundException"
                steps:
                  - transform:
                      constant: "do-catch caught an exception"
```

```java
@RegisterForReflection(targets = FileNotFoundException.class)
public class MyClass {
}
```
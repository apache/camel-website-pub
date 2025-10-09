# Build time properties

You may be required to provide certain **build-time properties** that are needed only during the process of `Integration` building. Since Camel K version 1.5, we introduced a `--build-property` flag that will be handful in such circumstances. The property value may be also used inside Camel K integrations using the **property placeholder** mechanism.

> **Note**
> the --build-property option is syntactic sugar for `builder.properties` trait.

## Single property

You will find this feature very useful when dealing with configuration that affects how `Quarkus` builds the `Integration`. For example, let’s see how to override the default `quarkus.application.name` expected by any `Quarkus` application:

build-property-route.yaml

```yaml
- from:
    uri: "timer:build-property"
    steps:
      - setBody:
          simple: "The application name: {{quarkus.application.name}}"
      - to: "log:info"
```

In order to give a value to the `quarkus.application.name` property you can pass it using the command line with the `--build-property` flag:

kamel run --build-property=quarkus.application.name=my-super-application build-property-route.yaml

You can provide more than one single `build-property` at once by just adding the flag repeatedly (ie, `--build-property=prop1=val1 --build-property=prop2=val2 …​`)

## Property File

Repeating the `--build-property` flag when you have many **build time configuration** may be cumbersome. Usually you deal with property files instead. You will be able to use the _file_ syntax available for `--build-property` flag. Here, as an example you have a property file with 2 `Quarkus` properties:

quarkus.properties

```properties
quarkus.application.name = my-super-application
quarkus.banner.enabled = true
```

build-property-route.yaml

```yaml
- from:
    uri: "timer:build-property"
    steps:
      - setBody:
          simple: "The application name: {{quarkus.application.name}}"
      - to: "log:info"
```

The `quarkus.banner.enabled` is configured to show the banner during the `Integration` startup. Let’s use `--build-property` flag in conjunction with file:

kamel run --build-property=file:quarkus.properties build-property-route.yaml

The property file is parsed and its properties configured on the `Integration`. As soon as the application starts, you will see the log with the expected configuration.

## Property collision priority

If you have a property repeated more than once, the general rule is that the last one declared in your `kamel run` statement will be taken in consideration. If the same property is found both in a single option declaration and inside a file, then, the single option will have higher priority and will be used.

## Run time properties

If you’re looking for **runtime properties configuration** you can look at the [Camel properties](camel-properties.md) section.
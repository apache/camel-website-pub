# Jasypt

JVM since1.2.0 Native since3.7.0

Security using Jasypt

## What’s inside

-   [Jasypt](../../../../components/next/others/jasypt.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jasypt)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jasypt</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

The configuration of Jasypt in Camel Quarkus is driven by [configuration properties](#extensions-jasypt-additional-camel-quarkus-configuration).

The minimum expectation is that you provide a master password for Jasypt decryption with configuration property `quarkus.camel.jasypt.password`.

You can choose the encryption algorithm and other aspects of the Jasypt configuration via the `quarkus.camel.jasypt` options described below.

By default, you do not need to write custom code to configure the Camel `JasyptPropertiesParser` or `PropertiesComponent`. This is done for you automatically.

Any Camel configuration property added to `application.properties` can be secured with Jasypt. To encrypt a value, there is a utility that can be run with [JBang](https://www.jbang.dev/).

```shell
jbang org.apache.camel:camel-jasypt:4.19.0 -c encrypt -p secret-password -i "Some secret content"
```

> **Important**
> If you choose to use a different Jasypt algorithm to the default (`PBEWithMD5AndDES`), you must provide `-a` (algorithm), `-riga` (IV generator algorithm) & `-rsga` (Salt generator algorithm) arguments to set the correct algorithms used in encryption. Else your application will not be able to decrypt configuration values.

Alternatively, when running in dev mode, open the [Dev UI](https://quarkus.io/guides/dev-mode-differences#dev-ui) and click the 'utilities' link in the Camel Jasypt pane. Next, select either the 'Decrypt' or 'Encrypt' action, enter some text and click the submit button. The result of the action is output together with a button to copy it to the clipboard.

Configuration properties can be added to `application.properties` with the encrypted value enclosed within `ENC()` For example.

```none
my.secret = ENC(BoDSRQfdBME4V/AcugPOkaR+IcyKufGz)
```

In your Camel routes, you can refer to the property name using the standard placeholder syntax and its value will get decrypted.

```java
public class MySecureRoute extends RouteBuilder {
    @Override
    public void configure() {
        from("timer:tick?period=5s")
            .to("{{my.secret}}");
    }
}
```

> **Tip**
> You can use the ability to mask security sensitive configuration in Camel by suffixing property values with `.secret`. You can also disable the startup configuration summary with the configuration `camel.main.autoConfigurationLogSummary = false`.

### Injecting encrypted configuration

You can use the `@ConfigProperty` annotation to inject encrypted configuration into your Camel routes or CDI beans.

```java
@ApplicationScoped
public class MySecureRoute extends RouteBuilder {
    @ConfigInject("my.secret")
    String mySecret;

    @Override
    public void configure() {
        from("timer:tick?period=5s")
            .to(mySecret);
    }
}
```

#### Securing alternate configuration sources

If you prefer to keep your secret configuration in a file separate to `application.properties`, you can use the `quarkus.config.locations` configuration option to specify additional configuration files.

In native mode you must also add any additional configuration file resource paths to `quarkus.native.resources.includes`.

#### Finer control of Jasypt configuration

If you require finer control of the Jasypt configuration than that provided by the default configuration, the following options are available.

##### JasyptConfigurationCustomizer

Implement a `JasyptConfigurationCustomizer` class to customize any aspect of the Jasypt `EnvironmentStringPBEConfig`.

```java
package org.acme;

import org.apache.camel.quarkus.component.jasypt.JasyptConfigurationCustomizer;
import org.jasypt.encryption.pbe.config.EnvironmentStringPBEConfig;
import org.jasypt.iv.RandomIvGenerator;
import org.jasypt.salt.RandomSaltGenerator;

public class JasyptConfigurationCustomizer implements JasyptConfigurationCustomizer {
    public void customize(EnvironmentStringPBEConfig config) {
        // Custom algorithms
        config.setAlgorithm("PBEWithHmacSHA256AndAES_256");
        config.setSaltGenerator(new RandomSaltGenerator("PKCS11"));
        config.setIvGenerator(new RandomIvGenerator("PKCS11"));
        // Additional customizations...
    }
}
```

In `application.properties` add the `quarkus.camel.jasypt.configuration-customizer-class-name` configuration property.

```none
quarkus.camel.jasypt.configuration-customizer-class-name = org.acme.MyJasyptEncryptorCustomizer
```

##### Disabling automatic Jasypt configuration

If you prefer to use the 'classic' Java DSL way of configuring Camel Jasypt, you can disable the automatic configuration with `quarkus.camel.jasypt.enabled = false`.

This allows you to configure the Camel `JasyptPropertiesParser` and `PropertiesComponent` manually.

> **Note**
> In this mode, you cannot use the `@ConfigProperty` annotation to inject encrypted configuration properties.

```java
import org.apache.camel.CamelContext;
import org.apache.camel.component.jasypt.JasyptPropertiesParser;
import org.apache.camel.component.properties.PropertiesComponent;

public class MySecureRoute extends RouteBuilder {
    @Override
    public void configure() {
        JasyptPropertiesParser jasypt = new JasyptPropertiesParser();
        jasypt.setPassword("secret");

        PropertiesComponent component = (PropertiesComponent) getContext().getPropertiesComponent();
        jasypt.setPropertiesComponent(component);
        component.setPropertiesParser(jasypt);

        from("timer:tick?period=5s")
            .to("{{my.secret}}");
    }
}
```

> **Note**
> If you call `setLocation(…​)` on the `PropertiesComponent` to specify a custom configuration file location using the `classpath:` prefix, you must add the file to `quarkus.native.resources.includes` so that it can be loaded in native mode.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.jasypt.enabled](#quarkus-camel-jasypt-enabled)`
Setting this option to false will disable Jasypt integration with Quarkus SmallRye configuration. You can however, manually configure Jasypt with Camel in the 'classic' way of manually configuring JasyptPropertiesParser and PropertiesComponent. Refer to the usage section for more details.

 | `boolean` | `true` |
| `[quarkus.camel.jasypt.algorithm](#quarkus-camel-jasypt-algorithm)`

The algorithm to be used for decryption.

 | `string` | `PBEWithMD5AndDES` |
| `[quarkus.camel.jasypt.password](#quarkus-camel-jasypt-password)`

The master password used by Jasypt for decrypting configuration values. This option supports prefixes which influence the master password lookup behaviour.

`sys:` will to look up the value from a JVM system property. `sysenv:` will look up the value from the OS system environment with the given key.

 | `string` |  |
| `[quarkus.camel.jasypt.random-iv-generator-algorithm](#quarkus-camel-jasypt-random-iv-generator-algorithm)`

Configures the Jasypt StandardPBEStringEncryptor with a RandomIvGenerator using the given algorithm.

 | `string` | `SHA1PRNG` |
| `[quarkus.camel.jasypt.random-salt-generator-algorithm](#quarkus-camel-jasypt-random-salt-generator-algorithm)`

Configures the Jasypt StandardPBEStringEncryptor with a RandomSaltGenerator using the given algorithm.

 | `string` | `SHA1PRNG` |
| `[quarkus.camel.jasypt.configuration-customizer-class-name](#quarkus-camel-jasypt-configuration-customizer-class-name)`

The fully qualified class name of an org.apache.camel.quarkus.component.jasypt.JasyptConfigurationCustomizer implementation. This provides the optional capability of having full control over the Jasypt configuration.

 | `string` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.
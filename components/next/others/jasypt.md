# Jasypt

**Since Camel 2.5**

[Jasypt](http://www.jasypt.org/) is a simplified encryption library that makes encryption and decryption easy. Camel integrates with Jasypt to allow sensitive information in [Properties](../properties-component.md) files to be encrypted. By dropping **`camel-jasypt`** on the classpath those encrypted values will automatically be decrypted on-the-fly by Camel. This ensures that human eyes can’t easily spot sensitive information such as usernames and passwords.

If you are using Maven, you need to add the following dependency to your `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jasypt</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Tooling

> **Warning**
> The command line utility shipped with `camel-jasypt` (the `Main` class) is **deprecated** and will be removed in a future Camel release. Use the standalone CLI scripts (`encrypt.sh` / `decrypt.sh` / `digest.sh`) shipped in the upstream [jasypt-1.9.3 distribution](https://github.com/jasypt/jasypt/releases/tag/jasypt-1.9.3) instead — they cover the same encrypt/decrypt workflow and let us drop the duplicated implementation maintained here.

The Jasypt component is a runnable JAR that provides a command line utility to encrypt or decrypt values.

The usage documentation can be output to the console to describe the syntax and options it provides:

```text
Apache Camel Jasypt takes the following options

  -h or -help = Displays the help screen
  -c or -command <command> = Command either encrypt or decrypt
  -p or -password <password> = Password to use
  -i or -input <input> = Text to encrypt or decrypt
  -a or -algorithm <algorithm> = Optional algorithm to use
  -rsga or -algorithm <algorithm> = Optional random salt generator algorithm to use
  -riga or -algorithm <algorithm> = Optional random iv generator algorithm to use
```

A simple way of running the tool is with [JBang](https://www.jbang.dev/).

For example, to encrypt the value `tiger`, you can use the following parameters. Make sure to specify the version of camel-jasypt that you want to use.

```bash
$ jbang org.apache.camel:camel-jasypt:<camel version here> -c encrypt -p secret -i tiger
```

Which outputs the following result

```text
Encrypted text: qaEEacuW7BUti8LcMgyjKw==
```

This means the encrypted representation `qaEEacuW7BUti8LcMgyjKw==` can be decrypted back to `tiger` if you know the _master_ password which was `secret`.  
If you run the tool again, then the encrypted value will return a different result. But decrypting the value will always return the correct original value.

You can test decrypting the value by running the tooling using the following parameters:

```bash
$ jbang org.apache.camel:camel-jasypt:<camel version here> -c decrypt -p secret -i qaEEacuW7BUti8LcMgyjKw==
```

Which outputs the following result:

```text
Decrypted text: tiger
```

The idea is to then use the encrypted values in your [Properties](../properties-component.md) files. For example.

```text
# Encrypted value for 'tiger'
my.secret = ENC(qaEEacuW7BUti8LcMgyjKw==)
```

## Protecting the master password

The _master_ password used by Jasypt must be provided, so that it’s capable of decrypting the values. However, having this _master_ password out in the open may not be an ideal solution. Therefore, you can provide it as a JVM system property or as an OS environment setting. If you decide to do so then the `password` option supports prefix that dictates this:

-   `sysenv:` means to look up the OS system environment with the given key.
    
-   `sys:` means to look up a JVM system property.
    

For example, you could provide the password before you start the application

```bash
$ export CAMEL_ENCRYPTION_PASSWORD=secret
```

Then start the application, such as running the start script.

When the application is up and running, you can unset the environment

```bash
$ unset CAMEL_ENCRYPTION_PASSWORD
```

On runtimes like Spring Boot and Quarkus, you can configure a password property in `application.properties` as follows.

```text
password=sysenv:CAMEL_ENCRYPTION_PASSWORD
```

Or if configuring `JasyptPropertiesParser` manually, you can set the password like this.

```java
jasyptPropertiesParser.setPassword("sysenv:CAMEL_ENCRYPTION_PASSWORD");
```

## Example configuration

-   Java
    
-   XML (Spring)
    

On the Spring Boot and Quarkus runtimes, Camel Jasypt can be configured via configuration properties. Refer to their respective documentation pages for more information.

Else, in Java DSL you need to configure Jasypt as a `JasyptPropertiesParser` instance and set it on the [Properties](../properties-component.md) component as shown below:

```java
// create the jasypt properties parser
JasyptPropertiesParser jasypt = new JasyptPropertiesParser();
// set the master password (see above for how to do this in a secure way)
jasypt.setPassword("secret");

// create the properties' component
PropertiesComponent pc = new PropertiesComponent();
pc.setLocation("classpath:org/apache/camel/component/jasypt/secret.properties");
// and use the jasypt properties parser, so we can decrypt values
pc.setPropertiesParser(jasypt);
// end enable nested placeholder support
pc.setNestedPlaceholder(true);

// add properties component to camel context
context.setPropertiesComponent(pc);
```

It is possible to configure custom algorithms on the JasyptPropertiesParser like this.

```java
JasyptPropertiesParser jasyptPropertiesParser = new JasyptPropertiesParser();

jasyptPropertiesParser.setAlgorithm("PBEWithHmacSHA256AndAES_256");
jasyptPropertiesParser.setRandomSaltGeneratorAlgorithm("PKCS11");
jasyptPropertiesParser.setRandomIvGeneratorAlgorithm("PKCS11");
```

The properties file `secret.properties` will contain your encrypted configuration values, such as shown below. Notice how the password value is encrypted and is surrounded like `ENC(value here)`.

```text
my.secret.password=ENC(bsW9uV37gQ0QHFu7KO03Ww==)
```

In Spring XML you need to configure the `JasyptPropertiesParser` which is shown below. Then the Camel [Properties](../properties-component.md) component is told to use `jasypt` as the property parser, which means Jasypt has its chance to decrypt values looked up in the properties file.

```xml
<!-- define the jasypt properties parser with the given password to be used -->
<bean id="jasypt" class="org.apache.camel.component.jasypt.JasyptPropertiesParser">
    <property name="password" value="secret"/>
</bean>

<!-- define the camel properties component -->
<bean id="properties" class="org.apache.camel.component.properties.PropertiesComponent">
    <!-- the properties file is in the classpath -->
    <property name="location" value="classpath:org/apache/camel/component/jasypt/secret.properties"/>
    <!-- and let it leverage the jasypt parser -->
    <property name="propertiesParser" ref="jasypt"/>
    <!-- end enable nested placeholder -->
    <property name="nestedPlaceholder" value="true"/>
</bean>
```

The [Properties](../properties-component.md) component can also be inlined inside the `<camelContext>` tag which is shown below. Notice how we use the `propertiesParserRef` attribute to refer to Jasypt.

```xml
<!-- define the jasypt properties parser with the given password to be used -->
<bean id="jasypt" class="org.apache.camel.component.jasypt.JasyptPropertiesParser">
    <!-- password is mandatory, you can prefix it with sysenv: or sys: to indicate it should use
         an OS environment or JVM system property value, so you don't have the master password defined here -->
    <property name="password" value="secret"/>
</bean>

<camelContext xmlns="http://camel.apache.org/schema/spring">
    <!-- define the camel properties placeholder, and let it leverage jasypt -->
    <propertyPlaceholder id="properties"
                         location="classpath:org/apache/camel/component/jasypt/secret.properties"
                         nestedPlaceholder="true"
                         propertiesParserRef="jasypt"/>
    <route>
        <from uri="direct:start"/>
        <to uri="{{cool.result}}"/>
    </route>
</camelContext>
```

## Spring Boot Auto-Configuration

When using jasypt with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jasypt-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jasypt.algorithm** | The algorithm to be used for decryption. Default: PBEWithMD5AndDES. | PBEWithMD5AndDES | String |
| **camel.component.jasypt.early-decryption-enabled** | Enable the early properties decryption during Spring Start Up. Enabling this feature, encrypted properties can be decrypted before the Spring Boot AutoConfiguration kicks in, for example, server.port=ENC(oBpQDDUvFY0c4WNAG0o4LIS5bWqmlxYlUUDTW2iXJIAZFYvM+3vOredaMcVfL4xW) will be decrypted to 8082, and the application will start using that port. | false | Boolean |
| **camel.component.jasypt.enabled** | Enable the component. | false | Boolean |
| **camel.component.jasypt.iv-generator-class-name** | The initialization vector (IV) generator applied in decryption operations. Default: org.jasypt.iv. |  | String |
| **camel.component.jasypt.password** | The master password used by Jasypt for decrypting the values. This option supports prefixes which influence the master password lookup behaviour: sysenv: means to lookup the OS system environment with the given key. sys: means to lookup a JVM system property. |  | String |
| **camel.component.jasypt.provider-name** | The class name of the security provider to be used for obtaining the encryption algorithm. |  | String |
| **camel.component.jasypt.random-iv-generator-algorithm** | The algorithm for the random iv generator. | SHA1PRNG | String |
| **camel.component.jasypt.random-salt-generator-algorithm** | The algorithm for the salt generator. | SHA1PRNG | String |
| **camel.component.jasypt.salt-generator-class-name** | The salt generator applied in decryption operations. Default: org.jasypt.salt.RandomSaltGenerator. | org.jasypt.salt.RandomSaltGenerator | String |
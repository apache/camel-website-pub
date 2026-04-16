# LDAP

JVM since1.1.0 Native since3.2.0

Perform searches on LDAP servers.

## What’s inside

-   [LDAP component](../../../../components/next/ldap-component.md), URI syntax: `ldap:dirContextName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-ldap)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-ldap</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Configuration via properties

The LDAP component supports property-based configuration in addition to plain Camel configuration. Configuration property should follow the pattern:

```properties
quarkus.camel.ldap.dir-contexts.<dirContextName>.<property>
```

For more details, refer to the dirContext [Javadoc](https://docs.oracle.com/en/java/javase/17/docs/api/java.naming/javax/naming/directory/DirContext.md). The following options are available:

-   initial-context-factory
    
-   provider-url
    
-   security-authentication
    
-   security-protocol
    
-   socket-factory
    

If you need to specify an option that is not listed above, use the following property format:

```properties
quarkus.camel.ldap.dr-contexts."your_name".additional-options."not-listed_option_name"
```

Here is an example of configuration of a dirContext named `your_context` using SSL.

```properties
quarkus.camel.ldap.dir-contexts."your_context".initial-context-factory=com.sun.jndi.ldap.LdapCtxFactory
quarkus.camel.ldap.dir-contexts."your_context".provider-url=ldaps://${ldap.host}:${ldap.sslPort}
quarkus.camel.ldap.dir-contexts."your_context".security-protocol=ssl
quarkus.camel.ldap.dir-contexts."your_context".socket-factory=org.apache.camel.quarkus.component.ldap.it.CustomSSLSocketFactory
```

### Using SSL in Native Mode

When using a custom `SSLSocketFactory` in native mode, such as the one in the [Configuring SSL](../../../../components/next/ldap-component.html#_configuring_ssl) section, you need to register the class for reflection otherwise the class will not be made available on the classpath. Add the `@RegisterForReflection` annotation above the class definition, as follows:

```java
@RegisterForReflection
public class CustomSSLSocketFactory extends SSLSocketFactory {
    // The class definition is the same as in the above link.
}
```

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.ldap.dir-contexts."dir-contexts".initial-context-factory](#quarkus-camel-ldap-dir-contexts-dir-contexts-initial-context-factory)`
The initial context factory to use. The value of the property should be the fully qualified class name of the factory class that will create an initial context.

 | `string` |  |
| `[quarkus.camel.ldap.dir-contexts."dir-contexts".provider-url](#quarkus-camel-ldap-dir-contexts-dir-contexts-provider-url)`

The service provider to use. The value of the property should contain a URL string (e.g. "ldap://somehost:389").

 | `string` |  |
| `[quarkus.camel.ldap.dir-contexts."dir-contexts".security-protocol](#quarkus-camel-ldap-dir-contexts-dir-contexts-security-protocol)`

The security protocol to use. Its value is a string determined by the service provider (e.g. "ssl").

 | `string` |  |
| `[quarkus.camel.ldap.dir-contexts."dir-contexts".security-authentication](#quarkus-camel-ldap-dir-contexts-dir-contexts-security-authentication)`

The security level to use. Its value is one of the following strings: "none", "simple", "strong". If this property is unspecified, the behaviour is determined by the service provider.

 | `string` | `none` |
| `[quarkus.camel.ldap.dir-contexts."dir-contexts".socket-factory](#quarkus-camel-ldap-dir-contexts-dir-contexts-socket-factory)`

The custom socket factory to use. The value of the property should be the fully qualified class name of the socket factory class.

 | `string` |  |
| `[quarkus.camel.ldap.dir-contexts."dir-contexts".additional-options."additional-options"](#quarkus-camel-ldap-dir-contexts-dir-contexts-additional-options-additional-options)`

Any other option which will be used during dirContext creation.

 | `Map<String,String>` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.
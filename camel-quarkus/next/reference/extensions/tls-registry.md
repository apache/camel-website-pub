# TLS Registry

JVM since3.36.0 Native since3.36.0 🧪Experimental

Configuration bridge for the Quarkus TLS registry and Camel SSLContextParameters

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-tls-registry)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-tls-registry</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

This extension provides integration between [Quarkus TLS Registry](https://quarkus.io/guides/tls-registry-reference) and [Camel SSLContextParameters](../../../../manual/camel-configuration-utilities.md). When enabled, TLS configurations defined via `quarkus.tls.*` properties are automatically converted and registered as `SSLContextParameters` beans in the Camel registry.

This eliminates the need to configure TLS separately for Quarkus and Camel components - configure it once in Quarkus, and use it everywhere in your Camel routes.

### Basic Configuration

#### Default TLS Configuration

Configure a default TLS configuration using `quarkus.tls.*` properties:

```properties
# Default TLS configuration
quarkus.tls.key-store.p12.path=/etc/ssl/keystore.p12
quarkus.tls.key-store.p12.password=changeit
quarkus.tls.trust-store.p12.path=/etc/ssl/truststore.p12
quarkus.tls.trust-store.p12.password=changeit
```

This creates an `SSLContextParameters` bean named `defaultSslContextParameters` that can be referenced in your routes:

```java
from("timer:tick")
    .to("https://api.example.com?sslContextParameters=#defaultSslContextParameters");
```

> **Note**
> The bean name for the default TLS configuration can be customized using `quarkus.camel.tls-registry.default-bean-name`.

#### Named TLS Configurations

Define multiple named TLS configurations for different purposes (e.g., separate client and server certificates):

```properties
# Client TLS configuration
quarkus.tls.client.key-store.p12.path=/etc/ssl/client-keystore.p12
quarkus.tls.client.key-store.p12.password=changeit
quarkus.tls.client.trust-all=true

# Server TLS configuration
quarkus.tls.server.key-store.p12.path=/etc/ssl/server-keystore.p12
quarkus.tls.server.key-store.p12.password=changeit
quarkus.tls.server.trust-store.p12.path=/etc/ssl/server-truststore.p12
```

Named configurations are automatically discovered and registered as beans with their configuration name:

```java
// Use the client certificate
from("timer:tick")
    .to("https://api.example.com?sslContextParameters=#client");

// Use the server certificate
from("netty-http:https://0.0.0.0:8443/secure?sslContextParameters=#server")
    .to("log:requests");
```

### Global SSL Context

You can set the Quarkus default TLS configuration as Camel’s global `SSLContextParameters`:

```properties
quarkus.camel.tls-registry.quarkus-default-as-global=true

# Default TLS configuration becomes global
quarkus.tls.key-store.p12.path=/etc/ssl/keystore.p12
quarkus.tls.key-store.p12.password=changeit
```

When configured as global, Camel components can opt in to using it automatically:

```java
from("timer:tick")
    // No need to specify sslContextParameters, uses global SSL context
    .to("https://api.example.com?useGlobalSslContextParameters=true");
```

### Certificate Reload

The extension automatically observes certificate reload events from Quarkus TLS registry. When certificates are reloaded (e.g., due to file system changes), the corresponding `SSLContextParameters` beans are updated and Camel routes are restarted to pick up the new certificates.

This feature is enabled by default but can be controlled via configuration:

```properties
# Enable certificate reloading
quarkus.tls.reload-period=1h

# Enable/disable certificate reload (default: true)
quarkus.camel.tls-registry.reload-on-certificate-update=true

# Debounce delay in milliseconds to avoid multiple reloads (default: 2000)
quarkus.camel.tls-registry.reload-certificate-delay=2000
```

The debounce delay ensures that when multiple certificates are updated in quick succession, only a single Camel context reload occurs after all updates have stabilized.

For more information see the [Quarkus TLS Registry Reference Guide](https://quarkus.io/guides/tls-registry-reference#reloading-certificates).

### Bean Name Conflicts

If you have an existing `SSLContextParameters` bean with the same name as a Quarkus TLS configuration, the extension will throw an `IllegalStateException` at startup with a helpful message.

To resolve this, you can either:

1.  Remove or rename the existing `SSLContextParameters` bean, or
    
2.  Rename the Quarkus TLS configuration (e.g., `quarkus.tls.my-config.*` instead of the conflicting name)
    

### PEM Format Support

Quarkus TLS registry supports both PKCS12 and PEM formats. The extension automatically works with both:

```properties
# PEM format
quarkus.tls.key-store.pem.cert=/etc/ssl/cert.pem
quarkus.tls.key-store.pem.key=/etc/ssl/key.pem
quarkus.tls.trust-store.pem.certs=/etc/ssl/ca-bundle.pem

# Or PKCS12 format
quarkus.tls.key-store.p12.path=/etc/ssl/keystore.p12
quarkus.tls.key-store.p12.password=changeit
```

### Additional Resources

-   [Quarkus TLS Registry Reference Guide](https://quarkus.io/guides/tls-registry-reference)
    
-   [Camel SSLContextParameters Documentation](../../../../manual/camel-configuration-utilities.md)
    

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.tls-registry.enabled](#quarkus-camel-tls-registry-enabled)`
Enable automatic conversion and registration of Quarkus TLS configurations as Camel SSLContextParameters beans.

When enabled, the default TLS configuration and any named configurations will be automatically discovered and registered as beans in the Camel registry.

 | `boolean` | `true` |
| `[quarkus.camel.tls-registry.quarkus-default-as-global](#quarkus-camel-tls-registry-quarkus-default-as-global)`

Whether to set the Quarkus default TLS configuration as Camel’s global SSLContextParameters.

When true, if a default TLS configuration exists (`quarkus.tls.*`), it will be converted and set as the global SSL context via `CamelContext.setSSLContextParameters()`. Components can opt in to this global context using `useGlobalSslContextParameters=true`.

 | `boolean` | `false` |
| `[quarkus.camel.tls-registry.default-bean-name](#quarkus-camel-tls-registry-default-bean-name)`

The name to use when registering the default TLS configuration as a bean.

Only applicable if the default configuration is not set as global (i.e., `quarkus-default-as-global=false`).

 | `string` | `defaultSslContextParameters` |
| `[quarkus.camel.tls-registry.reload-on-certificate-update](#quarkus-camel-tls-registry-reload-on-certificate-update)`

Enable automatic Camel Context reload when certificates are updated.

When enabled, if Quarkus reloads a certificate (e.g., file watch detects changes), the corresponding SSLContextParameters bean will be updated in the Camel registry and a context reload will be triggered to restart routes with the new certificates.

This uses Camel’s `ContextReloadStrategy` to gracefully restart routes without stopping the entire application.

To avoid excessive reloads when multiple certificates are updated in quick succession, the reload is debounced with a configurable delay. If additional certificate updates occur during this delay, the timer is reset, ensuring only one reload happens after all updates have stabilized.

 | `boolean` | `true` |
| `[quarkus.camel.tls-registry.reload-certificate-delay](#quarkus-camel-tls-registry-reload-certificate-delay)`

Delay period to avoid excessive Camel Context reloads when multiple certificates are updated in quick succession.

 | `long` | `2000` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.
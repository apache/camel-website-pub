# Jolokia

JVM since3.19.0 Native since3.20.0

Expose runtime metrics and management operations via JMX with Jolokia

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jolokia)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jolokia</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

This extension adds [Jolokia](https://jolokia.org/) support to your application.

### Jolokia HTTP endpoints

In prod mode, Jolokia is accessible at the following URLs.

-   [http://0.0.0.0:8778/jolokia/](http://0.0.0.0:8778/jolokia/)
    

In dev and test modes Jolokia is bound only to `localhost`.

If you want to disable Jolokia entirely, then add the following configuration to `application.properties`.

```none
quarkus.camel.jolokia.enabled=false
```

### Jolokia configuration

Any of the [Jolokia configuration options](https://jolokia.org/reference/html/manual/agents.md) can be configured via the `quarkus.camel.jolokia.additional-properties.<jolokia-property-name>` option. Where `<jolokia-property-name>` is the name of the Jolokia configuration option you want to set.

For example, the following configuration added to `application.properties` enables Jolokia debugging and sets the max depth for traversing bean properties.

```none
quarkus.camel.jolokia.additional-properties.debug=true
quarkus.camel.jolokia.additional-properties.maxDepth=10
```

### Jolokia restrictor

By default, a Jolokia restrictor is automatically registered that exposes access to only a specific set of MBean domains.

-   `org.apache.camel`
    
-   `java.lang`
    
-   `java.nio`
    

If this is too restrictive, then you can either specify your own MBean domains, disable the default restrictor, or create a custom restrictor.

#### Default restrictor MBean domains

You can modify the set of MBean domains referenced by the default restrictor by adding configuration like the following to `application.properties`.

```none
quarkus.camel.jolokia.camel-restrictor-allowed-mbean-domains=org.apache.camel
```

#### Disabling the default restrictor

The following configuration added to `application.properties` disables the default restrictor.

```none
quarkus.camel.jolokia.register-camel-restrictor=false
```

#### Create a custom restrictor

You can create your own restrictor class and register it with Jolokia.

```java
public class CustomRestrictor extends AllowAllRestrictor {
    // Override methods to apply custom restrictions
}
```

Register the restrictor with Jolokia by adding the following configuration to `application.properties`.

```none
quarkus.camel.jolokia.additional-properties.restrictorClass=org.acme.CustomRestrictor
```

### Kubernetes & OpenShift support

#### Generated Kubernetes manifests

If the `quarkus-kubernetes` or `quarkus-openshift` extensions are present, a container port named `jolokia` will be added automatically to the pod configuration within the generated Kubernetes manifest resources.

This can be disabled by adding the following configuration to `application.properties`.

```none
quarkus.camel.jolokia.kubernetes.expose-container-port=false
```

#### Automatic enablement of SSL client authentication

If the application detects that it is running on Kubernetes or OpenShift, then Jolokia is automatically configured for SSL client authentication. This is useful if you use tools like [Hawtio](https://hawt.io/) to discover and connect to your running application pod.

This functionality can be disabled by adding the following configuration to `application.properties`.

```none
quarkus.camel.jolokia.kubernetes.client-authentication-enabled=false
```

Note that if you choose to use [hawtio-online](https://github.com/hawtio/hawtio-online) to connect to your running application, then you must configure the Jolokia client principal.

```none
quarkus.camel.jolokia.kubernetes.client-principal=cn=hawtio-online.hawtio.svc
```

## Camel Quarkus limitations

### Native mode limitations

JMX in GraalVM is still **experimental**. Therefore, some features are not available in native mode.

Refer to the Camel Quarkus Management extension [limitations](management.html#extensions-management-limitations-native-mode) section for more details.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.jolokia.enabled](#quarkus-camel-jolokia-enabled)`
Enables Jolokia support.

 | `boolean` | `true` |
| `[quarkus.camel.jolokia.path](#quarkus-camel-jolokia-path)`

The context path that the Jolokia agent is deployed under.

 | `string` | `jolokia` |
| `[quarkus.camel.jolokia.camel-restrictor-allowed-mbean-domains](#quarkus-camel-jolokia-camel-restrictor-allowed-mbean-domains)`

Comma separated list of allowed MBean domains used by `CamelJolokiaRestrictor`.

 | List of `string` | `org.apache.camel,java.lang,java.nio` |
| `[quarkus.camel.jolokia.kubernetes.expose-container-port](#quarkus-camel-jolokia-kubernetes-expose-container-port)`

When `true` and the quarkus-kubernetes extension is present, a container port named jolokia will be added to the generated Kubernetes manifests within the container spec ports definition.

 | `boolean` | `true` |
| `[quarkus.camel.jolokia.server.auto-start](#quarkus-camel-jolokia-server-auto-start)`

Whether the Jolokia agent HTTP server should be started automatically. When set to `false`, it is the user responsibility to start the server. This can be done via `@Inject CamelQuarkusJolokiaServer` and then invoking the `start()` method.

 | `boolean` | `true` |
| `[quarkus.camel.jolokia.server.host](#quarkus-camel-jolokia-server-host)`

The host address to which the Jolokia agent HTTP server should bind. When unspecified, the default is localhost for dev and test mode. In prod mode the default is to bind to all interfaces at 0.0.0.0.

 | `string` |  |
| `[quarkus.camel.jolokia.server.port](#quarkus-camel-jolokia-server-port)`

The port on which the Jolokia agent HTTP server should listen.

 | `int` | `8778` |
| `[quarkus.camel.jolokia.server.discovery-enabled-mode](#quarkus-camel-jolokia-server-discovery-enabled-mode)`

The mode in which Jolokia agent discovery is enabled. The default `dev-test`, enables discovery only in dev and test modes. A value of `all` enables agent discovery in dev, test and prod modes. Setting the value to `none` will disable agent discovery in all modes.

 | `all`, `dev-test`, `none` | `dev-test` |
| `[quarkus.camel.jolokia.kubernetes.client-authentication-enabled](#quarkus-camel-jolokia-kubernetes-client-authentication-enabled)`

Whether to enable Jolokia SSL client authentication in Kubernetes environments. Useful for tools such as hawtio to be able to connect with your application.

 | `boolean` | `true` |
| `[quarkus.camel.jolokia.kubernetes.service-ca-cert](#quarkus-camel-jolokia-kubernetes-service-ca-cert)`

Absolute path of the CA certificate Jolokia should use for SSL client authentication.

 | [`File`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/File.md) | `/var/run/secrets/kubernetes.io/serviceaccount/service-ca.crt` |
| `[quarkus.camel.jolokia.kubernetes.client-principal](#quarkus-camel-jolokia-kubernetes-client-principal)`

The principal which must be given in a client certificate to allow access to Jolokia.

 | `string` |  |
| `[quarkus.camel.jolokia.additional-properties."additional-properties"](#quarkus-camel-jolokia-additional-properties-additional-properties)`

Arbitrary Jolokia configuration options. These are described at the [Jolokia documentation](https://jolokia.org/reference/html/manual/agents.md). Options can be configured like `quarkus.camel.jolokia.additional-properties."debug"=true`.

 | `Map<String,String>` |  |
| `[quarkus.camel.jolokia.register-camel-restrictor](#quarkus-camel-jolokia-register-camel-restrictor)`

When `true`, a Jolokia restrictor is registered that limits MBean read, write and operation execution to the following MBean domains.

-   org.apache.camel
    
-   java.lang
    
-   java.nio
    

Note that this option has no effect if `quarkus.camel.jolokia.additional-properties."restrictorClass"` is set.

 | `boolean` | `true` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.
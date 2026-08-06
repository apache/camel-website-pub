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

Jolokia is accessible at the following URL.

-   [http://localhost:8778/jolokia/](http://localhost:8778/jolokia/)
    

By default, the Jolokia agent HTTP server binds to `localhost`. Remote dev mode and WSL environments default to `0.0.0.0`.

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

You can create your own restrictor class and register it with Jolokia. Extending `CamelJolokiaRestrictor` inherits the secure defaults (remote access control, CORS blocking, MBean domain filtering).

```java
public class CustomRestrictor extends CamelJolokiaRestrictor {
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

#### Configuring Jolokia for remote management tools

Tools such as [Hawtio](https://hawt.io/) and [hawtio-online](https://github.com/hawtio/hawtio-online) connect to Jolokia via the pod IP address, which is a non-loopback address. By default, the Jolokia agent binds to `localhost` and the default restrictor blocks connections from non-loopback addresses.

To allow remote management tools to connect to Jolokia in Kubernetes, add the following configuration to `application.properties`.

```none
quarkus.camel.jolokia.server.host=0.0.0.0
quarkus.camel.jolokia.remote-access-allowed=true
```

This is safe when combined with SSL client authentication (enabled by default in Kubernetes), which ensures that only clients presenting a valid certificate signed by the service CA can connect. If you use hawtio-online, you must also configure the Jolokia client principal.

```none
quarkus.camel.jolokia.kubernetes.client-principal=cn=hawtio-online.hawtio.svc
```

### Security

> **Note**
> Even when bound to `localhost`, Jolokia does not require authentication by default. On shared hosts or in container environments where localhost may be reachable from other containers, consider using a custom restrictor or Jolokia access policy to restrict access further.

#### Network binding

By default, the Jolokia agent HTTP server binds to `localhost`, making it accessible only from the local machine. If you need to expose Jolokia to remote hosts, you must explicitly configure the bind address and enable remote access.

```none
quarkus.camel.jolokia.server.host=0.0.0.0
quarkus.camel.jolokia.remote-access-allowed=true
```

#### Remote access control

The default Camel Jolokia restrictor blocks connections from non-loopback addresses. This is controlled by the `quarkus.camel.jolokia.remote-access-allowed` property (default `false`). When set to `false`, only connections from loopback addresses (e.g. `127.0.0.1`, `::1`) are accepted, regardless of the server bind address.

#### Cross-origin requests (CORS)

The default Camel Jolokia restrictor denies all cross-origin requests. If you need to allow specific origins (e.g. for a browser-based monitoring tool connecting cross-origin), you can use a [Jolokia access policy](https://jolokia.org/reference/html/manual/security.md) (`jolokia-access.xml`) with a `<cors>` section, or configure a custom restrictor that overrides `isOriginAllowed()`.

#### Jolokia access policy

Jolokia supports fine-grained access control via an XML policy file (`jolokia-access.xml`). This can restrict access by IP address, CORS origin, HTTP method, and MBean operation.

The default Camel restrictor automatically loads `jolokia-access.xml` from the classpath if present. Place the file in `src/main/resources/jolokia-access.xml` to use it alongside the Camel restrictor. The Camel restrictor always allows loopback connections. For non-loopback requests, it delegates remote access, CORS, allowed request types (`<commands>`), and HTTP method (`<http>`) checks to the policy file, while continuing to enforce MBean domain filtering.

For example, the following `jolokia-access.xml` allows access from the `10.0.0.0/8` subnet, CORS requests from a monitoring tool, and restricts Jolokia to read-only operations over HTTP GET.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<restrict>
    <remote>
        <host>10.0.0.0/8</host>
    </remote>
    <cors>
        <allow-origin>http://monitoring.example.com</allow-origin>
    </cors>
    <commands>
        <command>read</command>
        <command>list</command>
        <command>version</command>
        <command>search</command>
    </commands>
    <http>
        <method>get</method>
    </http>
</restrict>
```

Refer to the [Jolokia security documentation](https://jolokia.org/reference/html/manual/security.md) for the full policy file format.

To load the policy file from a different location, such as a file path mounted from a Kubernetes ConfigMap, configure the `policyLocation` property.

```none
quarkus.camel.jolokia.additional-properties."policyLocation"=file:/etc/jolokia/jolokia-access.xml
```

As an alternative, you can disable the default Camel restrictor entirely and let Jolokia manage the policy file directly. This gives full control to `jolokia-access.xml` (including MBean-level rules) but loses the Camel MBean domain filtering.

```none
quarkus.camel.jolokia.register-camel-restrictor=false
```

If you are building a native executable, the policy file must be explicitly included as a native resource.

```none
quarkus.native.resources.includes=jolokia-access.xml
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

The host address to which the Jolokia agent HTTP server should bind. When unspecified, the default is localhost in all modes except remote dev, where it defaults to 0.0.0.0.

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
| `[quarkus.camel.jolokia.remote-access-allowed](#quarkus-camel-jolokia-remote-access-allowed)`

When `true`, the default Camel Jolokia restrictor allows connections from non-loopback (remote) addresses. When `false` (the default), only connections from loopback addresses (e.g. 127.0.0.1, ::1) are permitted. This provides defense-in-depth: even if the server host is configured to bind to all interfaces, remote requests are rejected unless this property is explicitly set to `true`.

This option only takes effect when `register-camel-restrictor` is `true` and a custom restrictor class is not configured via `quarkus.camel.jolokia.additional-properties."restrictorClass"`.

 | `boolean` | `false` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.
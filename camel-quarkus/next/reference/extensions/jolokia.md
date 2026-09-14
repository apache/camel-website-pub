Camel Quarkus

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

Jolokia is accessible at [http://localhost:8778/jolokia/](http://localhost:8778/jolokia/).

The agent HTTP server binds to `localhost`, except in remote dev mode, in dev and test mode on WSL, and on Kubernetes with [SSL client authentication](#extensions-jolokia-usage-ssl-client-authentication) configured, where it binds to `0.0.0.0`.

> **Note**
> Binding `0.0.0.0` in remote dev mode, and on WSL, does not on its own allow remote clients. Client addresses are restricted to loopback in every mode, so reaching the agent from another host also needs `quarkus.camel.jolokia.remote-access-allowed=true`. See [Allowing remote clients](#extensions-jolokia-usage-allowing-remote-clients).

To disable Jolokia entirely, add the following to `application.properties`.

```none
quarkus.camel.jolokia.enabled=false
```

### Jolokia configuration

Any of the [Jolokia configuration options](https://jolokia.org/reference/html/manual/agents.md) can be set via `quarkus.camel.jolokia.additional-properties.<jolokia-property-name>`.

For example, to enable Jolokia debugging and set the max depth for traversing bean properties.

```none
quarkus.camel.jolokia.additional-properties.debug=true
quarkus.camel.jolokia.additional-properties.maxDepth=10
```

## Security

By default, Jolokia is reachable only from the machine the application runs on, and exposes only Camel and JVM MBeans. The defaults are applied by `CamelJolokiaRestrictor`, which is registered automatically.

  
|  | Default | Configured by |
| --- | --- | --- |
| Bind address | `localhost`, or `0.0.0.0` on Kubernetes with SSL client authentication | `quarkus.camel.jolokia.server.host` |
| Client addresses | Loopback addresses only, such as `127.0.0.1` and `::1`, regardless of the bind address. Lifted on Kubernetes with SSL client authentication, which authenticates every client | `quarkus.camel.jolokia.remote-access-allowed` |
| Cross-origin requests | Denied, except loopback origins and requests carrying no `Origin` header. Lifted on Kubernetes when `kubernetes.client-principal` is set and no origins are listed here | `quarkus.camel.jolokia.allowed-origins` |
| MBean domains | `org.apache.camel`, `java.lang`, `java.nio` | `quarkus.camel.jolokia.camel-restrictor-allowed-mbean-domains` |

### Authentication

Jolokia can require HTTP basic authentication. It is off by default and is configured through the agent’s own options.

```none
quarkus.camel.jolokia.additional-properties.authMode=basic
quarkus.camel.jolokia.additional-properties.user=jolokia
quarkus.camel.jolokia.additional-properties.password=${JOLOKIA_PASSWORD}
```

> **Important**
> Basic authentication sends the password on every request, so serve the agent over HTTPS or keep it off untrusted networks. On Kubernetes and OpenShift, [SSL client authentication](#extensions-jolokia-usage-ssl-client-authentication) is the better option and is already enabled by default.

### Allowing remote clients

To reach the agent from another host, open up both the bind address and remote access.

```none
quarkus.camel.jolokia.server.host=0.0.0.0
quarkus.camel.jolokia.remote-access-allowed=true
```

This opens up client addresses only. Cross-origin requests remain restricted, so a browser based console needs its origin listed as well. See [Allowing cross-origin requests](#extensions-jolokia-usage-allowing-cross-origin-requests).

A reverse proxy in front of the agent needs this too, even on the same host, since the client address it forwards is not a loopback address.

> **Note**
> Turning on `quarkus.camel.jolokia.additional-properties.allowDnsReverseLookup`, which Jolokia leaves off, adds the name the client address resolves back to. A host whose loopback address resolves to something other than `localhost` then refuses local clients too, answering `No access from client [chain: myhost → 127.0.0.1] allowed`. Allow the name through the `<remote>` section of an [access policy](#extensions-jolokia-usage-access-policy-files).

> **Important**
> This exposes an agent that authenticates nobody. Anyone who can reach it gets full access to the allowed MBean domains, which by default means invoking Camel management operations such as `sendStringBody`, which sends a message to any endpoint the application can resolve, and stopping the `CamelContext`. Confine the agent to a trusted network, or configure [authentication](#extensions-jolokia-usage-authentication).

### Allowing cross-origin requests

To let a browser based tool such as [Hawtio](https://hawt.io/) drive the agent, list its origin.

```none
quarkus.camel.jolokia.allowed-origins=https://hawtio.example.com
```

Matching is case insensitive, and `*` is a wildcard, exactly as in the `<allow-origin>` rules of a Jolokia access policy. So a whole domain can be covered in one entry.

```none
quarkus.camel.jolokia.allowed-origins=*://*.example.com
```

A value of `*` on its own accepts any origin.

Each value is matched against the scheme, host and port of the request origin, so a path or query in the entry never matches. A port that is the default for the scheme is optional, so `[https://hawtio.example.com](https://hawtio.example.com)` and `[https://hawtio.example.com:443](https://hawtio.example.com:443)` are interchangeable. Any other port has to be listed, since `[https://hawtio.example.com:8443](https://hawtio.example.com:8443)` is a different origin. An internationalised host has to be listed in its punycode form, such as `[https://xn—​e1afmkfd.example](https://xn—​e1afmkfd.example)`, since that is what a browser sends. A host containing an underscore cannot be matched at all, as it is not a valid host name, so such an origin is always refused.

Loopback origins are always accepted, so that a console on the same machine needs no configuration. That still applies once `quarkus.camel.jolokia.remote-access-allowed` has opened the agent to other hosts, so a page served from `localhost` in any browser that can reach the agent is accepted as well.

> **Important**
> This property is the only way to allow an origin. The `<cors>` section of a `jolokia-access.xml` access policy is **not** used at all. If you are bringing an existing policy file, copy its `<allow-origin>` values here unchanged, replace `<ignore-scheme/>` with `quarkus.camel.jolokia.ignore-origin-scheme=true`, and delete the section.

#### Requests with no origin

A request carrying neither an `Origin` nor a `Referer` header is accepted, so that command line clients such as `curl` keep working. There is no equivalent of the `<strict-checking/>` element of an access policy to turn that off.

Browsers are stopped from exploiting this by Jolokia’s handling of the `Sec-Fetch-*` headers, which refuses anything a browser marks as other than an explicit top-level navigation. Leave that in place.

```none
# Do not do this
quarkus.camel.jolokia.additional-properties.useFetchMetadata=false
```

#### HTTPS origins and a plain HTTP agent

Jolokia refuses a request whose `Origin` uses `https` when the agent itself serves plain `http`, responding with a status of `403`, whatever `allowed-origins` lists.

Either serve the agent over HTTPS, or turn the check off.

```none
quarkus.camel.jolokia.ignore-origin-scheme=true
```

> **Warning**
> Only do this where something in front of the agent terminates TLS. Otherwise, a page loaded over HTTPS ends up driving an agent that is not.

This does not arise where [SSL client authentication](#extensions-jolokia-usage-ssl-client-authentication) is configured, since the agent then serves HTTPS.

### MBean domains

The restrictor hides MBeans outside the allowed domains, and denies reads, writes and operations against them. Adjust the set as needed.

```none
quarkus.camel.jolokia.camel-restrictor-allowed-mbean-domains=org.apache.camel,java.lang
```

### Access policy files

Jolokia supports fine grained access control via an XML policy file, which can restrict access by IP address, HTTP method, request type and MBean operation. Refer to the [Jolokia security documentation](https://jolokia.org/reference/html/manual/security.md) for the full format.

Place the file at `src/main/resources/jolokia-access.xml` and it is picked up automatically. For example, the following policy allows the `10.0.0.0/8` subnet and restricts Jolokia to read-only operations over HTTP GET.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<restrict>
    <remote>
        <host>10.0.0.0/8</host>
    </remote>
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

To load the policy from elsewhere, such as a file mounted from a Kubernetes ConfigMap, set `policyLocation`.

```none
quarkus.camel.jolokia.additional-properties."policyLocation"=file:/etc/jolokia/jolokia-access.xml
```

#### How a policy combines with the restrictor

The policy’s `<remote>`, `<commands>`, `<http>` and MBean level rules (`<allow>`, `<deny>`, `<filter>`) all apply. MBean domain filtering applies on top of them.

-   A `<remote>` section decides client addresses. `quarkus.camel.jolokia.remote-access-allowed` and the loopback default no longer apply, so a `<remote>` section that does not list `127.0.0.1` refuses local clients too.
    
-   A policy with no `<remote>` section says nothing about addresses, so the loopback default and `quarkus.camel.jolokia.remote-access-allowed` still decide them. A `<remote>` section listing `0.0.0.0/0` is read the same way, since it grants no more than saying nothing does.
    
-   The `<cors>` section is not consulted at all. Use `quarkus.camel.jolokia.allowed-origins` in place of `<allow-origin>`, and `quarkus.camel.jolokia.ignore-origin-scheme` in place of `<ignore-scheme/>`. `<strict-checking/>` has no equivalent.
    
-   Where a proxy forwards the client address in a `Forwarded`, `X-Forwarded-For` or `X-Real-IP` header, `<remote>` has to allow that address as well. Hawtio forwards the browser address by default.
    

#### Loading failures

A `policyLocation` that is configured but points at nothing fails the application at startup. This covers a `classpath:` location that was not packaged, and a `file:` location that is not there, such as a ConfigMap that failed to mount.

A policy that is found but cannot be read or parsed denies all Jolokia access and logs an error.

In native mode, a policy at the default `jolokia-access.xml` location is registered as a resource automatically. A policy loaded from any other `classpath:` location must be registered by your application.

```none
quarkus.native.resources.includes=my-jolokia-access.xml
```

### Custom restrictors

Extending `CamelJolokiaRestrictor` inherits the secure defaults described above, including access policy handling.

The access checks are `final`. A subclass adds restrictions through the `allows*` hooks, which are called only once the inherited checks have allowed the request.

```java
public class CustomRestrictor extends CamelJolokiaRestrictor {
    @Override
    protected boolean allowsOperation(ObjectName objectName, String operation) {
        return operation.startsWith("dump");
    }
}
```

Each hook returns `true` to keep the inherited decision and `false` to refuse, so a subclass can only narrow what the defaults permit.

 
| Hook | Narrows |
| --- | --- |
| `allowsRemoteAccess(String…​)` | Which client addresses may reach the agent |
| `allowsOrigin(String, boolean)` | Which origins may reach the agent |
| `allowsHttpMethod(HttpMethod)` | Which HTTP methods may be used |
| `allowsRequestType(RequestType)` | Which Jolokia request types may be used |
| `allowsAttributeRead(ObjectName, String)` | Which attributes may be read |
| `allowsAttributeWrite(ObjectName, String)` | Which attributes may be written |
| `allowsOperation(ObjectName, String)` | Which operations may be invoked |
| `allowsObjectName(ObjectName)` | Which MBeans are listed |

`isAllowedDomain(ObjectName)` is `protected`, for a hook that needs the domain restriction. The inherited checks apply it already.

To grant access, use the configuration options above. Implementing Jolokia’s `Restrictor` interface directly replaces these decisions and inherits none of the defaults.

```none
quarkus.camel.jolokia.additional-properties.restrictorClass=org.acme.CustomRestrictor
```

Alternatively, disabling the Camel restrictor hands full control to `jolokia-access.xml`, including its `<cors>` section and MBean level rules, but loses MBean domain filtering and every property described above.

```none
quarkus.camel.jolokia.register-camel-restrictor=false
```

> **Warning**
> With no restrictor and no access policy, Jolokia is unrestricted.

## Kubernetes & OpenShift

### Generated Kubernetes manifests

If the `quarkus-kubernetes` or `quarkus-openshift` extensions are present, a production build adds a container port named `jolokia` to the container spec of the generated manifests. To disable this.

```none
quarkus.camel.jolokia.kubernetes.expose-container-port=false
```

### SSL client authentication

On Kubernetes and OpenShift, Jolokia is configured for SSL client authentication wherever the service CA certificate is present, so that only clients presenting a certificate signed by it can connect. This is the default on OpenShift.

Because every client is then authenticated by the transport, the agent binds `0.0.0.0` rather than `localhost` and the loopback restriction on client addresses does not apply.

The certificate is checked against the service CA only, so unless a client principal is configured, any client holding a certificate the CA happened to sign is accepted. Restrict this to a specific service identity.

```none
quarkus.camel.jolokia.kubernetes.client-principal=cn=hawtio-online.hawtio.svc
```

Once a client principal is set, the authenticated peer is a known identity rather than any certificate holder, so cross-origin requests it forwards are accepted and [`allowed-origins`](#extensions-jolokia-usage-allowing-cross-origin-requests) does not have to list the console. Setting `allowed-origins` anyway still takes effect, being the more specific instruction.

> **Note**
> Only `quarkus.camel.jolokia.kubernetes.client-principal` accepts those cross-origin requests. Jolokia reads the same value from a `clientPrincipal` option, and from `clientPrincipal.1`, `clientPrincipal.2` and so on for several identities, either of which can be set through `quarkus.camel.jolokia.additional-properties`. Both restrict which certificate is accepted, but the restrictor does not read them, so cross-origin requests stay restricted. The `Origins:` value in the Jolokia line logged at startup shows which applies.

Without a client principal, cross-origin requests remain restricted to loopback origins and whatever `allowed-origins` lists. A startup warning says so.

To disable SSL client authentication entirely.

```none
quarkus.camel.jolokia.kubernetes.client-authentication-enabled=false
```

> **Warning**
> Disabling it opts out of the only thing authenticating clients. The agent then falls back to binding `localhost` and accepting loopback clients only, exactly as it does off Kubernetes. Opening it up again with `server.host` and `remote-access-allowed` would expose an unauthenticated agent to the pod network.

> **Note**
> The default `service-ca-cert` path is written by the OpenShift service CA operator and is absent on vanilla Kubernetes, where none of the above applies unless `quarkus.camel.jolokia.kubernetes.service-ca-cert` is pointed at a CA certificate you mount yourself.

Where client authentication is enabled but not in effect, because the certificate is absent or `additional-properties` overrode one of the options it is made of, the application fails to start unless the agent is bound to `localhost`. Mount a certificate, bind to `localhost`, or set `client-authentication-enabled=false`.

## Hawtio & Hawtio Online

[Hawtio](https://hawt.io/) and [Hawtio Online](https://github.com/hawtio/hawtio-online) proxy browser requests to the agent, forwarding the browser `Origin` header and adding the browser address as `X-Forwarded-For`.

Hawtio running on the same machine as the application needs no configuration. Both the origin it forwards and the address it adds are loopback, so the defaults accept them. Everything below concerns reaching an agent on another host, which is how Hawtio Online always connects, via the pod IP address.

Hawtio lists MBeans beyond those of Camel and the JVM. Add any other domain it should show, such as `org.apache.activemq.artemis`, to [`camel-restrictor-allowed-mbean-domains`](#extensions-jolokia-usage-mbean-domains).

### On Kubernetes & OpenShift

[SSL client authentication](#extensions-jolokia-usage-ssl-client-authentication) already covers the bind address, the client addresses and, once the client principal is pinned, the console origin. A deployment following the Hawtio Online instructions therefore needs one property.

```none
quarkus.camel.jolokia.kubernetes.client-principal=cn=hawtio-online.hawtio.svc
```

This is the subject of the client certificate Hawtio Online presents, which its `generate-proxying.sh` issues with a CN of `hawtio-online.hawtio.svc` by default, where `hawtio` is the namespace. Adjust it if the certificate was generated with a different CN or namespace.

To restrict which console origins are accepted on top of that, list them.

```none
quarkus.camel.jolokia.allowed-origins=https://hawtio-online.apps.example.com
```

The origin to list is the address the browser uses for the Hawtio console, not the address of the agent.

### Anywhere else

With nothing authenticating clients, the agent has to be opened up explicitly.

```none
quarkus.camel.jolokia.server.host=0.0.0.0
quarkus.camel.jolokia.remote-access-allowed=true
quarkus.camel.jolokia.allowed-origins=https://hawtio.example.com
```

On plain Kubernetes, add `quarkus.camel.jolokia.kubernetes.client-authentication-enabled=false` as well. SSL client authentication is enabled by default and cannot be configured there, so binding to a non-loopback address otherwise fails at startup.

The agent serves plain HTTP here, so an `https` console origin is refused whatever `allowed-origins` lists. See [HTTPS origins and a plain HTTP agent](#extensions-jolokia-usage-https-origins-and-a-plain-http-agent).

## Camel Quarkus limitations

### Native mode limitations

JMX in GraalVM is still **experimental**. Therefore, some features are not available in native mode.

Refer to the Camel Quarkus Management extension [limitations](management.html#extensions-management-limitations-native-mode) section for more details.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).

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

The host address to which the Jolokia agent HTTP server should bind. When unspecified, the default is localhost, except in remote dev mode, in dev and test mode on WSL, and on Kubernetes with SSL client authentication configured, where it defaults to 0.0.0.0.

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

The principal which must be given in a client certificate to allow access to Jolokia. For example `cn=hawtio-online.hawtio.svc`.

Without it, any client holding a certificate signed by the service CA is accepted. Setting it also lets the default Camel Jolokia restrictor accept cross-origin requests forwarded by that client, since the authenticated peer is then a known identity.

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

When `true`, the default Camel Jolokia restrictor allows connections from non-loopback (remote) addresses. When `false` (the default), only connections from loopback addresses (e.g. 127.0.0.1, ::1) are permitted.

This controls client addresses only. Cross-origin requests remain restricted to loopback origins and whatever `quarkus.camel.jolokia.allowed-origins` lists.

This option only takes effect when `register-camel-restrictor` is `true` and a custom restrictor class is not configured via `quarkus.camel.jolokia.additional-properties."restrictorClass"`. It is ignored when a Jolokia access policy (`jolokia-access.xml`) carries a `<remote>` section, since that section decides client addresses outright. A policy with no `<remote>` section says nothing about addresses, so this option still applies.

It is not needed on Kubernetes when `quarkus.camel.jolokia.kubernetes.client-authentication-enabled` is `true` and the service CA certificate is present, since SSL client authentication then authenticates every client and non-loopback addresses are already accepted.

 | `boolean` | `false` |
| `[quarkus.camel.jolokia.allowed-origins](#quarkus-camel-jolokia-allowed-origins)`

Origins from which the default Camel Jolokia restrictor accepts cross-origin requests, in addition to loopback origins and requests that carry no `Origin` header. That loopback exception still applies once `quarkus.camel.jolokia.remote-access-allowed` has opened the agent to clients on other hosts.

Each value is matched against the scheme, host and port of the request `Origin` header, for example `[https://myhost.example.com](https://myhost.example.com)`. A port that is the default for the scheme is optional. Matching is case-insensitive and **is a wildcard, as in the `<allow-origin>` rules of a Jolokia access policy, so** `://**.example.com**` **covers a whole domain and** on its own accepts any origin.

Jolokia falls back to the `Referer` header when a request carries no `Origin`. Such a value is reduced to its origin before being matched, so only the origin needs listing.

This is the only way to allow an origin. The `<cors>` section of a Jolokia access policy (`jolokia-access.xml`) is not used, though `<allow-origin>` values can be copied here unchanged and `<ignore-scheme/>` has an equivalent in `quarkus.camel.jolokia.ignore-origin-scheme`. The rest of a policy is applied as normal.

Note that Jolokia itself rejects a request whose `Origin` uses `https` when the agent is serving plain `http`, whatever this option is set to.

On Kubernetes, cross-origin requests are accepted without this option once `quarkus.camel.jolokia.kubernetes.client-principal` pins which client identity may connect. Setting it anyway restores the origin check, since an explicit list is the more specific instruction.

This option only takes effect when `register-camel-restrictor` is `true` and a custom restrictor class is not configured via `quarkus.camel.jolokia.additional-properties."restrictorClass"`.

 | List of `string` |  |
| `[quarkus.camel.jolokia.ignore-origin-scheme](#quarkus-camel-jolokia-ignore-origin-scheme)`

When `true`, Jolokia stops refusing a request whose `Origin` uses `https` while the agent itself serves plain `http`. That rule applies whatever `quarkus.camel.jolokia.allowed-origins` lists.

Enable it only where the agent sits behind something that terminates TLS, since it otherwise allows a page loaded over HTTPS to be served by an agent that is not.

This is the equivalent of `<ignore-scheme/>` in the `<cors>` section of a Jolokia access policy, which is not consulted.

This option only takes effect when `register-camel-restrictor` is `true` and a custom restrictor class is not configured via `quarkus.camel.jolokia.additional-properties."restrictorClass"`.

 | `boolean` | `false` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.
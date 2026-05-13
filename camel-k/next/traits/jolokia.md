# Jolokia Trait

Deprecated since2.8.0 The Jolokia trait activates and configures the Jolokia Java agent. This trait is useful to enable JMX access to Camel application. Make sure you have the right privileges to perform such an action on the cluster.

See [https://jolokia.org/reference/html/manual/agents.html](https://jolokia.org/reference/html/manual/agents.md)

> **Warning**
> The Jolokia trait is **deprecated** and will removed in future release versions: use `jvm.agents` configuration instead.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait jolokia.[key]=[value] --trait jolokia.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `jolokia.enabled` | `bool` | Can be used to enable or disable a trait. All traits share this common property. |
| `jolokia.CACert` | `string` | The PEM encoded CA certification file path, used to verify client certificates, applicable when `protocol` is `https` and `use-ssl-client-authentication` is `true` (default `/var/run/secrets/kubernetes.io/serviceaccount/service-ca.crt` for OpenShift). |
| `jolokia.clientPrincipal` | `[]string` | The principal(s) which must be given in a client certificate to allow access to the Jolokia endpoint, applicable when `protocol` is `https` and `use-ssl-client-authentication` is `true` (default `clientPrincipal=cn=system:master-proxy`, `cn=hawtio-online.hawtio.svc` and `cn=fuse-console.fuse.svc` for OpenShift). |
| `jolokia.discoveryEnabled` | `bool` | Listen for multicast requests (default `false`) |
| `jolokia.extendedClientCheck` | `bool` | Mandate the client certificate contains a client flag in the extended key usage section, applicable when `protocol` is `https` and `use-ssl-client-authentication` is `true` (default `true` for OpenShift). |
| `jolokia.host` | `string` | The Host address to which the Jolokia agent should bind to. If `"*"` or `"0.0.0.0"` is given, the servers binds to every network interface (default `"*"`). |
| `jolokia.password` | `string` | The password used for authentication, applicable when the `user` option is set. |
| `jolokia.port` | `int32` | The Jolokia endpoint port (default `8778`). |
| `jolokia.protocol` | `string` | The protocol to use, either `http` or `https` (default `https` for OpenShift) |
| `jolokia.user` | `string` | The user to be used for authentication |
| `jolokia.useSSLClientAuthentication` | `bool` | Whether client certificates should be used for authentication (default `true` for OpenShift). |
| `jolokia.options` | `[]string` | A list of additional Jolokia options as defined in [JVM agent configuration options](https://jolokia.org/reference/html/agents.html#agent-jvm-config) |
> **Note**
> the variable names are "snake case" if you’re using in `kamel` CLI, for example `trait.myParam` has to be translated as `-t trait.my-param`
# Gateway Trait

The Gateway trait can be used to expose the service associated with the Integration to the outside world with a Kubernetes Gateway API. The trait is in charge to automatically discover associate the Integration Service generated with a Gateway and an HTTPRoute resource (HTTP/HTTPS protocol only supported).

> **Note**
> if any other protocol is required, please create a request in order to develop it.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait gateway.[key]=[value] --trait gateway.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `gateway.enabled` | `bool` | Can be used to enable or disable a trait. All traits share this common property. |
| `gateway.class-name` | `string` | The class name to use for the gateway configuration. |
| `gateway.listeners` | `[]string` | The listeners in the format "port;protocol" (default, "8080;HTTP"). |
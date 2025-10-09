# Openapi Trait

Deprecated since2.5.0 The OpenAPI DSL trait is internally used to allow creating integrations from a OpenAPI specs.

> **Warning**
> The Openapi trait is **deprecated** and will removed in future release versions: use Camel REST contract first instead (see Camel core documentation).

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

> **Note**
> The openapi trait is a **platform trait** and cannot be disabled by the user.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait openapi.[key]=[value] --trait openapi.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `openapi.enabled` | `bool` | Deprecated: no longer in use. |
| `openapi.configmaps` | `[]string` | The configmaps holding the spec of the OpenAPI (compatible with > 3.0 spec only). |
# Pull Secret Trait

The Pull Secret trait sets a pull secret on the pod, to allow Kubernetes to retrieve the container image from an external registry.

It’s enabled by default whenever you configure authentication for an external container registry, so it assumes that external registries are private.

If your registry does not need authentication for pulling images, you can disable this trait.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait pull-secret.[key]=[value] --trait pull-secret.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `pull-secret.enabled` | `bool` | Can be used to enable or disable a trait. All traits share this common property. |
| `pull-secret.secret-name` | `string` | The pull secret name to set on the Pod. If left empty this is automatically taken from the platform registry configuration. |
| `pull-secret.image-puller-delegation` | `bool` | When using a global operator with a shared platform, this enables delegation of the `system:image-puller` cluster role on the operator namespace to the integration service account.
Deprecated: may be removed in future releases.

 |
| `pull-secret.auto` | `bool` | Automatically configures the platform registry secret on the pod if it is of type `kubernetes.io/dockerconfigjson`. |
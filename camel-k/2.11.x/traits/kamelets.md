# Kamelets Trait

The kamelets trait is a platform trait used to inject Kamelets into the integration runtime.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait kamelets.[key]=[value] --trait kamelets.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `kamelets.enabled` | `bool` | Can be used to enable or disable a trait. All traits share this common property. |
| `kamelets.auto` | `bool` | Automatically inject all referenced Kamelets and their default configuration (enabled by default) |
| `kamelets.list` | `string` | Comma separated list of Kamelet names to load into the current integration |
| `kamelets.mountPoint` | `string` | The directory where the application mounts and reads Kamelet spec (default `/etc/camel/kamelets`) |
> **Note**
> the variable names are "snake case" if you’re using in `kamel` CLI, for example `trait.myParam` has to be translated as `-t trait.my-param`
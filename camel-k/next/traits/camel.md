# Camel Trait

The Camel trait can be used to configure versions of Camel runtime and related libraries, it cannot be disabled.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

> **Note**
> The camel trait is a **platform trait** and cannot be disabled by the user.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait camel.[key]=[value] --trait camel.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `camel.enabled` | `bool` | Deprecated: no longer in use. |
| `camel.runtimeProvider` | `string` | The runtime provider to use for the integration. (Default, plain Quarkus). |
| `camel.runtimeVersion` | `string` | The runtime version to use for the integration. It overrides the default version set in the Integration Platform. You can use a fixed version (for example "3.2.3") or a semantic version (for example "3.x") which will try to resolve to the best matching Catalog existing on the cluster (Default, the one provided by the operator version). |
| `camel.properties` | `[]string` | A list of properties to be provided to the Integration runtime |
> **Note**
> the variable names are "snake case" if you’re using in `kamel` CLI, for example `trait.myParam` has to be translated as `-t trait.my-param`
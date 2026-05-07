# Environment Trait

The environment trait is used internally to inject standard environment variables in the integration container, such as `NAMESPACE`, `POD_NAME` and others.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

> **Note**
> The environment trait is a **platform trait** and cannot be disabled by the user.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait environment.[key]=[value] --trait environment.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `environment.enabled` | `bool` | Deprecated: no longer in use. |
| `environment.containerMeta` | `bool` | Enables injection of `NAMESPACE` and `POD_NAME` environment variables (default `true`) |
| `environment.httpProxy` | `bool` | Propagates the `HTTP_PROXY`, `HTTPS_PROXY` and `NO_PROXY` environment variables (default `true`) |
| `environment.vars` | `[]string` | A list of environment variables to be added to the integration container. The syntax is either VAR=VALUE or VAR=\[configmap|secret\]:name/key, where name represents the resource name, and key represents the resource key to be mapped as and environment variable. These take precedence over any previously defined environment variables. |
> **Note**
> the variables names are "snake case" if you’re using in `kamel` CLI, for example `trait.myParam` has to be translated as `-t trait.my-param`
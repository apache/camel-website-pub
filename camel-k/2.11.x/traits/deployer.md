# Deployer Trait

The deployer trait is responsible for deploying the resources owned by the integration, and can be used to explicitly select the underlying controller that will manage the integration pods.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

> **Note**
> The deployer trait is a **platform trait** and cannot be disabled by the user.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait deployer.[key]=[value] --trait deployer.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `deployer.enabled` | `bool` | Deprecated: no longer in use. |
| `deployer.kind` | `string` | Allows to explicitly select the desired deployment kind between `deployment`, `cron-job` or `knative-service` when creating the resources for running the integration.
Deprecated: this feature will be removed in future releases.

 |
| `deployer.useSSA` | `bool` | Deprecated: no longer in use. |
> **Note**
> the variable names are "snake case" if you’re using in `kamel` CLI, for example `trait.myParam` has to be translated as `-t trait.my-param`
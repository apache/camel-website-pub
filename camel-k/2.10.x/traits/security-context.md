# Security Context Trait

The Security Context trait can be used to configure the security setting of the Pod running the application.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

> **Note**
> The security-context trait is a **platform trait** and cannot be disabled by the user.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait security-context.[key]=[value] --trait security-context.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `security-context.enabled` | `bool` | Deprecated: no longer in use. |
| `security-context.run-as-user` | `int64` | Security Context RunAsUser configuration (default none): this value is automatically retrieved in Openshift clusters when not explicitly set. |
| `security-context.run-as-non-root` | `bool` | Security Context RunAsNonRoot configuration (default false). |
| `security-context.seccomp-profile-type` | `SeccompProfileType` | Security Context SeccompProfileType configuration (default RuntimeDefault). |
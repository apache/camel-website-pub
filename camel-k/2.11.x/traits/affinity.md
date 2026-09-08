# Affinity Trait

Allows constraining which nodes the integration pod(s) are eligible to be scheduled on, based on labels on the node, or with inter-pod affinity and anti-affinity, based on labels on pods that are already running on the nodes.

It’s disabled by default.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait affinity.[key]=[value] --trait affinity.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `affinity.enabled` | `bool` | Can be used to enable or disable a trait. All traits share this common property. |
| `affinity.podAffinity` | `bool` | Always co-locates multiple replicas of the integration in the same node (default `false`). |
| `affinity.podAntiAffinity` | `bool` | Never co-locates multiple replicas of the integration in the same node (default `false`). |
| `affinity.nodeAffinityLabels` | `[]string` | Defines a set of nodes the integration pod(s) are eligible to be scheduled on, based on labels on the node. |
| `affinity.podAffinityLabels` | `[]string` | Defines a set of pods (namely those matching the label selector, relative to the given namespace) that the integration pod(s) should be co-located with. |
| `affinity.podAntiAffinityLabels` | `[]string` | Defines a set of pods (namely those matching the label selector, relative to the given namespace) that the integration pod(s) should not be co-located with. |
> **Note**
> the variable names are "snake case" if you’re using in `kamel` CLI, for example `trait.myParam` has to be translated as `-t trait.my-param`

## Examples

-   To schedule the integration pod(s) on a specific node using the [built-in node label](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#interlude-built-in-node-labels) `kubernetes.io/hostname`:
    
    ```console
    $ kamel run -t affinity.node-affinity-labels="kubernetes.io/hostname in(node-66-50.hosted.k8s.tld)" ...
    ```
    
-   To schedule a single integration pod per node (using the `Exists` operator):
    
    ```console
    $ kamel run -t affinity.pod-anti-affinity-labels="camel.apache.org/integration" ...
    ```
    
-   To co-locate the integration pod(s) with other integration pod(s):
    
    ```console
    $ kamel run -t affinity.pod-affinity-labels="camel.apache.org/integration in(it1, it2)" ...
    ```
    

The `*-labels` options follow the requirements from [Label selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#label-selectors). They can be multi-valuated, then the requirements list is ANDed, e.g., to schedule a single integration pod per node AND not co-located with the Camel K operator pod(s):

```console
$ kamel run -t affinity.pod-anti-affinity-labels="camel.apache.org/integration" -t affinity.pod-anti-affinity-labels="camel.apache.org/component=operator" ...
```

More information can be found in the official Kubernetes documentation about [Assigning Pods to Nodes](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/).

> **Note**
> Operators can restrict which label keys CR authors are permitted to use in `affinity.nodeAffinityLabels` by setting the `AFFINITY_NODE_LABELS_ALLOWED_KEYS` environment variable on the operator deployment to a comma-separated list of allowed keys (e.g. `kubernetes.io/hostname,topology.kubernetes.io/zone`). Expressions whose key is not in the list are dropped and an info message is logged. When the variable is unset or empty, all keys are accepted (default behavior). See build environment variables documentation for details.
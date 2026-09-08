# Toleration Trait

This trait sets Tolerations over Integration pods. Tolerations allow (but do not require) the pods to schedule onto nodes with matching taints. See [https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for more details.

The toleration should be expressed in a similar manner that of taints, i.e., `Key[=Value]:Effect[:Seconds]`, where values in square brackets are optional.

For examples:

-   `node-role.kubernetes.io/master:NoSchedule`
    
-   `node.kubernetes.io/network-unavailable:NoExecute:3000`
    
-   `disktype=ssd:PreferNoSchedule`
    

It’s disabled by default.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait toleration.[key]=[value] --trait toleration.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `toleration.enabled` | `bool` | Can be used to enable or disable a trait. All traits share this common property. |
| `toleration.taints` | `[]string` | The list of taints to tolerate, in the form `Key[=Value]:Effect[:Seconds]` |

## Examples

-   To tolerate the integration pod(s) to be scheduled on the master node:
    
    ```console
    $ kamel run -t toleration.taints="node-role.kubernetes.io/master:NoSchedule" ...
    ```
    
-   To tolerate the integration pod(s) executing on a node with network not available for 300 seconds:
    
    ```console
    $ kamel run -t toleration.taints="node.kubernetes.io/network-unavailable:NoExecute:300" ...
    ```
    
-   To tolerate the integration pod(s) to be scheduled on a node with a disk of SSD type:
    
    ```console
    $ kamel run -t toleration.taints="disktype=ssd:PreferNoSchedule" ...
    ```
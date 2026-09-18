# Infrastructure Pods and Resource Management

During the installation procedure you will be able to provide information on how to best "operationalize" your infrastructure. Here we give you some Kubernetes best practices you can use in order to configure a production ready environment.

The usage of these advanced configuration assumes you’re familiar with the [Kubernetes Scheduling](https://kubernetes.io/docs/concepts/scheduling-eviction/) concepts and configurations.

Depending on the installation methodology (ie, Helm) provided you may have certain configuration parameters out of the box. Otherwise you should be able to fine tune those parameters altering directly the Camel K operator Deployment.

## Scheduling Node Selectors, Affinity and Tolerations

### Operator Pod

We suggest to edit the Deployment to configure the [`NodeSelector` Kubernetes feature](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/) and the [`Taint` and `Toleration` Kubernetes feature](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/).

### Builder Pods and Integrations

Builder Pods and Integration Pods can be also scheduled and assigned in the cluster. For this reason you need to use [builder trait](../../traits/builder.md) configuration (for builder Pod when using `pod` building strategy) and [affinity](../../traits/affinity.md), [pod](../../traits/pod.md), [toleration](../../traits/toleration.md) traits for Integration Pods.

## Resources

While installing the Camel K operator, you can also specify the resources requests and limits to assign to the operator `Pod`. This configuration will expect the setting as required by [Kubernetes Resource Management](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/).

> **Note**
> if you specify a limit, but does not specify a request, Kubernetes automatically assigns a request that matches the limit.

### Default Operator Pod configuration

The main Camel K Operator Pod contributor resources consumption is likely to be the number of parallel builds that are performed in the operator `Pod`. So the resource requirements should be defined accordingly. The following requirements are sensible defaults that should work in most cases:

```none
resources:
  requests:
    memory: "2Gi"
    cpu: "500m"
  limits:
    memory: "8Gi"
    cpu: "2"
```

Note that if you plan to perform **native builds**, then the memory requirements may be increased significantly. Also, the CPU requirements are rather "soft", in the sense that it won’t break the operator, but it’ll perform slower in general.

### Default Integration Pod configuration

The resource set on the container here is highly dependant on what your application is doing. You can control this behavior by setting opportunely the resources on the Integration via [container](../../traits/container.md) trait.

Be aware that the default are actually the following:

```none
resources:
  requests:
    memory: "256Mi"
    cpu: "125m"
  limits:
    memory: "1Gi"
    cpu: "500m"
```

### Builder Pod configuration

You can set the resources requests and limits for the builder Pod using [container](../../traits/builder.md) trait.
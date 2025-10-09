# Camel K Monitoring

The Camel K monitoring architecture relies on [Prometheus](https://prometheus.io) and the eponymous operator.

The [Prometheus Operator](https://prometheus-operator.dev) serves to make running Prometheus on top of Kubernetes as easy as possible, while preserving Kubernetes-native configuration options.

## Prerequisites

To take full advantage of the Camel K monitoring capabilities, it is recommended to have a Prometheus Operator instance, that can be configured to integrate the Camel K operator and integrations.

### Kubernetes

The easiest way of starting with the Prometheus Operator is by deploying it as part of [kube-prometheus](https://github.com/prometheus-operator/kube-prometheus), which provisions an entire monitoring stack. You can follow the [quickstart](https://prometheus-operator.dev/docs/prologue/quick-start/) from the Prometheus Operator [documentation](https://prometheus-operator.dev/).

Alternatively, you can quickly deploy the Prometheus operator by running:

```console
$ kubectl apply -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/main/bundle.yaml
```

> **Warning**
> Beware this installs the operator in the `default` namespace. You must download the file locally and replace the `namespace` fields to deploy the resources into another namespace. This also installs the version from the `main` branch, which you can change in the URL by choosing a stable release version.

Then, you can create a `Prometheus` resource, that the operator will use as configuration to deploy a managed Prometheus instance:

```console
$ cat <<EOF | kubectl apply -f -
apiVersion: monitoring.coreos.com/v1
kind: Prometheus
metadata:
  name: prometheus
spec:
  podMonitorSelector:
    matchExpressions:
      - key: camel.apache.org/integration
        operator: Exists
EOF
```

By default, the Prometheus instance discovers applications to be monitored in the same namespace. You can use the `podMonitorNamespaceSelector` field from the `Prometheus` resource to enable cross-namespace monitoring. You may also need to specify a ServiceAccount with the `serviceAccountName` field, that’s bound to a Role with the necessary permissions.

### OpenShift

Starting OpenShift 4.3, the Prometheus Operator, that’s already deployed as part of the monitoring stack, can be used to [monitor application services](https://docs.openshift.com/container-platform/4.3/monitoring/monitoring-your-own-services.md). This needs to be enabled by following these instructions:

1.  Check whether the `cluster-monitoring-config` ConfigMap object exists in the `openshift-monitoring` project:
    
    $ oc -n openshift-monitoring edit configmap cluster-monitoring-config
    
2.  If it does not exist, create it:
    
    $ oc -n openshift-monitoring create configmap cluster-monitoring-config
    
3.  Start editing the cluster-monitoring-config ConfigMap:
    
    $ oc -n openshift-monitoring edit configmap cluster-monitoring-config
    
4.  Set the `enableUserWorkload` setting to `true` under `data/config.yaml`:
    
    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: cluster-monitoring-config
      namespace: openshift-monitoring
    data:
      config.yaml: |
        enableUserWorkload: true
    ```
    
    Note that, in OpenShift versions from 4.3 to 4.5, the configuration is as following:
    
    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: cluster-monitoring-config
      namespace: openshift-monitoring
    data:
      config.yaml: |
        techPreviewUserWorkload:
          enabled: true
    ```
    

On OpenShift versions prior to 4.3, or if you do not want to change your cluster monitoring stack configuration, you can refer to the [Kubernetes](#kubernetes) section in order to deploy a separate Prometheus Operator instance.

### What’s Next

-   [Camel K operator monitoring](monitoring/operator.md)
    
-   [Camel K integration monitoring](monitoring/integration.md)
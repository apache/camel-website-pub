# Camel K Operator Monitoring

The Camel K Operator monitoring architecture relies on [Prometheus](https://prometheus.io) and the eponymous operator.

The [Prometheus Operator](https://prometheus-operator.dev) serves to make running Prometheus on top of Kubernetes as easy as possible, while preserving Kubernetes-native configuration options.

> **Note**
> the Camel K Integration monitoring part is deprecated in favour of [Camel Dashboard](dashboard.md).

## Prerequisites

To take full advantage of the Camel K operator monitoring capabilities, it is recommended to have a Prometheus Operator instance, that can be configured to integrate the Camel K operator and integrations.

### Kubernetes

The easiest way of starting with the Prometheus Operator is by deploying it as part of [kube-prometheus](https://github.com/prometheus-operator/kube-prometheus), which provisions an entire monitoring stack. You can follow the [quickstart](https://prometheus-operator.dev/docs/prologue/quick-start/) from the Prometheus Operator [documentation](https://prometheus-operator.dev/).

Alternatively, you can quickly deploy the Prometheus operator by running:

```console
$ kubectl apply -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/main/bundle.yaml
```

> **Note**
> the above script installs the operator in the `default` namespace. You must download the file locally and replace the `namespace` fields to deploy the resources into another namespace. This also installs the version from the `main` branch, which you can change in the URL by choosing a stable release version.

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

### What’s Next

-   [Camel K operator monitoring](monitoring/operator.md)
    
-   [Camel K integration monitoring](monitoring/integration.md)
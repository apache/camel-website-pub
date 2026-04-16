# Camel K Operator Monitoring

> **Note**
> The Camel K monitoring architecture relies on [Prometheus](https://prometheus.io) and the eponymous operator. Make sure you’ve checked the [Camel K monitoring prerequisites](../monitoring.html#prerequisites).

## Installation

You need to create the resources required to let Prometheus to interact with the metrics exposed by the operator. There is a Kustomization based configuration you can find under `/install/base/config/prometheus`.

We have prepared a base configuration you can quickly apply executing:

kubectl apply -k github.com/apache/camel-k/install/base/config/prometheus?ref=v2.10.0

> **Note**
> change the ref value with the installation version tag you want to install.

However, most of the time you want to probably configure and add different thresholds and KPIs in order to monitor in a properly manner your installation.

## Metrics

The Camel K operator monitoring endpoint exposes the following metrics:

Table 1. Camel K operator metrics     
| Name | Type | Description | Buckets | Labels |
| --- | --- | --- | --- | --- |
| `camel_k_reconciliation_duration_seconds` | `HistogramVec` | Reconciliation request duration | 0.25s, 0.5s, 1s, 5s | `namespace`, `group`, `version`, `kind`, `result`: `Reconciled`|`Errored`|`Requeued`, `tag`: `""`|`PlatformError`|`UserError` |
| `camel_k_build_duration_seconds` | `HistogramVec` | Build duration | 30s, 1m, 1.5m, 2m, 5m, 10m | `result`, `type`: `Succeeded`|`Error`, `fast-jar`|`native` |
| `camel_k_build_recovery_attempts` | `Histogram` | Build recovery attempts | 0, 1, 2, 3, 4, 5 | `result`, `type`: `Succeeded`|`Error`, `fast-jar`|`native` |
| `camel_k_build_queue_duration_seconds` | `Histogram` | Build queue duration | 5s, 15s, 30s, 1m, 5m, | `type`: `fast-jar`|`native` |
| `camel_k_integration_first_readiness_seconds` | `Histogram` | Time to first integration readiness | 5s, 10s, 30s, 1m, 2m | N/A |

## Discovery

A `PodMonitor` resource must be created for the Prometheus Operator to reconcile, so that the managed Prometheus instance can scrape the Camel K operator _metrics_ endpoint.

As an example, hereafter is the `PodMonitor` resource that is created when executing the default Prometheus configuration provided above:

operator-pod-monitor.yaml

```yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: camel-k-operator
  labels: (1)
    ...
spec:
  selector:
    matchLabels: (2)
      app: "camel-k"
      camel.apache.org/component: operator
  podMetricsEndpoints:
    - port: metrics
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>The labels must match the <code>podMonitorSelector</code> field from the <code>Prometheus</code> resource</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>This label selector matches the Camel K operator Deployment labels</td></tr></tbody></table>

The Prometheus Operator [getting started](https://prometheus-operator.dev/docs/user-guides/getting-started/) guide documents the discovery mechanism, as well as the relationship between the operator resources.

In case your operator metrics are not discovered, you may want to rely on [Troubleshooting `ServiceMonitor` changes](https://prometheus-operator.dev/docs/operator/troubleshooting/#troubleshooting-servicemonitor-changes), which also applies to `PodMonitor` resources troubleshooting.

## Alerting

> **Note**
> The Prometheus Operator declares the `AlertManager` resource that can be used to configure _AlertManager_ instances, along with `Prometheus` instances. The following section assumes an `AlertManager` resource already exists in your cluster.

A `PrometheusRule` resource can be created for the Prometheus Operator to reconcile, so that the managed AlertManager instance can trigger alerts, based on the metrics exposed by the Camel K operator.

As an example, hereafter is the alerting rules that are defined in `PrometheusRule` resource that is created when executing the default Prometheus configuration provided above:

Table 2. Camel K operator alerts   
| Name | Severity | Description |
| --- | --- | --- |
| `CamelKReconciliationDuration` | warning | More than 10% of the reconciliation requests have their duration above 0.5s over at least 1 min. |
| `CamelKReconciliationFailure` | warning | More than 1% of the reconciliation requests have failed over at least 10 min. |
| `CamelKSuccessBuildDuration2m` | warning | More than 10% of the successful builds have their duration above 2 min over at least 1 min. |
| `CamelKSuccessBuildDuration5m` | critical | More than 1% of the successful builds have their duration above 5 min over at least 1 min. |
| `CamelKBuildError` | critical | More than 1% of the builds have errored over at least 10 min. |
| `CamelKBuildQueueDuration1m` | warning | More than 1% of the builds have been queued for more than 1 min over at least 1 min. |
| `CamelKBuildQueueDuration5m` | critical | More than 1% of the builds have been queued for more than 5 min over at least 1 min. |

You can register your own `PrometheusRule` resources, to be used by Prometheus AlertManager instances to trigger alerts, e.g.:

```yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: camel-k-alerts
spec:
  groups:
    - name: camel-k-alerts
      rules:
        - alert: CamelKIntegrationTimeToReadiness
          expr: |
            (
            1 - sum(rate(camel_k_integration_first_readiness_seconds_bucket{le="60"}[5m])) by (job)
            /
            sum(rate(camel_k_integration_first_readiness_seconds_count[5m])) by (job)
            )
            * 100
            > 10
          for: 1m
          labels:
            severity: warning
          annotations:
            message: |
              {{ printf "%0.0f" $value }}% of the integrations
              for {{ $labels.job }} have their first time to readiness above 1m.
```

More information can be found in the Prometheus Operator [Alerting](https://prometheus-operator.dev/docs/user-guides/alerting/) user guide. You can also find more details in [Creating alerting rules](https://docs.openshift.com/container-platform/4.12/monitoring/managing-alerts.html#creating-alerting-rules-for-user-defined-projects_managing-alerts) from the OpenShift documentation.
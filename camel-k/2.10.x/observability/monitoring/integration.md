# Camel K Integration Monitoring

> **Note**
> The Camel K monitoring architecture relies on [Prometheus](https://prometheus.io) and the eponymous operator. Make sure you’ve checked the [Camel K monitoring prerequisites](../monitoring.html#prerequisites).

## Instrumentation

The [Prometheus trait](../../traits/prometheus.md) automates the configuration of integration pods to expose a _metrics_ endpoint, that can be discovered and scraped by a Prometheus server.

The Prometheus trait can be enabled when running an integration, e.g.:

```console
$ kamel run -t prometheus.enabled=true
```

Alternatively, the Prometheus trait can be enabled globally once, by updating the integration platform, e.g.:

```console
$ kubectl patch ip camel-k --type=merge -p '{"spec":{"traits":{"prometheus":{"configuration":{"enabled":true}}}}}'
```

Or by directly editing the `IntegrationPlatform` resource, e.g.:

```yaml
apiVersion: camel.apache.org/v1
kind: IntegrationPlatform
metadata:
  name: camel-k
spec:
  traits:
    prometheus:
      configuration:
        enabled: true (1)
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Activates the Prometheus trait at the platform level</td></tr></tbody></table>

The Camel Quarkus Micrometer Metrics extension is responsible for collecting and exposing metrics in the [OpenMetrics](https://github.com/OpenObservability/OpenMetrics) text format.

The Micrometer Metrics extension registers and exposes the following metrics out-of-the-box:

-   Basic JVM and operating system related metrics
    
-   [Camel related metrics](../../../../components/4.18.x/micrometer-component.md)
    

It is possible to extend this set of metrics by using either, or both:

-   The Micrometer Metrics component
    
-   The [Micrometer Quarkus Metrics annotations](https://quarkus.io/guides/micrometer#does-micrometer-support-annotations)
    

## Discovery

The Prometheus trait automatically configures the resources necessary for the Prometheus Operator to reconcile, so that the managed Prometheus instance can scrape the integration _metrics_ endpoint.

By default, the Prometheus trait creates a `PodMonitor` resource, with the `camel.apache.org/integration` label, which must match the `podMonitorSelector` field from the `Prometheus` resource. Additional labels can be specified with the `pod-monitor-labels` parameter from the Prometheus trait, e.g.:

```console
$ kamel run -t prometheus.pod-monitor-labels="label_to_be_match_by=prometheus_selector" ...
```

The creation of the `PodMonitor` resource can be disabled using the `pod-monitor` parameter, e.g.:

```console
$ kamel run -t prometheus.pod-monitor=false ...
```

More information can be found in the [Prometheus trait](../../traits/prometheus.md) documentation.

The Prometheus Operator [getting started](https://prometheus-operator.dev/docs/user-guides/getting-started/) guide documents the discovery mechanism, as well as the relationship between the operator resources.

In case your integration metrics are not discovered, you may want to rely on [Troubleshooting `ServiceMonitor` changes](https://prometheus-operator.dev/docs/operator/troubleshooting/#troubleshooting-servicemonitor-changes), which also applies to `PodMonitor` resources troubleshooting.

## Alerting

The Prometheus Operator declares the `AlertManager` resource that can be used to configure _AlertManager_ instances, along with `Prometheus` instances.

Assuming an `AlertManager` resource already exists in your cluster, you can register a `PrometheusRule` resource that is used by Prometheus to trigger alerts, e.g.:

```console
$ cat <<EOF | kubectl apply -f -
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  labels:
    prometheus: example
    role: alert-rules
  name: prometheus-rules
spec:
  groups:
  - name: camel-k.rules
    rules:
    - alert: CamelKAlert
      expr: application_camel_context_exchanges_failed_total > 0
EOF
```

More information can be found in the Prometheus Operator [Alerting](https://prometheus-operator.dev/docs/user-guides/alerting/) user guide. You can also find more details in [Creating alerting rules](https://docs.openshift.com/container-platform/4.12/monitoring/managing-alerts.html#creating-alerting-rules-for-user-defined-projects_managing-alerts) from the OpenShift documentation.
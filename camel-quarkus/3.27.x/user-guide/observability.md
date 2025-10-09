# Observability

## Health & liveness checks

Health & liveness checks are supported via the [MicroProfile Health](../reference/extensions/microprofile-health.md) extension. They can be configured via the [Camel Health](../../../manual/health-check.md) API or via [Quarkus MicroProfile Health](https://quarkus.io/guides/microprofile-health).

All configured checks are available on the standard MicroProfile Health endpoint URLs:

-   [http://localhost:8080/q/health](http://localhost:8080/q/health)
    
-   [http://localhost:8080/q/health/live](http://localhost:8080/q/health/live)
    
-   [http://localhost:8080/q/health/ready](http://localhost:8080/q/health/ready)
    

There’s an example project which demonstrates health checks: [https://github.com/apache/camel-quarkus-examples/tree/main/health](https://github.com/apache/camel-quarkus-examples/tree/main/health)

Note that the `/q` path prefix was added in Camel Quarkus 2.0.0. Refer to the [migration guide](../migration-guide/2.0.0.md) for more information.

## Metrics

Metrics are provided by the [Micrometer](../reference/extensions/micrometer.md) extension which integrates with [Quarkus Micrometer](https://quarkus.io/guides/micrometer).

Some basic Camel metrics are provided for you out of the box, and these can be supplemented by configuring additional metrics in your routes.

Metrics are available on the standard Quarkus metrics endpoint:

-   [http://localhost:8080/q/metrics](http://localhost:8080/q/metrics)
    

## Tracing

[Camel Quarkus OpenTelemetry extension](../reference/extensions/opentelemetry.md) and [Camel Quarkus OpenTelemetry2 extension](../reference/extensions/opentelemetry.md) integrate with the [Quarkus OpenTelemetry extension](https://quarkus.io/guides/opentelemetry). All you need to do is set up the required [configuration](https://quarkus.io/guides/opentelemetry#create-the-configuration) properties and an `OpenTelemetryTracer` will get automatically added to the registry for Camel to use.

There’s an example project demonstrating the above features here: [https://github.com/apache/camel-quarkus-examples/tree/main/observability](https://github.com/apache/camel-quarkus-examples/tree/main/observability)

## All-in-One observability

For a simplified observability experience, use the [Observability Services](../reference/extensions/observability-services.md) extension. It provides all of the above mentioned features, together with some opinionated configuration defaults.
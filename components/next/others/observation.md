# Micrometer Observability

> **Warning**
> **Deprecated:** This observation is deprecated and may be removed in a future release.

**Since Camel 3.21**

The Micrometer Observation component is used for performing observability of incoming and outgoing Camel messages using [Micrometer Observation](https://micrometer.io/docs/observation).

> **Note**
> this component is deprecated since version 4.19.0. Please, use [`camel-micrometer-observability`](micrometer-observability.md) component instead.

By configuring the `ObservationRegistry` you can add behaviour to your observations such as metrics (e.g., via `Micrometer`) or tracing (e.g., via `OpenTelemetry` or `Brave`) or any custom behaviour.

Events are captured for incoming and outgoing messages being sent to/from Camel.

## Configuration

The configuration properties for the Micrometer Observations are:

  
| Option | Default | Description |
| --- | --- | --- |
| excludePatterns |  | Sets exclude pattern(s) that will disable tracing for Camel messages that matches the pattern. The content is a Set<String> where the key is a pattern. The pattern uses the rules from Intercept. |
| encoding | false | Sets whether the header keys need to be encoded (connector specific) or not. The value is a boolean. Dashes required for instances to be encoded for JMS property keys. |

### Configuration

Include the `camel-opentelemetry` component in your POM, along with any specific dependencies associated with the chosen OpenTelemetry compliant Tracer.

To explicitly configure OpenTelemetry support, instantiate the `OpenTelemetryTracer` and initialize the camel context. You can optionally specify a `Tracer`, or alternatively it can be implicitly discovered using the `Registry`

```java
ObservationRegistry observationRegistry = ObservationRegistry.create();
MicrometerObservationTracer micrometerObservationTracer = new MicrometerObservationTracer();

// This component comes from Micrometer Core - it's used for creation of metrics
MeterRegistry meterRegistry = new SimpleMeterRegistry();

// This component comes from Micrometer Tracing - it's an abstraction over tracers
io.micrometer.tracing.Tracer otelTracer = otelTracer();
// This component comes from Micrometer Tracing - an example of B3 header propagation via OpenTelemetry
OtelPropagator otelPropagator = new OtelPropagator(ContextPropagators.create(B3Propagator.injectingSingleHeader()), tracer);

// Configuration ObservationRegistry for metrics
observationRegistry.observationConfig().observationHandler(new DefaultMeterObservationHandler(meterRegistry));

// Configuration ObservationRegistry for tracing
observationRegistry.observationConfig().observationHandler(new ObservationHandler.FirstMatchingCompositeObservationHandler(new CamelPropagatingSenderTracingObservationHandler<>(otelTracer, otelPropagator), new CamelPropagatingReceiverTracingObservationHandler<>(otelTracer, otelPropagator), new CamelDefaultTracingObservationHandler(otelTracer)));

// Both components ObservationRegistry and MeterRegistry should be set manually, or they will be resolved from CamelContext if present
micrometerObservationTracer.setObservationRegistry(observationRegistry);
micrometerObservationTracer.setTracer(otelTracer);

// Initialize the MicrometerObservationTracer
micrometerObservationTracer.init(context);
```

## Spring Boot

If you are using Spring Boot, then you can add the `camel-observation-starter` dependency, and turn on OpenTracing by annotating the main class with `@CamelObservation`.

The `MicrometerObservationTracer` will be implicitly obtained from the camel context’s `Registry`, unless a `MicrometerObservationTracer` bean has been defined by the application.

## Spring Boot Auto-Configuration

When using observation with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-observation-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.observation.encoding** | **Deprecated** Activate or deactivate dash encoding in headers (required by JMS) for messaging. |  | Boolean |
| **camel.observation.exclude-patterns** | **Deprecated** Sets exclude pattern(s) that will disable observability for Camel messages that matches the pattern. Multiple patterns can be separated by comma. |  | String |

## MDC Logging

You can add \[Micrometer Observability Mapped Diagnostic Context tracing information\]([https://docs.micrometer.io/tracing/reference/index.html](https://docs.micrometer.io/tracing/reference/index.md)) (ie, `traceId` and `spanId`) adding some instrumentation bridge to your application. You may add the `io.micrometer:micrometer-tracing-bridge-otel` dependency and you will be able to get those MDC information automatically.

> **Note**
> mind that MDC variables `traceId` and `spanId` are different from other tracing implementations (eg, `camel-opentelemetry`) which use `trace_id` and `span_id`.
# Micrometer Observability

**Since Camel 3.21**

The Micrometer Observation component is used for performing observability of incoming and outgoing Camel messages using [Micrometer Observation](https://micrometer.io/docs/observation).

By configuring the `ObservationRegistry` you can add behaviour to your observations such as metrics (e.g. via `Micrometer`) or tracing (e.g. via `OpenTelemetry` or `Brave`) or any custom behaviour.

Events are captured for incoming and outgoing messages being sent to/from Camel.

## Configuration

The configuration properties for the Micrometer Observations are:

  
| Option | Default | Description |
| --- | --- | --- |
| excludePatterns |  | Sets exclude pattern(s) that will disable tracing for Camel messages that matches the pattern. The content is a Set<String> where the key is a pattern. The pattern uses the rules from Intercept. |
| encoding | false | Sets whether the header keys need to be encoded (connector specific) or not. The value is a boolean. Dashes need for instances to be encoded for JMS property keys. |

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
// This component comes from Micrometer Tracing - example of B3 header propagation via OpenTelemetry
OtelPropagator otelPropagator = new OtelPropagator(ContextPropagators.create(B3Propagator.injectingSingleHeader()), tracer);

// Configuration ObservationRegistry for metrics
observationRegistry.observationConfig().observationHandler(new DefaultMeterObservationHandler(meterRegistry));

// Configuration ObservationRegistry for tracing
observationRegistry.observationConfig().observationHandler(new ObservationHandler.FirstMatchingCompositeObservationHandler(new CamelPropagatingSenderTracingObservationHandler<>(otelTracer, otelPropagator), new CamelPropagatingReceiverTracingObservationHandler<>(otelTracer, otelPropagator), new CamelDefaultTracingObservationHandler(otelTracer)));

// Both components ObserationRegistry and MeterRegistry should be set manually or they will be resolved from CamelContext if present
micrometerObservationTracer.setObservationRegistry(observationRegistry);
micrometerObservationTracer.setTracer(otelTracer);

// Initialize the MicrometerObservationTracer
micrometerObservationTracer.init(context);
```

## Spring Boot

If you are using Spring Boot then you can add the `camel-observation-starter` dependency, and turn on OpenTracing by annotating the main class with `@CamelObservation`.

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

The component supports 12 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.observation.encoding** | Activate or deactivate dash encoding in headers (required by JMS) for messaging. |  | Boolean |
| **camel.observation.exclude-patterns** | Sets exclude pattern(s) that will disable observability for Camel messages that matches the pattern. |  | Set |
| **management.tracing.baggage.correlation.enabled** | Whether to enable correlation of the baggage context with logging contexts. | true | Boolean |
| **management.tracing.baggage.correlation.fields** | List of fields that should be correlated with the logging context. That means that these fields would end up as key-value pairs in e.g. MDC. |  | List |
| **management.tracing.baggage.enabled** | Whether to enable Micrometer Tracing baggage propagation. | true | Boolean |
| **management.tracing.baggage.remote-fields** | List of fields that are referenced the same in-process as it is on the wire. For example, the field "x-vcap-request-id" would be set as-is including the prefix. |  | List |
| **management.tracing.enabled** | Whether auto-configuration of tracing is enabled. | true | Boolean |
| **management.tracing.propagation.type** | Tracing context propagation type. |  | TracingProperties$Propagation$PropagationType |
| **management.tracing.sampling.probability** | Probability in the range from 0.0 to 1.0 that a trace will be sampled. | 0.1 | Float |
| **management.zipkin.tracing.connect-timeout** | Connection timeout for requests to Zipkin. | 1s | Duration |
| **management.zipkin.tracing.endpoint** | URL to the Zipkin API. | [http://localhost:9411/api/v2/spans](http://localhost:9411/api/v2/spans) | String |
| **management.zipkin.tracing.read-timeout** | Read timeout for requests to Zipkin. | 10s | Duration |

## MDC Logging

When MDC Logging is enabled for the active Camel context the Trace ID and Span ID will be added and removed from the MDC for each route, the keys are `trace_id` and `span_id`, respectively.
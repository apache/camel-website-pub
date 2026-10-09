# OpenFeature

**Since Camel 4.23**

**Only producer is supported**

The OpenFeature component evaluates feature flags using the [OpenFeature specification](https://openfeature.dev/) with [flagd](https://flagd.dev/) as the default provider.

It supports boolean flags for toggle and detour patterns, and string flags for A/B testing, fractional targeting, and targeted rollout.

For boolean predicates in Java, XML and YAML DSL, use the [OpenFeature language](languages/openfeature-language.md) supplied by this component.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-openfeature</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

openfeature:domain\[/evaluationType\]\[?options\]

Where **domain** is the OpenFeature domain to bind the provider to and **evaluationType** is an optional path parameter that selects the evaluation type (`boolean`, `variant`, or `isEnabled`).

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The OpenFeature component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Default configuration shared by OpenFeature endpoints. |  | OpenFeatureConfiguration |
| **contextFromBody** (common) | When true, a Map message body is used as the evaluation context. When false (default), the body is not used as context. The CamelOpenFeatureEvaluationContext header is always used regardless of this setting. | false | boolean |
| **deadline** (common) | Deadline in milliseconds for the remote flagd connection. | 500 | int |
| **defaultValue** (common) | Default value when flag evaluation fails. When evaluationType is not set, also determines the evaluation type: true or false (case-insensitive) selects boolean evaluation, any other value selects string evaluation. | false | String |
| **evaluationType** (common) | 
The evaluation type. 'boolean' and 'isEnabled' use boolean evaluation (getBooleanValue). 'variant' uses string evaluation (getStringValue). When not set, the type is inferred from defaultValue. Can also be set as a path parameter in the endpoint URI, which takes precedence.

Enum values:

-   boolean
    
-   variant
    
-   isEnabled
    





 |  | String |
| **flagKey** (common) | The feature flag key to evaluate. Can be overridden per message via the CamelOpenFeatureFlagKey header. |  | String |
| **flags** (common) | A JSON object defining feature flags in flagd format (inline). Mutually exclusive with flagsResource. |  | String |
| **flagsResource** (common) | Camel resource URI pointing to a feature flag definition file in flagd format. Mutually exclusive with flags. When provider is also set, the provider takes precedence. |  | String |
| **host** (common) | Remote flagd service host. When set, the flagd RPC resolver is used. |  | String |
| **port** (common) | Remote flagd service port. | 8013 | int |
| **provider** (common) | Bean reference to a custom FeatureProvider (e.g. #myProvider). When set, takes precedence over flags, flagsResource, and host. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **resultProperty** (producer) | Store the evaluation result in this exchange property, preserving the original message body. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **certPath** (security) | Path to the TLS certificate for the remote flagd connection. |  | String |
| **tls** (security) | Whether to use TLS for the remote flagd connection. | false | boolean |

## Endpoint Options

The OpenFeature endpoint is configured using URI syntax:

openfeature:domain/evaluationType

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **domain** (producer) | **Required** The OpenFeature domain to bind the provider to. |  | String |
| **evaluationType** (producer) | 
The evaluation type. 'boolean' and 'isEnabled' use boolean evaluation (getBooleanValue). 'variant' uses string evaluation (getStringValue). When not set, the type is inferred from defaultValue.

Enum values:

-   boolean
    
-   variant
    
-   isEnabled
    





 |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **contextFromBody** (common) | When true, a Map message body is used as the evaluation context. When false (default), the body is not used as context. The CamelOpenFeatureEvaluationContext header is always used regardless of this setting. | false | boolean |
| **deadline** (common) | Deadline in milliseconds for the remote flagd connection. | 500 | int |
| **defaultValue** (common) | Default value when flag evaluation fails. When evaluationType is not set, also determines the evaluation type: true or false (case-insensitive) selects boolean evaluation, any other value selects string evaluation. | false | String |
| **flagKey** (common) | The feature flag key to evaluate. Can be overridden per message via the CamelOpenFeatureFlagKey header. |  | String |
| **flags** (common) | A JSON object defining feature flags in flagd format (inline). Mutually exclusive with flagsResource. |  | String |
| **flagsResource** (common) | Camel resource URI pointing to a feature flag definition file in flagd format. Mutually exclusive with flags. When provider is also set, the provider takes precedence. |  | String |
| **host** (common) | Remote flagd service host. When set, the flagd RPC resolver is used. |  | String |
| **port** (common) | Remote flagd service port. | 8013 | int |
| **provider** (common) | Bean reference to a custom FeatureProvider (e.g. #myProvider). When set, takes precedence over flags, flagsResource, and host. |  | String |
| **resultProperty** (producer) | Store the evaluation result in this exchange property, preserving the original message body. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **certPath** (security) | Path to the TLS certificate for the remote flagd connection. |  | String |
| **tls** (security) | Whether to use TLS for the remote flagd connection. | false | boolean |

## Message Headers

The OpenFeature component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOpenFeatureFlagKey** (producer) Constant: [`FLAG_KEY`](https://javadoc.io/doc/org.apache.camel/camel-openfeature/latest/org/apache/camel/component/openfeature/OpenFeatureConstants.html#FLAG_KEY) | Overrides the configured flag key for this message. |  | String |
| **CamelOpenFeatureTargetingKey** (producer) Constant: [`TARGETING_KEY`](https://javadoc.io/doc/org.apache.camel/camel-openfeature/latest/org/apache/camel/component/openfeature/OpenFeatureConstants.html#TARGETING_KEY) | Sets the targeting key for the OpenFeature evaluation context. |  | String |
| **CamelOpenFeatureEvaluationContext** (producer) Constant: [`EVALUATION_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-openfeature/latest/org/apache/camel/component/openfeature/OpenFeatureConstants.html#EVALUATION_CONTEXT) | A Map of additional evaluation context key-value pairs. |  | Map |
| **CamelOpenFeatureEvaluationType** (producer) Constant: [`EVALUATION_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-openfeature/latest/org/apache/camel/component/openfeature/OpenFeatureConstants.html#EVALUATION_TYPE) | Sets the evaluation type (boolean, variant, isEnabled) for the OpenFeature evaluation. |  | String |
| **CamelOpenFeatureVariant** (producer) Constant: [`EVALUATION_VARIANT`](https://javadoc.io/doc/org.apache.camel/camel-openfeature/latest/org/apache/camel/component/openfeature/OpenFeatureConstants.html#EVALUATION_VARIANT) | The variant name returned by the provider for this evaluation. |  | String |
| **CamelOpenFeatureReason** (producer) Constant: [`EVALUATION_REASON`](https://javadoc.io/doc/org.apache.camel/camel-openfeature/latest/org/apache/camel/component/openfeature/OpenFeatureConstants.html#EVALUATION_REASON) | The reason string returned by the provider for this evaluation. |  | String |
| **CamelOpenFeatureErrorCode** (producer) Constant: [`EVALUATION_ERROR_CODE`](https://javadoc.io/doc/org.apache.camel/camel-openfeature/latest/org/apache/camel/component/openfeature/OpenFeatureConstants.html#EVALUATION_ERROR_CODE) | The error code when the evaluation failed (e.g. FLAG\_NOT\_FOUND, TYPE\_MISMATCH). |  | String |

## Provider resolution

The component resolves the feature flag provider in this order:

1.  **Explicit provider bean** (`provider`): a bean reference (e.g., `#myProvider`) to a custom `FeatureProvider` looked up from the Camel registry. When set, `provider` takes precedence over `flags`, `flagsResource`, and `host`.
    
2.  **Default bean lookup**: a bean named `flags` of type `FeatureProvider` in the Camel registry.
    
3.  **Flagd fallback** (`flags`, `flagsResource`, or `host`): creates a flagd provider automatically. Use `flags` or `flagsResource` for local file-based evaluation, or `host` for a remote flagd gRPC service.
    

## Evaluation type

The evaluation type (boolean or string) can be set as a path parameter in the endpoint URI or as a query parameter / component property:

-   `boolean` — boolean evaluation (`getBooleanValue`)
    
-   `isEnabled` — same as `boolean`, semantically indicates a feature toggle check
    
-   `variant` — string evaluation (`getStringValue`)
    

When `evaluationType` appears both as a path parameter and as a query parameter or component property, the path parameter takes precedence.

Examples:

openfeature:flags/boolean?flagKey=enrichment-enabled
openfeature:flags/isEnabled?flagKey=enrichment-enabled
openfeature:flags/variant?flagKey=checkout-banner
openfeature:flags?flagKey=enrichment-enabled&evaluationType=boolean

When `evaluationType` is not set at all, the type is inferred from `defaultValue`:

-   When `defaultValue` is `"true"` or `"false"` (case-insensitive), boolean evaluation is used.
    
-   When `defaultValue` is any other string, string evaluation is used.
    

The default is `"false"` with no `evaluationType`, so boolean evaluation is the default.

## Evaluation context and targeting key

The OpenFeature evaluation context carries metadata about the current request — such as a user ID, customer tier, or region — so the provider can make targeting decisions. The **targeting key** is a special field that uniquely identifies the subject of the evaluation (e.g. a user, an order, or a session). Providers use the targeting key for consistent assignment in fractional rollouts and for per-subject targeting rules.

The evaluation context is built from these sources:

1.  **`CamelOpenFeatureEvaluationContext` header or exchange property**: when set to a `Map<String, Object>`, entries are added to the context. An entry with key `"targetingKey"` is treated as the targeting key. Context values preserve their original types (Boolean, Integer, Double, String, etc.) for accurate provider-side evaluation.
    
2.  **Message body** (opt-in): when `contextFromBody=true` is set and no `CamelOpenFeatureEvaluationContext` header or property is present, a `Map<String, Object>` body is used as the context. This is disabled by default to prevent untrusted inbound messages from supplying targeting attributes.
    
3.  **`CamelOpenFeatureTargetingKey` header or exchange property**: when set, overrides the targeting key from any of the above sources.
    

## Evaluation result details

The producer exposes evaluation details as message headers after each evaluation:

-   `CamelOpenFeatureVariant` — the variant name returned by the provider
    
-   `CamelOpenFeatureReason` — the reason string (e.g. `TARGETING_MATCH`, `DEFAULT`, `STATIC`)
    
-   `CamelOpenFeatureErrorCode` — the error code when evaluation failed (e.g. `FLAG_NOT_FOUND`, `TYPE_MISMATCH`)
    

When an evaluation error occurs, a warning is logged with the flag key, error code, and error message.

## Usage

The examples below use flagd flag definitions in [flagd JSON format](https://flagd.dev/reference/flag-definitions/). Store the flag definitions in a file (e.g. `flags.json`) and configure the component to load them:

```properties
camel.component.openfeature.flags-resource = classpath:flags.json
```

### Boolean flag (toggle / detour pattern)

A boolean flag enables or disables a feature. The flag definition declares two variants (`on` / `off`) mapping to `true` / `false`:

```json
{
  "flags": {
    "enrichment-enabled": {
      "state": "ENABLED",
      "variants": { "on": true, "off": false },
      "defaultVariant": "on"
    }
  }
}
```

The route evaluates the flag and stores the result in an exchange property so the original message body is preserved:

```java
from("direct:start")
    .to("openfeature:flags?flagKey=enrichment-enabled&resultProperty=enrichEnabled")
    .choice()
        .when(exchangeProperty("enrichEnabled").isEqualTo(true))
            .to("direct:enrich-order")
        .otherwise()
            .to("direct:skip-enrichment")
    .end();
```

Boolean evaluation is the default (`evaluationType` is unset and `defaultValue` defaults to `"false"`).

### Variant flag (string evaluation)

A variant flag returns a string value rather than a boolean. Set `evaluationType` to `variant` — either as a path parameter or query parameter:

```json
{
  "flags": {
    "checkout-banner": {
      "state": "ENABLED",
      "variants": {
        "summer-sale": "Buy 2 get 1 free!",
        "common": "Free shipping on orders over $50"
      },
      "defaultVariant": "common"
    }
  }
}
```

```java
from("direct:start")
    .to("openfeature:flags/variant?flagKey=checkout-banner&resultProperty=banner")
    .log("Banner: ${exchangeProperty.banner}");
```

The `resultProperty` option stores the result in an exchange property instead of replacing the message body.

### Fractional variant (A/B testing)

A fractional targeting rule splits traffic across variants by percentage. The provider uses the targeting key to assign each request deterministically to a variant — the same targeting key always gets the same variant.

```json
{
  "flags": {
    "routing-algorithm": {
      "state": "ENABLED",
      "variants": {
        "legacy": "content-based-router",
        "new": "dynamic-router"
      },
      "defaultVariant": "legacy",
      "targeting": {
        "fractional": [
          ["legacy", 90],
          ["new", 10]
        ]
      }
    }
  }
}
```

The route passes a targeting key so each order ID is consistently assigned to the same variant:

```java
from("direct:start")
    .setHeader("CamelOpenFeatureTargetingKey", simple("${header.orderId}"))
    .to("openfeature:flags/variant?flagKey=routing-algorithm&resultProperty=algorithm")
    .toD("direct:route-${exchangeProperty.algorithm}");
```

Without a targeting key, fractional evaluation may fall back to a random assignment or the default variant, depending on the provider.

### Targeted variant (context-based rollout)

A targeted rule uses evaluation context attributes to decide which variant to return. In this example, enterprise and VIP customer orders get `v2` while all others get `v1`:

```json
{
  "flags": {
    "order-compliance-v2": {
      "state": "ENABLED",
      "variants": { "v1": "v1", "v2": "v2" },
      "defaultVariant": "v1",
      "targeting": {
        "if": [
          { "in": [{ "var": "customer_tier" }, ["ENTERPRISE", "VIP"]] },
          "v2",
          "v1"
        ]
      }
    }
  }
}
```

The route stores the result in an exchange property and routes dynamically:

```java
from("direct:start")
    .to("openfeature:flags/variant?flagKey=order-compliance-v2&resultProperty=orderVariant")
    .toD("direct:orders-${exchangeProperty.orderVariant}");
```

The evaluation context is provided via a header — useful when the message body carries business data:

```java
from("direct:start")
    .setHeader("CamelOpenFeatureTargetingKey", constant("order-123"))
    .setHeader("CamelOpenFeatureEvaluationContext",
        constant(Map.of("customer_tier", "ENTERPRISE")))
    .to("openfeature:flags/variant?flagKey=order-compliance-v2&resultProperty=orderVariant")
    .toD("direct:orders-${exchangeProperty.orderVariant}");
```

Alternatively, enable `contextFromBody=true` to use a `Map` body as the evaluation context:

```java
from("direct:start")
    .to("openfeature:flags/variant?flagKey=order-compliance-v2"
        + "&resultProperty=orderVariant&contextFromBody=true")
    .toD("direct:orders-${exchangeProperty.orderVariant}");
```

### Remote flagd service

For a remote flagd service, configure `host` (and optionally `port`, `tls`, `certPath`, and `deadline`):

```properties
camel.component.openfeature.host = flagd.example.com
camel.component.openfeature.port = 8013
camel.component.openfeature.tls = true
camel.component.openfeature.cert-path = /etc/tls/ca.crt
camel.component.openfeature.deadline = 1000
```

### Custom provider

OpenFeature is a vendor-neutral specification. Beyond the built-in flagd provider, the OpenFeature community maintains provider implementations for many feature flag services. Examples include LaunchDarkly, Split, Flagsmith, Flipt, ConfigCat, GrowthBook, and AWS AppConfig among others. See the [OpenFeature ecosystem page](https://openfeature.dev/ecosystem/) for the full list of available Java providers.

To use a custom provider, add the provider’s Maven dependency to your project and register it as a bean. For example, the `env-var` provider resolves flag values from environment variables:

```xml
<dependency>
    <groupId>dev.openfeature.contrib.providers</groupId>
    <artifactId>env-var</artifactId>
    <version>0.0.12</version>
</dependency>
```

Register the provider as a bean named `flags` (the default lookup name) or with a custom name:

```java
import dev.openfeature.contrib.providers.envvar.EnvVarProvider;

registry.bind("flags", new EnvVarProvider());
```

Routes then use the provider without any additional configuration:

```java
from("direct:start")
    .to("openfeature:flags?flagKey=MY_FEATURE_FLAG&resultProperty=flagValue");
```

Or reference a named provider bean explicitly:

```java
from("direct:start")
    .to("openfeature:myDomain?flagKey=enrichment-enabled&provider=#myFlagProvider");
```

### InMemoryProvider (testing and simple use cases)

The OpenFeature SDK ships with an `InMemoryProvider` that requires no external service and no additional dependency. Register it as a bean named `flags` to make it the default provider, or reference it explicitly with the `provider` option.

```java
import dev.openfeature.sdk.providers.memory.Flag;
import dev.openfeature.sdk.providers.memory.InMemoryProvider;

InMemoryProvider provider = new InMemoryProvider(Map.of(
    "feature-x", Flag.<Boolean>builder()
        .variant("on", true)
        .variant("off", false)
        .defaultVariant("on")
        .build()));

registry.bind("flags", provider);
```

Routes then use the provider without any additional configuration:

```java
from("direct:start")
    .to("openfeature:flags?flagKey=feature-x");
```

### Boolean predicate in filter (language)

For boolean predicates in EIP constructs, use the [OpenFeature language](languages/openfeature-language.md):

```java
from("direct:start")
    .filter().language("openfeature", "enrichment-enabled")
        .to("direct:enrich-order")
    .end();
```
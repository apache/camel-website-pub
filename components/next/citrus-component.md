# Citrus

**Since Camel 4.24**

**Only producer is supported**

The Citrus component integrates with the [Citrus integration test framework](https://citrusframework.org/) to perform message validation on exchanges arriving at a Camel endpoint. It allows test authors to verify exchange body content, headers, and path expressions (JsonPath, XPath) using Citrus validation modules.

This component is intended for use in Camel route unit and integration tests.

## Maven dependency

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-test-citrus</artifactId>
    <scope>test</scope>
</dependency>
```

## URI format

citrus:operation/name\[?options\]

Where `operation` is `validate` or `receive`, and `name` is an optional identifier to distinguish multiple Citrus endpoints in the same route.

-   `validate` — validates exchanges without modifying them (pass-through validation). Validation failures are collected silently and only surface when `assertIsSatisfied()` is called.
    
-   `receive` — validates exchanges and returns a simulated response (request/response simulation). Validation failures remain on the exchange and trigger Camel’s `onException` handlers.
    

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

The Citrus component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **log** (producer) | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging, then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **exchangeFormatter** (advanced) | **Autowired** To use a custom ExchangeFormatter to format the Exchange into a String suitable for logging. |  | ExchangeFormatter |

## Endpoint Options

The Citrus endpoint is configured using URI syntax:

citrus:operation/name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform. 'validate' validates exchanges without modifying them. 'receive' validates exchanges and returns a simulated response.

Enum values:

-   validate
    
-   receive
    





 |  | String |
| **name** (producer) | A unique name to identify this endpoint. Allows multiple Citrus endpoints with different validation expectations in the same route. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **assertPeriod** (producer) | Sets a grace period after which the mock will re-assert to ensure the preliminary assertion is still valid. This is used, for example, to assert that exactly a number of messages arrive. For example, if the expected count was set to 5, then the assertion is satisfied when five or more messages arrive. To ensure that exactly 5 messages arrive, then you would need to wait a little period to ensure no further message arrives. This is what you can use this method for. By default, this period is disabled. |  | long |
| **expectedCount** (producer) | Specifies the expected number of message exchanges that should be received by this mock. Beware: If you want to expect that 0 messages, then take extra care, as 0 matches when the tests starts, so you need to set a assert period time to let the test run for a while to make sure there are still no messages arrived; for that use the assertPeriod option. If you want to assert that exactly nth message arrives to this mock, then see also the assertPeriod option for further details. | \-1 | int |
| **messageType** (producer) | The message type for validation. Determines which Citrus validation module is used. Supported values: json, xml, yaml, plaintext. |  | String |
| **copyOnExchange** (producer (advanced)) | Sets whether to make a deep copy of the incoming Exchange when received at this mock endpoint. | true | boolean |
| **failFast** (producer (advanced)) | Sets whether assertIsSatisfied() should fail fast at the first detected failed expectation while it may otherwise wait for all expected messages to arrive before performing expectations verifications. Is by default true. Set to false to use behavior as in Camel 2.x. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **log** (producer (advanced)) | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging, then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | boolean |
| **reportGroup** (producer (advanced)) | A number that is used to turn on throughput logging based on groups of the size. |  | int |
| **resultMinimumWaitTime** (producer (advanced)) | Sets the minimum expected amount of time the assertIsSatisfied() will wait on a latch until it is satisfied. |  | long |
| **resultWaitTime** (producer (advanced)) | Sets the maximum amount of time the assertIsSatisfied() will wait on a latch until it is satisfied. |  | long |
| **retainFirst** (producer (advanced)) | Specifies to only retain the first nth number of received Exchanges. This is used when testing with big data, to reduce memory consumption by not storing copies of every Exchange this mock endpoint receives. Important: When using this limitation, then the getReceivedCounter() will still return the actual number of received message. For example if we have received 5000 messages and have configured to only retain the first 10 Exchanges, then the getReceivedCounter() will still return 5000 but there is only the first 10 Exchanges in the getExchanges() and getReceivedExchanges() methods. When using this method, then some of the other expectation methods is not supported, for example the expectedBodiesReceived(Object…​) sets a expectation on the first number of bodies received. You can configure both retainFirst and retainLast options, to limit both the first and last received. | \-1 | int |
| **retainLast** (producer (advanced)) | Specifies to only retain the last nth number of received Exchanges. This is used when testing with big data, to reduce memory consumption by not storing copies of every Exchange this mock endpoint receives. Important: When using this limitation, then the getReceivedCounter() will still return the actual number of received message. For example if we have received 5000 messages and have configured to only retain the last 20 Exchanges, then the getReceivedCounter() will still return 5000 but there is only the last 20 Exchanges in the getExchanges() and getReceivedExchanges() methods. When using this method, then some of the other expectation methods is not supported, for example the expectedBodiesReceived(Object…​) sets a expectation on the first number of bodies received. You can configure both retainFirst and retainLast options, to limit both the first and last received. | \-1 | int |
| **sleepForEmptyTest** (producer (advanced)) | Allows a sleep to be specified to wait to check that this mock really is empty when expectedMessageCount(int) is called with zero value. |  | long |
| **browseLimit** (advanced) | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | int |

## Usage

The Citrus endpoint acts as a producer-only endpoint. Routes send exchanges **to** `citrus:validate`, and the component validates each exchange using Citrus message validation.

> **Note**
> Spec setup (`validate()`, `validateAll()`, `when().receive()`) must complete before exchanges start arriving. For async consumers (SEDA, timer-based routes), ensure all validation chains are fully configured before starting the `CamelContext`.

The route under test sends to the endpoint like to any other, and the test sets the expectations on the endpoint, as the sections below show. In YAML:

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: citrus:validate
            parameters:
              messageType: json
```

### Validation modules

The component does not bundle Citrus validation modules. You must add the required validation module dependency for your message type to your test classpath:

 
| Dependency | Description |
| --- | --- |
| `citrus-validation-json` | JSON message validation with JsonPath expressions and JSON schema support |
| `citrus-validation-xml` | XML message validation with XPath expressions, XML schema (XSD/WSDL) and XSLT support |
| `citrus-validation-text` | Plain text message validation including binary (stream and base64) and gzip support |
| `citrus-validation-yaml` | YAML message validation |
| `citrus-validation-binary` | Binary message validation with stream comparison and base64 encoding |
| `citrus-validation-hamcrest` | Hamcrest matcher assertions for use with JsonPath and XPath expressions |

All modules use the `org.citrusframework` group ID. Refer to the [Citrus reference documentation](https://citrusframework.org/citrus/reference/html/) for detailed usage of each validation module.

### Citrus empowered message validation

Citrus uses a powerful template-based approach to message validation: you provide an expected message template and Citrus compares it against the received message using format-aware comparison. This brings several capabilities beyond simple string equality.

#### Ignore expressions

Use the `@ignore@` placeholder anywhere in an expected message template to skip validation of dynamic values such as timestamps, generated IDs, or correlation tokens. The element must be present, but its value is not checked.

```json
{
  "orderId": "@ignore@",
  "timestamp": "@ignore@",
  "status": "created"
}
```

This works across all supported message types — in XML element and attribute values, JSON property values, and YAML property values. The ignore placeholder can also replace an entire sub-object or element including its children.

For plain text messages, the `@ignore@` placeholder works on a positional basis — it matches a word-length character sequence at the exact position in the text. Use `@ignore(n)@` to ignore exactly _n_ characters when the value contains non-word characters:

```plaintext
Your current id is "@ignore@", it expires on 01/01/2030
```

This ignores the word following `id is "` based on the position of the ignore expression in the template. Because no character count is specified, Citrus ignores the entire word regardless of its length. The word boundary is determined by the first non-word character (whitespace, punctuation, etc.).

```plaintext
Your current id is "@ignore(12)@", it expires on @ignore(10)@
```

This ignores the next 12 characters starting at the position of the ignore expression in the template. This also includes whitespace and non-word characters (e.g. `Your current id is "1234/ 34567 D", it expires on 01/01/2030`).

#### Validation matchers

Citrus validation matchers are inline assertions embedded directly in the expected message template, surrounded by `@` markers. They work across all message formats (JSON, XML, YAML, plain text) and provide richer assertions than exact equality:

```json
{
  "name": "@equalsIgnoreCase('JOHN')@",
  "age": "@greaterThan(17)@",
  "email": "@matches('[a-z]+@[a-z]+\\.[a-z]+')@",
  "created": "@matchesDatePattern('yyyy-MM-dd')@",
  "id": "@isNumber()@",
  "token": "@startsWith('tk-')@",
  "status": "@contains('active')@"
}
```

You can also use `@variable('name')@` to extract the actual value into a Citrus test variable for later use, and `@assertThat(hamcrestMatcher)@` to use Hamcrest matchers inline (requires `citrus-validation-hamcrest`):

```json
{
  "count": "@assertThat(allOf(greaterThan(0), lessThan(100)))@",
  "type": "@assertThat(anyOf(equalTo(A), equalTo(B)))@"
}
```

#### JSON validation

Citrus JSON validation compares JSON object structures regardless of property order. It supports two modes configurable via `citrus.json.message.validation.strict`:

-   **Strict mode** (default): the received JSON must match the expected structure exactly — no additional properties or array items are allowed.
    
-   **Non-strict mode**: the expected JSON can be a subset of the received message — additional properties and array items in the received JSON are silently ignored. This is useful when you only want to verify specific fields.
    

JSON validation also supports:

-   **JsonPath expressions** for targeted field validation without specifying the full message body
    
-   **JSON schema validation** against JSON Schema V3/V4 definitions
    
-   **`@ignore@` and validation matchers** within JSON values
    

#### XML validation

Citrus XML validation performs a structural DOM tree comparison that correctly handles:

-   **XML namespaces** with different prefixes — the comparison is namespace-aware, so `<ns1:element xmlns:ns1="…​">` and `<ns2:element xmlns:ns2="…​">` are treated as equivalent when they share the same namespace URI.
    
-   **XML schema validation** against XSD and WSDL definitions to verify structural correctness.
    
-   **XPath expressions** for targeted element validation, with full namespace support via namespace context configuration. This includes automatic namespace prefix resolution when the prefixes differ between the control template and the received message.
    
-   **`@ignore@` and validation matchers** within XML element values and attributes.
    

#### Plain text validation

Plain text validation performs exact string comparison with support for:

-   **Positional `@ignore@`** to skip dynamic word-length sequences at specific positions.
    
-   **`@ignore(n)@`** to skip exactly _n_ characters (useful for values with non-word characters).
    
-   **`@variable('name')@`** to extract values at specific positions into test variables.
    
-   **Whitespace normalization** (configurable) to ignore line separator differences (CR, LF, CRLF) or all whitespace.
    
-   **Gzip** and **binary/base64** content comparison via the respective message types.
    

#### YAML validation

YAML validation compares YAML documents structurally, similar to JSON validation:

-   **Strict/non-strict mode** — configurable via `citrus.yaml.message.validation.strict`.
    
-   **Path expressions** for ignoring specific elements in the YAML structure.
    
-   **`@ignore@` and validation matchers** within YAML values.
    

### Validation specification API

The endpoint provides a fluent API for specifying validation expectations. You can define a single validation that applies to all incoming exchanges, or specify individual validations for each exchange in sequence.

#### Single validation for all exchanges

Use `validateAll()` to define one validation specification that is applied to every exchange. The returned `MessageValidationSpec` provides a fluent API with `body()`, `header()`, and `validate()` methods:

```java
CitrusEndpoint citrus = context.getEndpoint("citrus:validate?messageType=json", CitrusEndpoint.class);
citrus.validateAll()
    .body("{\"status\": \"ok\"}")
    .header("operation", "test");
citrus.expectedMessageCount(3);

// All three exchanges are validated against the same spec
template.sendBodyAndHeader("direct:start", "{\"status\": \"ok\"}", "operation", "test");
template.sendBodyAndHeader("direct:start", "{\"status\": \"ok\"}", "operation", "test");
template.sendBodyAndHeader("direct:start", "{\"status\": \"ok\"}", "operation", "test");

citrus.assertIsSatisfied();
```

#### Per-exchange sequential validation

Use `validate()` to specify different validation expectations for the 1st, 2nd, 3rd, etc. exchange. Each call to `validate()` auto-increments the index, so specs are applied in order. Each incoming exchange triggers the next validation spec in sequence:

```java
CitrusEndpoint citrus = context.getEndpoint("citrus:validate?messageType=json", CitrusEndpoint.class);

citrus.validate().body("{\"event\": \"created\"}").header("action", "create");
citrus.validate().body("{\"event\": \"updated\"}").header("action", "update");
citrus.validate().body("{\"event\": \"deleted\"}").header("action", "delete");
citrus.expectedMessageCount(3);

template.sendBodyAndHeader("direct:start", "{\"event\": \"created\"}", "action", "create");
template.sendBodyAndHeader("direct:start", "{\"event\": \"updated\"}", "action", "update");
template.sendBodyAndHeader("direct:start", "{\"event\": \"deleted\"}", "action", "delete");

citrus.assertIsSatisfied();
```

You can also use `validate(index)` to target a specific exchange by its 1-based position.

Indexed specs (`validate()`, `validate(index)`, `when().receive()`) imply a minimum message count equal to the highest index, unless the test sets `expectedMessageCount(…​)` or a larger `expectedMinimumMessageCount(…​)`. So `assertIsSatisfied()` fails when fewer exchanges arrive.

When both `validate(index)` and `validateAll()` are configured, the indexed spec takes priority — it replaces `validateAll()` for that exchange entirely (the two are never combined). The `validateAll()` spec acts as a fallback for exchanges that have no matching indexed spec.

If an exchange arrives at an index with no matching indexed spec and no `validateAll()` fallback, the exchange passes through without validation. No failure is recorded by the endpoint. For the `validate` operation, unmatched exchanges are ignored silently. For the `receive` operation, no simulated response is applied and the exchange continues unchanged.

```java
citrus.validate(1).body("{\"event\": \"start\"}");
citrus.validateAll().body("{\"event\": \"progress\"}").header("type", "status");

// Exchange 1 → validated against validate(1) only (validateAll() is NOT applied)
// Exchange 2, 3, ... → validated against validateAll() (body + header)
```

### Receive operation (request/response simulation)

The `receive` operation extends the validation endpoint with response simulation. It uses a Gherkin-style fluent API to define what the endpoint expects to receive (`when`) and what it should respond with (`then`). This is useful for simulating backend services in route tests.

#### Basic usage

```java
CitrusEndpoint citrus = context.getEndpoint("citrus:receive/service?messageType=json", CitrusEndpoint.class);

// Define expected request and simulated response
citrus.when().receiveAll()
    .body("{\"action\": \"greet\"}")
    .then().respond()
    .body("{\"greeting\": \"Hello!\"}");
citrus.expectedMessageCount(1);

// Send a request and verify the response
Exchange result = template.send("direct:start", exchange -> {
    exchange.getIn().setBody("{\"action\": \"greet\"}");
});

citrus.assertIsSatisfied();
assertThat(result.getIn().getBody(String.class)).isEqualTo("{\"greeting\": \"Hello!\"}");
```

The route under test calls the simulated service like any other endpoint, and gets the simulated response as its body:

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: citrus:receive/service
            parameters:
              messageType: json
        - log:
            message: "Response: ${body}"
```

#### Gherkin-style API

The `when()` method returns a `WhenSpec` that provides a chained fluent syntax:

-   `when().receive(index).body(…​).then().respond()` — define validation and response for a specific exchange (1-based index)
    
-   `when().receive().body(…​).then().respond()` — auto-incrementing index for sequential exchanges
    
-   `when().receiveAll().body(…​).then().respond()` — define default validation and response for all exchanges
    
-   `then().send()` — alias for `respond()`
    

Both the `receive()` / `receiveAll()` spec and the `respond()` / `send()` spec support `body()` and `header()` methods.

#### Per-exchange request/response

You can define different request expectations and responses for each exchange in sequence:

```java
CitrusEndpoint citrus = context.getEndpoint("citrus:receive/service?messageType=json", CitrusEndpoint.class);

citrus.when().receive(1).body("{\"action\": \"create\"}")
    .then().respond().body("{\"id\": \"1\", \"status\": \"created\"}");

citrus.when().receive(2).body("{\"action\": \"update\"}")
    .then().respond().body("{\"id\": \"1\", \"status\": \"updated\"}");

citrus.expectedMessageCount(2);
```

Indexed specs take priority over `receiveAll()` for both request validation and response simulation. When a specific exchange has no indexed spec, the `receiveAll()` spec is used as a fallback.

#### Response with headers

```java
citrus.when().receiveAll()
    .body("{\"action\": \"greet\"}")
    .then().respond()
    .body("{\"greeting\": \"Hello!\"}")
    .header("Content-Type", "application/json")
    .header("X-Status", "ok");
```

#### Citrus variables in responses

Exchange properties and exchange variables are available as Citrus test variables in response templates. This enables dynamic response generation based on the incoming request context:

```java
citrus.when().receiveAll()
    .body("{\"action\": \"greet\", \"name\": \"@ignore@\"}")
    .then().respond()
    .body("{\"greeting\": \"Hello ${userName}!\"}")
    .header("X-Correlation-Id", "${correlationId}");
```

#### Response-only mode

When you only need response simulation without request validation, omit the body on `receive()`:

```java
CitrusEndpoint citrus = context.getEndpoint("citrus:receive/responder", CitrusEndpoint.class);

citrus.when().receive().then().respond()
    .body("OK")
    .header("status", "200");
citrus.expectedMessageCount(1);
```

### Error handling and redelivery

The two operations handle validation failures differently with respect to Camel’s error handling:

-   **`validate` operation** — validation failures are captured internally and the exception is cleared from the exchange. Camel’s `onException` handlers and redelivery policies do **not** trigger. Failures surface only when `assertIsSatisfied()` is called.
    
-   **`receive` operation** — validation failures remain on the exchange as an exception. Camel’s `onException` handlers and redelivery policies **do** trigger, which matches the expected behavior for a request/response endpoint where callers need to see errors.
    

> **Note**
> Each redelivery attempt counts as a new exchange in the mock counter. So if a `receive(1)` spec fails and Camel redelivers, the retry is exchange 2 and `receive(2)` applies to it — not `receive(1)` again. If no spec exists for the retry, it passes without validation and the earlier failure is not recorded, so set `expectedMessageCount(…​)` to catch the extra exchange.

### Exchange properties and variables as Citrus variables

All exchange properties and exchange variables are automatically propagated to the Citrus test context as test variables. This enables the use of Citrus variable placeholders (\`${variableName}\`) in expected message templates and response bodies.

Variables extracted by Citrus during validation (e.g., via `@variable('name')@`) are written back to the exchange as exchange variables, making them available for downstream route processing.

### Path validation

Use the `validate()` method on a `MessageValidationSpec` to add Citrus validation context builders such as JsonPath or XPath expressions. These are provided by the Citrus `DefaultValidations` class:

```java
CitrusEndpoint citrus = context.getEndpoint("citrus:validate?messageType=json", CitrusEndpoint.class);
citrus.validateAll().validate(new DefaultValidations().jsonPath()
    .expression("$.user.name", "John")
    .expression("$.user.age", "30"));
```

```java
CitrusEndpoint citrus = context.getEndpoint("citrus:validate?messageType=xml", CitrusEndpoint.class);
citrus.validateAll().validate(new DefaultValidations().xpath()
    .expression("/order/status", "completed")
    .expression("/order/total", "99.99"));
```
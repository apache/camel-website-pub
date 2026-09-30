# Switch

**Since Camel 4.23**

Switch selects one destination from a table declared by the route author. The selector can use any Camel expression language. Its result selects a case; it cannot supply a new endpoint URI.

Use Switch for literal value dispatch. Use [Choice](choice-eip.md) for predicates, ranges, overlapping conditions, or nested processing steps. A case can send to a `direct:` route when more processing is needed. Use [To D](toD-eip.md) when the endpoint URI itself must be calculated dynamically.

## Options

The Switch eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **selector** | **Required** Expression evaluated once per entry. Returns a scalar value to match against the literal cases. |  | ExpressionSubElementDefinition |
| **case** | Literal cases. Duplicate values are rejected at startup, ignoring case. |  | List |
| **otherwise** | Fixed fallback URI for null or unmatched selector results. Without a fallback processing continues. |  | SwitchOtherwiseDefinition |

## Scalar selectors

The selector is evaluated once on each entry. Scalar results are converted to strings and matched case-insensitively using the English locale. An empty string is a valid literal. An asterisk is literal, not a wildcard. Duplicate normalized values are rejected at startup.

Map, collection and array results are rejected with an `IllegalArgumentException`. They follow normal Camel error handling and do not select `otherwise`.

### Route from a header

This route reads the `department` header. The body is passed unchanged to the selected destination. The examples on this page are independent; load one at a time and connect the `direct:` destinations to your application’s handling routes.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:tickets")
    .doSwitch(header("department"))
        .doCase("billing", "direct:billing")
        .doCase("technical", "direct:technical")
        .otherwise("direct:review")
    .end();
```

```xml
<route xmlns="http://camel.apache.org/schema/spring">
    <from uri="direct:tickets"/>
    <switch>
        <selector><header>department</header></selector>
        <case value="billing" uri="direct:billing"/>
        <case value="technical" uri="direct:technical"/>
        <otherwise uri="direct:review"/>
    </switch>
</route>
```

```yaml
- route:
    from:
      uri: direct:tickets
      steps:
        - switch:
            selector:
              header:
                expression: department
            case:
              - value: billing
                uri: direct:billing
              - value: technical
                uri: direct:technical
            otherwise:
              uri: direct:review
```

Send a message to any of these equivalent routes with a `ProducerTemplate`:

```java
template.sendBodyAndHeader("direct:tickets", "Please check this invoice",
    "department", "BILLING");
```

 
| Header value | Destination |
| --- | --- |
| `billing` or `BILLING` | `direct:billing` |
| `technical` | `direct:technical` |
| `sales` or an absent header | `direct:review` |

A null or unmatched result uses `otherwise`. Without `otherwise`, the exchange continues after Switch. Selector failures follow normal Camel error handling and never select the fallback. Streams are reset after selector evaluation when stream caching is enabled. Loops and retries that enter Switch again evaluate the selector again; results are not cached across entries.

### Connect the example destinations

For a local demonstration, the destination routes can simply log the message. Load these routes alongside one of the examples above; replace the logging steps with the application’s processing when integrating the example.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:billing").log("Billing: ${body}");
from("direct:technical").log("Technical: ${body}");
from("direct:review").log("Review: ${body}");
```

```xml
<routes xmlns="http://camel.apache.org/schema/xml-io">
    <route><from uri="direct:billing"/><log message="Billing: ${body}"/></route>
    <route><from uri="direct:technical"/><log message="Technical: ${body}"/></route>
    <route><from uri="direct:review"/><log message="Review: ${body}"/></route>
</routes>
```

```yaml
- route:
    from:
      uri: direct:billing
      steps:
        - log: "Billing: ${body}"
- route:
    from:
      uri: direct:technical
      steps:
        - log: "Technical: ${body}"
- route:
    from:
      uri: direct:review
      steps:
        - log: "Review: ${body}"
```

## Destinations and management

Case and fallback URIs support property placeholders resolved at startup. Simple expressions in URIs are rejected. In YAML, both cases and `otherwise` accept `uri` plus `parameters`:

```yaml
case:
  - value: orders
    uri: kafka
    parameters:
      topic: orders
otherwise:
  uri: direct
  parameters:
    name: review
```

Each case has an identity for tracing, debugging and management. The Switch MBean’s `extendedInformation` table reports case IDs, literal values, destination URIs and selection counts. URIs are masked when management masking is enabled (the default). These counts indicate case selection, not successful delivery. `UnmatchedCount` also records unmatched results when no fallback is configured.
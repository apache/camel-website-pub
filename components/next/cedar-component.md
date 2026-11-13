# Cedar

**Since Camel 4.24**

**Only producer is supported**

Cedar evaluates embedded authorization policies using `com.cedarpolicy:cedar-java:4.11.0` and its bundled JNI engine. It supports a producer and an `AuthorizationPolicy` bean, preserves the application body, and makes no authorization-server request. The caller supplies principal, action, resource, explicit optional context, and relevant entity data. It complements [SPIFFE identity](spiffe-component.md) and [OpenFGA relationships](openfga-component.md). AWS Verified Permissions and remote policy servers are separate integrations.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-cedar</artifactId>
    <version>x.x.x</version>
</dependency>
```

## URI format

```text
cedar:authorize[?options]
```

`policiesResource` and `schemaResource` are required `classpath:` or `file:` resource URIs containing Cedar policy text and Cedar schema text. `entitiesResource` optionally supplies static Cedar entity JSON through the same local resource schemes. Remote resource schemes are rejected; this preview does not manage HTTP resource-fetch deadlines. `principal`, `action` and `resource` are required configured `Expression` references returning an SDK `EntityUID` or a canonical UID string, for example `Action::"read"`. An optional `context` expression explicitly selects a POJO or map; nothing implicitly reads the body or forwards headers. Expression references use normal registry binding, for example `principal=#bean:workloadPrincipal`. Policy selection and input expressions are fixed by configuration; there are no dispatch headers.

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

The Cedar component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Cedar endpoint is configured using URI syntax:

cedar:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | **Required** Operation to perform. Only authorize is supported. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | **Required** Required configured expression yielding a Cedar EntityUID or canonical entity UID string. |  | Expression |
| **context** (producer) | Optional explicit expression yielding a context object or map. No implicit body extraction. |  | Expression |
| **entitiesResource** (producer) | Optional classpath: or file: static Cedar entity JSON resource URI. Published coherently with policy and schema. |  | String |
| **entityProvider** (producer) | Optional request scoped entity JSON provider. Provider owns its bounded I/O and freshness contract. |  | CedarEntityProvider |
| **maxResourceSize** (producer) | Maximum bytes per policy, schema, entity resource, explicit context and provider entity JSON. Reload fails without replacing the active revision if exceeded. | 1048576 | int |
| **policiesResource** (producer) | **Required** Required classpath: or file: Cedar policy text resource URI. Loaded and schema validated at startup and explicit reload. |  | String |
| **principal** (producer) | **Required** Required configured expression yielding a Cedar EntityUID or canonical entity UID string. |  | Expression |
| **resource** (producer) | **Required** Required configured expression yielding a Cedar EntityUID or canonical entity UID string. |  | Expression |
| **schemaResource** (producer) | **Required** Required classpath: or file: Cedar schema text resource URI. Used for policy, entity and request validation. |  | String |
| **strict** (producer) | Reject evaluation errors even when the raw engine decision is allow. False explicitly honors Cedar skip-on-error semantics and retains diagnostics. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Decision and enforcement

The producer records an immutable `CedarAuthorizationResult` in the `CamelCedarAuthorizationResult` exchange property. The body, including stream bodies, remains unchanged unless an explicitly configured expression or provider consumes it. Every evaluation clears the previous result property and a same-named inbound header.

 
| Result member | Meaning |
| --- | --- |
| `outcome` | Effective `ALLOW`, `DENY` or `ERROR`. |
| `engineDecision` | Cedar’s raw `ALLOW` or `DENY`; `UNKNOWN` if no engine decision was produced. |
| `policyIds` | Determining policy identifiers from the engine. |
| `diagnostics` | Evaluation policy IDs and error codes. Raw error messages, policy text and request values are omitted. |
| `revision` | SHA-256 revision of the exact policy, schema and static entity content used for this exchange. |

Cedar has default deny and forbid precedence. Its native semantics skip erroneous policies, so an erroneous forbid and a matching permit can produce a raw allow. The default `strict=true` returns effective `ERROR` whenever evaluation diagnostics are present, including that case. Explicit `strict=false` honors the raw decision and retains diagnostics; use it only when native skip-on-error semantics are intended. Request/schema/entity failures and engine failures remain `ERROR` in both modes. There is no `failOpen` option.

The producer returns structured results for callers to inspect; it does not enforce access itself. `CedarSecurityPolicy` uses the same evaluator and throws `CamelAuthorizationException` on effective deny or error, preventing the guarded processor from running. Its denial message contains the effective outcome, and the result remains available to error handling. It sets `Exchange.AUTHENTICATION_FAILURE_POLICY_ID` to `CedarSecurityPolicy` on rejection and clears that header before the next check. Result `toString()` omits input and diagnostic contents. An evaluation failure of one exchange is logged at `WARN` with the exception class, or with the evaluator’s own reason when it rejected the input (an expression that did not yield an entity UID, a null or oversized context, invalid provider entity data); the SDK’s message is never logged. Do not use principal/resource values as metric labels or log an entire exchange to diagnose a decision.

## Validated resources and reload

Startup loads bounded resources, parses policy and schema, validates their compatibility, and validates static entities. Every authorization enables SDK request validation; the entities a provider adds are validated against the same schema for that request, while the static entities were validated when the snapshot was loaded. `maxResourceSize` defaults to 1 MiB per resource, explicit context JSON, and provider entity JSON. Resources close after loading; a Rust toolchain and a remote authorization service are not required.

An endpoint’s `reload()` explicitly loads and validates a complete candidate before publishing it atomically. A failed reload throws a sanitized exception and keeps the previous revision active. Its message, also logged at `WARN`, names the step (reading, parsing or validating), the option (`policiesResource`, `schemaResource` or `entitiesResource`), the exception class and, for a failed policy validation, the policy identifiers and error kinds; the SDK message, which can contain policy text or entity attributes, is neither logged nor kept as the cause. A failed first start says that no revision is active. Concurrent exchanges use a single old or new immutable snapshot, never partially mutated policy/schema/entity collections. No SDK `PolicySet` or mutable entity collection is exposed. There is no filesystem watcher or per-message resource reload.

`CedarSecurityPolicy.reload()` reloads its active evaluator. One policy bean can guard several route segments in the same CamelContext; the last segment stopping releases the evaluator. Use separate policy beans for separate CamelContexts. Stopping and starting an endpoint or policy reloads resources and rechecks native availability. JNI loading is JVM-scoped and the SDK has no per-engine native close operation.

An optional `CedarEntityProvider` returns request-scoped Cedar entity JSON:

```java
CedarEntityProvider provider = exchange -> entityRepository.loadCedarEntities(exchange);
```

The provider owns its I/O deadlines, cache freshness and authorization-data provenance. Provider entities are combined with static entities for this request; duplicate UIDs are rejected. Malformed or schema-invalid provider data produces `ERROR`. No exchange, provider data or credential is retained in the result.

## SPIFFE identity and DSL examples

Authenticate the transport first. A `SpiffeSecurityPolicy` on a consumer configured for verified mutual TLS records `CamelSpiffePeerId` as an exchange property. These examples enter `direct:verifiedWorkload` only from that authenticated route segment:

```java
from("netty-http:https://0.0.0.0:8443/orders?sslContextParameters=#spiffeSsl")
    .policy(spiffePolicy) // configured to verify/authorize the peer certificate
    .to("direct:verifiedWorkload");
```

`spiffeSsl` and `spiffePolicy` must be configured as described in [SPIFFE mutual TLS](spiffe-component.md). An untrusted message header is not a verified identity. Do not route unauthenticated callers directly to the internal entry point or copy caller headers into the identity property.

The supplied `CedarEntityUidExpression` constructs UID values as data from a configured entity type and exactly one constant `id` or `exchangeProperty`. It safely handles quotes in identifiers; never concatenate an external identifier into policy text.

Use these files on the classpath:

```cedar
// authz.cedar
permit(principal == User::"spiffe://example.org/frontend",
       action == Action::"read", resource == Doc::"budget");
```

```cedar
// authz.cedarschema
entity User;
entity Doc;
action "read" appliesTo {principal: User, resource: Doc, context: {}};
```

### Java

```java
CedarEntityUidExpression principal = new CedarEntityUidExpression();
principal.setEntityType("User");
principal.setExchangeProperty("CamelSpiffePeerId");
CedarEntityUidExpression action = new CedarEntityUidExpression();
action.setEntityType("Action");
action.setId("read");
CedarEntityUidExpression resource = new CedarEntityUidExpression();
resource.setEntityType("Doc");
resource.setId("budget");
CedarSecurityPolicy cedar = new CedarSecurityPolicy();
cedar.setPoliciesResource("classpath:authz.cedar");
cedar.setSchemaResource("classpath:authz.cedarschema");
cedar.setPrincipal(principal);
cedar.setAction(action);
cedar.setResource(resource);
from("direct:verifiedWorkload").policy(cedar).to("bean:orderService");
```

For decision-only evaluation, register the three expressions and use:

```java
from("direct:verifiedWorkload")
    .to("cedar:authorize?policiesResource=classpath:authz.cedar"
        + "&schemaResource=classpath:authz.cedarschema&principal=#bean:principal"
        + "&action=#bean:action&resource=#bean:resource")
    .process(exchange -> {
        CedarAuthorizationResult result = exchange.getProperty(
            CedarConstants.AUTHORIZATION_RESULT, CedarAuthorizationResult.class);
        // The route decides what to do with ALLOW, DENY and ERROR.
    });
```

### XML

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:camel="http://camel.apache.org/schema/spring">
  <bean id="principal" class="org.apache.camel.component.cedar.CedarEntityUidExpression">
    <property name="entityType" value="User"/>
    <property name="exchangeProperty" value="CamelSpiffePeerId"/>
  </bean>
  <bean id="action" class="org.apache.camel.component.cedar.CedarEntityUidExpression">
    <property name="entityType" value="Action"/><property name="id" value="read"/>
  </bean>
  <bean id="resource" class="org.apache.camel.component.cedar.CedarEntityUidExpression">
    <property name="entityType" value="Doc"/><property name="id" value="budget"/>
  </bean>
  <bean id="cedarPolicy" class="org.apache.camel.component.cedar.CedarSecurityPolicy">
    <property name="policiesResource" value="classpath:authz.cedar"/>
    <property name="schemaResource" value="classpath:authz.cedarschema"/>
    <property name="principal" ref="principal"/><property name="action" ref="action"/>
    <property name="resource" ref="resource"/>
  </bean>
  <camel:camelContext>
    <camel:route>
      <camel:from uri="direct:verifiedWorkload"/>
      <camel:policy ref="cedarPolicy"><camel:to uri="bean:orderService"/></camel:policy>
    </camel:route>
  </camel:camelContext>
</beans>
```

### YAML

```yaml
- beans:
    - name: principal
      type: org.apache.camel.component.cedar.CedarEntityUidExpression
      properties:
        entityType: User
        exchangeProperty: CamelSpiffePeerId
    - name: action
      type: org.apache.camel.component.cedar.CedarEntityUidExpression
      properties: {entityType: Action, id: read}
    - name: resource
      type: org.apache.camel.component.cedar.CedarEntityUidExpression
      properties: {entityType: Doc, id: budget}
    - name: cedarPolicy
      type: org.apache.camel.component.cedar.CedarSecurityPolicy
      properties:
        policiesResource: classpath:authz.cedar
        schemaResource: classpath:authz.cedarschema
        principal: '#bean:principal'
        action: '#bean:action'
        resource: '#bean:resource'
- from:
    uri: direct:verifiedWorkload
    steps:
      - policy:
          ref: cedarPolicy
          steps:
            - to: bean:orderService
```

## Deployment targets

This preview uses Cedar Java 4.11.0’s `uber` classifier, including its native library. Execution is tested on Linux amd64 with glibc and Java 21. The artifact also packages Linux arm64 GNU/glibc, macOS amd64/arm64, and Windows amd64 libraries; packaging inspection is not runtime validation of those targets. Stock musl Linux, ppc64le and s390x have no matching bundled library. GraalVM native image is not validated or advertised by this component.

Native extraction needs an appropriate writable, executable location. Use a tested glibc JVM image and verify startup in your deployment image; a read-only or `noexec` temporary filesystem requires an explicit native-loading configuration following the Cedar Java and JNE documentation. Startup errors name the exception class, the operating system and the architecture when the native library cannot be initialized, and the engine version when the SDK JAR declares one. Cedar uses Jackson 2 in its normal packages; it does not use Camel’s Jackson 3 serializer. The first implementation does not modify the SDK’s JVM-global native cache settings.
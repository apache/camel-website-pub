# MuleSoft migration

Camel Kit migrates MuleSoft Mule 3.x and 4.x applications to Camel 4 with YAML DSL routes. It understands Mule XML flows and sub-flows, DataWeave 1.0 and 2.0 scripts, connectors, error handlers, choice routers, scatter-gather and flow references. The shared steps, the migration package, the approval scope and the evidence rules are described in [Migration workflow](migration.md); this page covers what is specific to Mule.

## What is parsed

 
| Artifact | Location |
| --- | --- |
| Flow and sub-flow XML, global configuration | Mule XML files in the selected source boundary, typically `src/main/mule/` |
| DataWeave scripts | `.dwl` files and `<ee:transform>` or `<dw:transform-message>` elements |
| Connector configurations | XML configuration elements |
| Dependencies | `pom.xml` (`org.mule` and `com.mulesoft` groups identify the platform and version) |

Mule XML files are detected by the `mulesoft.org/schema/mule` namespace. When the project graph is built (see [Graph intelligence](graph.md)), the Mule and DataWeave parsers record every flow, sub-flow, connector, endpoint, transform and error handler as graph nodes, so the migration gets the flow topology, the connectors used per flow, the sub-flow call chains and the DataWeave complexity without walking the XML by hand. DataWeave scripts are analyzed for version declarations, input and output content types, function definitions and field access patterns to identify transformations that need manual attention.

## Evidence and retirement

`migration-analysis.md` records each Mule behavioral assumption and evidence gap with a stable ID, the affected flow or interface, the source evidence, a `Confirmed`, `Inferred` or `Unknown` status, the impact if the assumption is false, and the validation still required. API compatibility is not assumed just because a listener path or a connector has a plausible Camel mapping.

The source-retirement audit corroborates entry roots from the parsed message sources and follows constant `flow-ref` targets to flows and sub-flows. Dynamic flow names, custom modules, parse failures, missing domain or shared configuration, and callers outside the selected boundary stay **Unknown**. An `Incremental candidate` strategy requires current evidence, or explicit operator confirmation, of an existing external control such as an operator-controlled gateway, a deterministic broker partition, a mutually exclusive source directory or a pre-consumption routing predicate; a listener declaration or an in-flow predicate after consumption is not a traffic seam.

## Component mapping

The agent maps every Mule component to a Camel equivalent from the mapping guide shipped with the skill and verifies each target and its options in the catalog for the selected Camel version and runtime.

  
| Mule component | Camel component | Notes |
| --- | --- | --- |
| HTTP Listener | `platform-http` (`camel-platform-http`) | The listener port moves to the runtime’s server property (`camel.server.port` with `camel.server.enabled=true` on Camel Main, `server.port` on Spring Boot, `quarkus.http.port` on Quarkus); `platform-http` has no host or port option |
| HTTP Request | `http` / `https` (`camel-http`) | Outbound calls |
| Database select, insert, update, delete | `sql` (`camel-sql`) | `jdbc` for batch operations |
| File, FTP, SFTP | `file`, `ftp`, `sftp` | Direct equivalents |
| JMS, ActiveMQ, AMQP | `jms`, `activemq`, `amqp` | Queues and topics |
| VM queue | `seda` | In-memory, not persistent across restarts |
| Scheduler | `timer` or `quartz` | `quartz` for cron expressions |
| Kafka | `kafka` | Direct equivalent |
| Email (Mule 4 Email connector, Mule 3 transports) | `smtp`, `smtps`, `imap`, `imaps`, `pop3`, `pop3s` (all from `camel-mail`) | The scheme follows the Mule connection type; `mail` is the artifact name, not a scheme |
| Salesforce connector | `salesforce` |  |
| SOAP web service | `cxf` |  |
| REST consumer (RAML) | `rest` DSL with `openapi-java` | Import the OpenAPI specification |
| Choice router, `when`, `otherwise` | `choice` EIP |  |
| Scatter-Gather | `multicast` EIP | Parallel dispatch with an aggregation strategy |
| For Each, Splitter | `split` EIP |  |
| Until Successful | error handler with `redeliveryPolicy` |  |
| Async | `threads` EIP |  |
| Sub Flow, Flow Reference | `direct:` route |  |
| Set Payload, Set Variable, Set Property | `setBody`, `setHeader`, `setProperty` | Mule variables become exchange headers |
| Enrich, Poll Enrich | `enrich`, `pollEnrich` |  |
| Aggregator, Filter, Idempotent Filter, Wire Tap | `aggregate`, `filter`, `idempotentConsumer`, `wireTap` |  |
| Object to JSON / XML | `marshal` with `jackson` or `jaxb` |  |
| DataWeave Transform | DataMapper: inline Groovy or XSLT (`xslt-saxon`) | See [DataWeave](#dataweave) |
| Error handler, dead letter queue, retry | `doTry`/`doCatch`, Dead Letter Channel, `redeliveryPolicy` |  |

Infrastructure beans such as data sources and connection factories are configured through the Forage configuration ladder (see [Forage configuration catalog](forage.md)) before `camel.beans.*` is considered.

Proprietary connectors have no direct equivalent. The agent stops and asks you to choose a replacement, one connector at a time, and verifies the choice in the catalog:

 
| Mule connector | Suggested alternatives |
| --- | --- |
| Anypoint MQ | Amazon SQS, Azure Service Bus, RabbitMQ (`spring-rabbitmq`), ActiveMQ |
| Object Store | Infinispan, Redis, Caffeine cache, JPA |
| SAP connector | `camel-sap` if SAP JCo is licensed, otherwise SAP REST or SOAP APIs |
| Workday, NetSuite, Zuora, Marketo, Veeva, Anaplan, Siebel | The vendor’s REST or SOAP API through `http` or `cxf` |
| ServiceNow | `servicenow`, after checking the API coverage |
| Microsoft Dynamics 365 | `http` with the REST API, or `olingo4` |

## DataWeave

DataWeave scripts are not translated line by line. The agent first extracts the semantic field mapping, presents it for confirmation, and records it in the design specification. DataMapper then selects the engine from the mapping, not from the script: inline Groovy when both schemas are absent or the mapping has fewer than 20 leaf fields, XSLT only when the mapping has at least 20 leaf fields and at least one schema. DataWeave constructs without a simple equivalent are recorded as custom mapping or processor actions. Mule 3 uses DataWeave 1.0 (`%dw 1.0`, `flowVars`, `message.inboundProperties`); Mule 4 uses DataWeave 2.0 (`%dw 2.0`, `vars`, `attributes`), and the guide covers both syntaxes.

## Examples

### HTTP listener to database

Mule XML

```xml
<flow name="get-customer">
  <http:listener path="/customer/{id}"/>
  <db:select config-ref="dbConfig">
    <db:sql>SELECT * FROM customers WHERE id = :id</db:sql>
    <db:input-parameters>
      #[{'id': attributes.uriParams.id}]
    </db:input-parameters>
  </db:select>
</flow>
```

Camel YAML

```yaml
- route:
    id: get-customer
    from:
      uri: "platform-http:/customer/{id}"
      parameters:
        httpMethodRestrict: GET
      steps:
        - to: "sql:SELECT * FROM customers WHERE id = :#${header.id}"
```

### Scatter-gather

Mule XML

```xml
<scatter-gather>
  <route>
    <http:request url="http://inventory-service/check"/>
  </route>
  <route>
    <http:request url="http://pricing-service/price"/>
  </route>
</scatter-gather>
```

Camel YAML

```yaml
- multicast:
    parallelProcessing: true
    aggregationStrategy: "#class:org.apache.camel.processor.aggregate.GroupedBodyAggregationStrategy"
    steps:
      - to: http://inventory-service/check
      - to: http://pricing-service/price
```

### Sub-flow and flow reference

Mule XML

```xml
<flow name="main-flow">
  <http:listener path="/api"/>
  <flow-ref name="validate-order"/>
</flow>
<sub-flow name="validate-order">
  <validation:is-not-null value="#[payload.orderId]"/>
</sub-flow>
```

Camel YAML

```yaml
- route:
    id: main-flow
    from:
      uri: "platform-http:/api"
      parameters:
        httpMethodRestrict: POST
      steps:
        - unmarshal:
            json: {}
        - to: "direct:validate-order"
- route:
    id: validate-order
    from:
      uri: "direct:validate-order"
      steps:
        - validate:
            simple: "${body[orderId]} != null"
```

The JSON body is unmarshalled to a map before the sub-route reads it; a bean-style `body.orderId` expression on the raw JSON string would fail.

### Choice router

Conditional routing on a JSON payload that an earlier step unmarshalled to a map.

Mule XML

```xml
<choice>
  <when expression="#[payload.amount > 1000]">
    <flow-ref name="high-value-processing"/>
  </when>
  <otherwise>
    <flow-ref name="standard-processing"/>
  </otherwise>
</choice>
```

Camel YAML

```yaml
- choice:
    when:
      - simple: ${body[amount]} > 1000
        steps:
          - to: direct:high-value-processing
    otherwise:
      steps:
        - to: direct:standard-processing
```

### DataWeave to XSLT

This mapping has at least 20 leaf fields and both schemas, so DataMapper selected XSLT; the excerpt shows a few fields.

DataWeave

```dataweave
%dw 2.0
output application/xml
---
{
  Order: {
    ID: payload.orderId,
    Customer: payload.customer.name,
    Items: payload.items map {
      Item: {
        SKU: $.sku,
        Qty: $.quantity
      }
    }
  }
}
```

XSLT

```xml
<xsl:stylesheet version="2.0">
  <xsl:template match="/">
    <Order>
      <ID><xsl:value-of select="/order/orderId"/></ID>
      <Customer><xsl:value-of select="/order/customer/name"/></Customer>
      <Items>
        <xsl:for-each select="/order/items/item">
          <Item>
            <SKU><xsl:value-of select="sku"/></SKU>
            <Qty><xsl:value-of select="quantity"/></Qty>
          </Item>
        </xsl:for-each>
      </Items>
    </Order>
  </xsl:template>
</xsl:stylesheet>
```
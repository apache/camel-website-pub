# BizTalk migration

Camel Kit migrates Microsoft BizTalk Server applications (2004 through 2020) to Camel 4 with YAML DSL routes. It parses orchestrations, maps, pipelines, schemas and port bindings into migration candidates; unsupported or ambiguous constructs are kept explicit for manual review. The shared steps, the migration package, the approval scope and the evidence rules are described in [Migration workflow](migration.md); this page covers what is specific to BizTalk.

## What is parsed

  
| Artifact | Extension | Content |
| --- | --- | --- |
| Orchestrations | `.odx` | Business process shapes; 38 shape element names are recognized, and the mapping guide gives each one a Camel equivalent, marks Suspend as not supported and Group and RoleLinkDeclaration as having no runtime impact |
| Maps | `.btm` | Transformations with functoids; 45 functoid identifiers are recognized and classified into seven categories (string, math, date, logical, looping, scripting, advanced) |
| Pipelines | `.btp` | Receive and send processing stages and their component chains |
| Schemas | `.xsd` | Message formats |
| Bindings | `.xml` | Port configurations and adapter types, including UTF-16 exports from the BizTalk Administration Console |

BizTalk artifacts are detected by the `schemas.microsoft.com/BizTalk` namespace. When the project graph is built (see [Graph intelligence](graph.md)), the BizTalk parsers record the adapters used per orchestration, the map functoid complexity, the pipeline component chains and the port bindings, which lets the migration spot proprietary patterns such as scripting functoids, custom pipeline components and WCF-specific configuration early.

## Evidence and retirement

`migration-analysis.md` records each BizTalk behavioral assumption and evidence gap with a stable ID, the affected orchestration or interface, the source evidence, a `Confirmed`, `Inferred` or `Unknown` status, the impact if the assumption is false, and the validation still required. Adapter similarity or a plausible receive-port mapping is not treated as proof of compatibility.

The source-retirement audit corroborates entry roots from Receive Locations and activating receives in the deployment bindings, then follows constant orchestration calls and supported artifact references. Missing bindings or assemblies, Direct Binding or subscription behaviour not proven by bindings, dynamic .NET calls, parse failures and callers outside the selected boundary stay **Unknown**. An `Incremental candidate` strategy requires current evidence, or explicit operator confirmation, of operator-controlled external routing or of a mutually exclusive Receive Location or subscription filter that assigns traffic before consumption; bindings can corroborate what is deployed, but are at most **Inferred** evidence that a control is operative today.

## Adapter mapping

For each adapter the agent proposes a catalog-verified Camel component when a direct mapping exists; otherwise it records the gap and asks for a decision.

  
| BizTalk adapter | Camel component | Notes |
| --- | --- | --- |
| FILE | `file` |  |
| FTP, FTPS, SFTP | `ftp`, `ftps`, `sftp` (`camel-ftp`) |  |
| HTTP, HTTPS | Receive: `platform-http`; send: `http` / `https` | The direction determines the component |
| SOAP, WCF-BasicHttp, WCF-WSHttp | Receive: `platform-http` with `cxf`; send: `cxf` | WSDL-first services; WS-Security through CXF interceptors |
| WCF-NetTcp | `netty` | Binary TCP, needs a custom codec |
| SQL Server, Oracle, IBM Db2 | `sql` (`camel-sql`) | `jdbc` for batch operations |
| MSMQ | Decision required | See below |
| MQ Series | `jms` with the IBM MQ client |  |
| SMTP, POP3, IMAP | `smtp`, `pop3`, `imap` (`camel-mail`) | `mail` is the artifact name, not a scheme |
| Azure Service Bus, Event Hubs, Blob Storage | `azure-servicebus`, `azure-eventhubs`, `azure-storage-blob` | BizTalk 2016 or later |

MSMQ has no Camel equivalent. When it is found, the agent asks you to choose ActiveMQ Artemis through `jms`, RabbitMQ through `spring-rabbitmq`, Azure Service Bus, or to drop that processing step from the design, and records the decision. Infrastructure beans such as data sources and connection factories are configured through the Forage configuration ladder (see [Forage configuration catalog](forage.md)).

## Orchestration shapes

 
| BizTalk shape | Camel equivalent |
| --- | --- |
| Receive (activating) | `from` consumer, the route entry point |
| Send, Invoke | `to` producer |
| Construct Message, Message Assignment | `setBody`, `setHeader` |
| Transform | DataMapper mapping, inline Groovy or XSLT as selected (see [Maps and functoids](#maps)) |
| Decide, Switch | `choice` EIP |
| Loop, While, Until | `loop` EIP |
| ForEach | `split` EIP |
| Parallel Actions | `multicast` with `parallelProcessing` |
| Listen | `choice` with a timeout |
| Call Orchestration | `to("direct:…​")` |
| Start Orchestration | `wireTap` or `to("seda:…​")` |
| Scope, Catch, Throw, Terminate | `doTry`, `doCatch`, `throwException`, `stop` |
| AtomicTransaction | `transacted` |
| LongRunningTransaction, CompensationScope, Compensate | Saga EIP and its compensation |
| Delay | `delay` EIP |
| Expression | `process` or a Groovy script |
| Variable and correlation declarations | `setVariable`, `setHeader`, `correlationExpression` |
| CallRules, CallPolicy | `bean` or a rules engine integration |
| Suspend | Not supported: BizTalk dehydration has no Camel equivalent; the agent flags it for a redesign, for example a Dead Letter Channel or a manual hold pattern |
| Group, RoleLinkDeclaration | No runtime impact |

## Pipelines

-   Receive pipeline
    
-   Send pipeline
    

 
| Component | Camel pattern |
| --- | --- |
| XML Disassembler | Candidate: `split` plus the Jackson XML data format with a POJO or list model; otherwise a generated or custom processor |
| Flat File Disassembler | Candidate: Flatpack with a definition or Bindy with an annotated model; otherwise a custom processor |
| JSON Decoder | Jackson JSON data format |
| XML Validator | `validator:schema.xsd` |
| MIME Decoder | MIME multipart data format (`camel-mail`) |
| S/MIME Decoder | Manual, catalog-verified crypto or mail implementation after certificate and keystore review |
| Party Resolution, custom components | `bean` or `process`, re-implemented in Groovy or Java |

 
| Component | Camel pattern |
| --- | --- |
| XML Assembler | Candidate: Jackson XML data format with a POJO model, aggregating first for batches; envelope assembly may need a generated or custom processor |
| Flat File Assembler | Candidate: Bindy with an annotated model, or a generated or custom serializer |
| JSON Encoder | Jackson JSON data format |
| MIME Encoder | MIME multipart data format (`camel-mail`) |
| S/MIME Encoder | Manual, catalog-verified crypto or mail implementation after certificate and keystore review |
| Custom components | `bean` or `process`, re-implemented in Groovy or Java |

## Maps and functoids

A map is first extracted as a complete semantic mapping, then DataMapper selects the engine from the mapping, not from the functoid names: inline Groovy when both schemas are absent or the mapping has fewer than 20 leaf fields, XSLT only with at least 20 leaf fields and at least one schema.

-   Direct links contribute a source-to-target field mapping.
    
-   String concatenation, upper and lower case, value mapping, mass copy, record count and nil value functoids are recorded as typed mappings and rendered by the selected engine (for example `concat()` in XSLT).
    
-   Logical functoids become conditional mappings; a route-level business decision stays a `choice` EIP.
    
-   Looping functoids become collection mappings, or the `split` EIP when they drive the route itself.
    
-   Database lookup functoids map to the `enrich` EIP with `sql`.
    
-   Scripting functoids (C#, VB.NET) are preserved with their input and output semantics and flagged for manual review; the design may suggest a compatible Groovy replacement, otherwise it records a custom-processor action, which requires Spring Boot or Quarkus.
    

## Example

The `OrderToInvoiceMap` in this orchestration has at least 20 leaf fields and a schema, so DataMapper selected XSLT.

BizTalk orchestration

```xml
<ServiceBody>
  <ReceiveShape Name="ReceiveOrder" PortName="OrderPort" Operation="SubmitOrder"/>
  <TransformShape Name="MapOrder" Map="OrderToInvoiceMap"/>
  <DecisionShape Name="CheckAmount">
    <Branch Expression="OrderAmount > 1000">
      <SendShape Name="SendHighValue" PortName="HighValuePort"/>
    </Branch>
    <DefaultBranch>
      <SendShape Name="SendStandard" PortName="StandardPort"/>
    </DefaultBranch>
  </DecisionShape>
</ServiceBody>
```

Camel YAML

```yaml
- route:
    id: process-order
    from:
      uri: "platform-http:/api/orders"
      parameters:
        httpMethodRestrict: POST
      steps:
        - step:
            id: kaoto-datamapper-a1b2c3d4
            steps:
              - to:
                  id: kaoto-datamapper-xslt-a1b2
                  uri: "xslt-saxon:kaoto-datamapper-a1b2c3d4.xsl"
        - choice:
            when:
              - xpath: "/Invoice/Amount > 1000"
                steps:
                  - to: "direct:high-value-processing"
            otherwise:
              steps:
                - to: "direct:standard-processing"
```

The `xslt-saxon` step returns the transformed document as a string, so the decision reads it with XPath; a bean-style Simple expression on the body would fail.

## Flagged for manual review

-   Scripting functoids with C# or VB.NET code.
    
-   Custom .NET pipeline components, which need a custom Camel processor.
    
-   The MSMQ adapter, which needs a replacement decision.
    
-   The Suspend shape, which needs a redesign.
    
-   EDI disassemblers and assemblers: no Camel 4 catalog component is assumed; verify the available EDI support in the catalog, otherwise use a third-party EDI library or a custom processor, then review the mapping.
    
-   External assembly calls in expressions, which need a Java or Groovy reimplementation.
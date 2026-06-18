# OCSF

**Since Camel 4.18**

The OCSF Data Format uses the [Jackson library](https://github.com/FasterXML/jackson) to marshal and unmarshal security events following the [Open Cybersecurity Schema Framework (OCSF)](https://schema.ocsf.io/) specification.

OCSF is an open-source standard for cybersecurity event logging and data normalization. It provides a vendor-neutral schema for security events, enabling interoperability between different security tools and platforms.

## Supported OCSF Event Classes

This data format includes POJOs for 34 OCSF event classes and 70 reusable object types (based on OCSF schema 1.8.0). Key event classes include:

**Findings (Category 2):**

-   `DetectionFinding` - Alerts from SIEM, EDR, XDR tools (class\_uid: 2004)
    
-   `SecurityFinding`, `VulnerabilityFinding`, `ComplianceFinding`, `IncidentFinding`
    

**System Activity (Category 1):**

-   `FileActivity`, `ProcessActivity`, `KernelActivity`, `MemoryActivity`, `ModuleActivity`, `ScheduledJobActivity`
    

**Network Activity (Category 4):**

-   `NetworkActivity`, `HttpActivity`, `DnsActivity`, `DhcpActivity`, `RdpActivity`, `SmbActivity`, `SshActivity`, `FtpActivity`, `EmailActivity`, `NtpActivity`
    

**IAM (Category 3):**

-   `Authentication`, `AuthorizeSession`, `AccountChange`, `GroupManagement`, `UserAccess`, `EntityManagement`
    

**Application Activity (Category 6):**

-   `ApiActivity`, `DatastoreActivity`, `WebResourcesActivity`, `ScanActivity`
    

**Remediation (Category 7):**

-   `RemediationActivity`
    

All event classes extend `OcsfEvent` which provides common attributes like `time`, `severity_id`, `class_uid`, and `metadata`.

## Usage

### Marshalling OCSF Events

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .marshal().ocsf()
    .to("kafka:security-events");
```

```xml
<route>
  <from uri="direct:start"/>
  <marshal>
    <ocsf/>
  </marshal>
  <to uri="kafka:security-events"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            ocsf: {}
        - to:
            uri: kafka:security-events
```

### Unmarshalling OCSF Events

-   Java
    
-   XML
    
-   YAML
    

```java
from("kafka:security-events")
    .unmarshal().ocsf()
    .to("direct:process");
```

```xml
<route>
  <from uri="kafka:security-events"/>
  <unmarshal>
    <ocsf/>
  </unmarshal>
  <to uri="direct:process"/>
</route>
```

```yaml
- route:
    from:
      uri: kafka:security-events
      steps:
        - unmarshal:
            ocsf: {}
        - to:
            uri: direct:process
```

### Unmarshalling to a Specific Event Class

-   Java
    
-   XML
    
-   YAML
    

```java
from("kafka:security-events")
    .unmarshal().ocsf(DetectionFinding.class)
    .to("direct:process");
```

```xml
<route>
  <from uri="kafka:security-events"/>
  <unmarshal>
    <ocsf unmarshalType="org.apache.camel.dataformat.ocsf.model.DetectionFinding"/>
  </unmarshal>
  <to uri="direct:process"/>
</route>
```

```yaml
- route:
    from:
      uri: kafka:security-events
      steps:
        - unmarshal:
            ocsf:
              unmarshalType: org.apache.camel.dataformat.ocsf.model.DetectionFinding
        - to:
            uri: direct:process
```

### Using with AWS Security Hub

AWS Security Hub now outputs findings in OCSF format. You can use this data format to process those findings:

-   Java
    
-   XML
    
-   YAML
    

```java
from("aws-securityhub:findings")
    .unmarshal().ocsf(DetectionFinding.class)
    .choice()
        .when(simple("${body.severityId} >= 4"))
            .to("direct:high-severity")
        .otherwise()
            .to("direct:normal-severity");
```

```xml
<route>
  <from uri="aws-securityhub:findings"/>
  <unmarshal>
    <ocsf unmarshalType="org.apache.camel.dataformat.ocsf.model.DetectionFinding"/>
  </unmarshal>
  <choice>
    <when>
      <simple>${body.severityId} >= 4</simple>
      <to uri="direct:high-severity"/>
    </when>
    <otherwise>
      <to uri="direct:normal-severity"/>
    </otherwise>
  </choice>
</route>
```

```yaml
- route:
    from:
      uri: aws-securityhub:findings
      steps:
        - unmarshal:
            ocsf:
              unmarshalType: org.apache.camel.dataformat.ocsf.model.DetectionFinding
        - choice:
            when:
              - simple: "${body.severityId} >= 4"
                steps:
                  - to:
                      uri: direct:high-severity
            otherwise:
              steps:
                - to:
                    uri: direct:normal-severity
```

## OCSF Options

The OCSF dataformat supports 7 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **objectMapper** (advanced) |  | `String` | Lookup and use the existing ObjectMapper with the given id when using Jackson. |
| **useDefaultObjectMapper** (common) | `true` | `Boolean` | Whether to lookup and use default Jackson ObjectMapper from the registry. |
| **unmarshalType** (common) |  | `String` | Class name of the OCSF event type to use when unmarshalling. Defaults to OcsfEvent. |
| **collectionType** (advanced) |  | `String` | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows to use different collection types than java.util.Collection based as default. |
| **useList** (common) | `false` | `Boolean` | To unmarshal to a List of OCSF events. |
| **allowUnmarshallType** (common) | `false` | `Boolean` | If enabled then the unmarshal type can be specified via the CamelOcsfUnmarshalType header. This should only be enabled when desired to be used. |
| **prettyPrint** (common) | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |

## OCSF Event Categories

OCSF defines the following event categories:

  
| Category ID | Name | Description |
| --- | --- | --- |
| 1 | System Activity | Process, file system, kernel events |
| 2 | Findings | Security findings, vulnerabilities, compliance |
| 3 | IAM | Authentication, authorization, account changes |
| 4 | Network Activity | HTTP, DNS, SSH, network traffic |
| 5 | Discovery | Device inventory, configuration state |
| 6 | Application Activity | API activity, web resources, scans |
| 7 | Remediation | Remediation activities |

## Example: Creating a Detection Finding

_Java-only: creating and marshalling a DetectionFinding POJO_

```java
DetectionFinding finding = new DetectionFinding();
finding.setActivityId(1); // Create
finding.setSeverityId(4); // High
finding.setTime(System.currentTimeMillis());
finding.setMessage("Suspicious activity detected");

FindingInfo info = new FindingInfo();
info.setTitle("Malware Detection");
info.setDesc("Potential malware detected on endpoint");
finding.setFindingInfo(info);

from("direct:start")
    .setBody(constant(finding))
    .marshal().ocsf()
    .to("splunk-hec:...");
```

## Example: AI-Powered Security Finding Summarization

You can combine the OCSF DataFormat with the LangChain4j Chat component to use an AI agent that analyzes and summarizes security findings. This is useful for:

-   Generating human-readable summaries for security analysts
    
-   Prioritizing alerts based on AI assessment
    
-   Enriching findings with additional context and recommendations
    

### Java DSL Example

_Java-only: AI-powered security finding summarization with process and langchain4j_

```java
from("kafka:security-events")
    .unmarshal().ocsf(DetectionFinding.class)
    .process(exchange -> {
        DetectionFinding finding = exchange.getIn().getBody(DetectionFinding.class);

        // Build a prompt with the finding details
        String prompt = String.format("""
            Analyze this security detection finding and provide a brief summary:

            Title: %s
            Severity: %s
            Message: %s
            Description: %s

            Provide:
            1. A one-sentence summary of the threat
            2. Recommended immediate actions
            3. Risk assessment (Critical/High/Medium/Low)
            """,
            finding.getFindingInfo() != null ? finding.getFindingInfo().getTitle() : "Unknown",
            finding.getSeverityId(),
            finding.getMessage(),
            finding.getFindingInfo() != null ? finding.getFindingInfo().getDesc() : "No description"
        );
        exchange.getIn().setBody(prompt);
    })
    .to("langchain4j-chat:security-analyst?chatModel=#chatLanguageModel")
    .to("direct:ai-summary");
```

### YAML DSL Example

```yaml
- route:
    from:
      uri: kafka:security-events
    steps:
      - unmarshal:
          ocsf:
            unmarshalType: "org.apache.camel.dataformat.ocsf.model.DetectionFinding"
      - setHeader:
          name: "findingTitle"
          expression:
            simple:
              expression: "${body.findingInfo?.title}"
      - setHeader:
          name: "findingSeverity"
          expression:
            simple:
              expression: "${body.severityId}"
      - setHeader:
          name: "findingMessage"
          expression:
            simple:
              expression: "${body.message}"
      - setBody:
          expression:
            simple:
              expression: |
            Analyze this security detection finding and provide a brief summary:

            Title: ${header.findingTitle}
            Severity: ${header.findingSeverity}
            Message: ${header.findingMessage}

            Provide:
            1. A one-sentence summary of the threat
            2. Recommended immediate actions
            3. Risk assessment (Critical/High/Medium/Low)
      - to:
          uri: langchain4j-chat:security-analyst
          parameters:
            chatModel: "#chatLanguageModel"
      - to:
          uri: direct:ai-summary
```

## Dependencies

```xml
<dependency>
   <groupId>org.apache.camel</groupId>
   <artifactId>camel-ocsf</artifactId>
   <version>x.x.x</version>
</dependency>
```

## Generated Model Classes

The component includes generated Java POJOs for OCSF events and objects in the package `org.apache.camel.dataformat.ocsf.model`.

### Event Classes

  
| Class | Category | Description |
| --- | --- | --- |
| `OcsfEvent` | Base | Base class with common attributes (time, severity\_id, class\_uid, metadata) |
| `DetectionFinding` | Findings | Alerts from SIEM, EDR, XDR, threat detection tools |
| `SecurityFinding` | Findings | General security findings |
| `VulnerabilityFinding` | Findings | Vulnerability scan results |
| `ComplianceFinding` | Findings | Compliance check results |
| `IncidentFinding` | Findings | Security incidents |
| `FileActivity` | System | File system operations |
| `ProcessActivity` | System | Process creation, termination, injection |
| `KernelActivity` | System | Kernel-level events |
| `MemoryActivity` | System | Memory operations |
| `ModuleActivity` | System | Module/library loading |
| `ScheduledJobActivity` | System | Scheduled task events |
| `KernelExtensionActivity` | System | Kernel extension events |
| `NetworkActivity` | Network | Network connections and traffic |
| `HttpActivity` | Network | HTTP request/response events |
| `DnsActivity` | Network | DNS queries and responses |
| `DhcpActivity` | Network | DHCP events |
| `RdpActivity` | Network | Remote Desktop Protocol events |
| `SmbActivity` | Network | SMB/CIFS file sharing events |
| `SshActivity` | Network | SSH session events |
| `FtpActivity` | Network | FTP transfer events |
| `EmailActivity` | Network | Email events |
| `NtpActivity` | Network | NTP synchronization events |
| `NetworkFileActivity` | Network | Network file operations |
| `Authentication` | IAM | Login/logout events |
| `AuthorizeSession` | IAM | Session authorization |
| `AccountChange` | IAM | Account modifications |
| `GroupManagement` | IAM | Group membership changes |
| `UserAccess` | IAM | User access events |
| `EntityManagement` | IAM | Entity lifecycle events |
| `ApiActivity` | Application | API calls |
| `DatastoreActivity` | Application | Database operations |
| `WebResourcesActivity` | Application | Web resource access |
| `ScanActivity` | Application | Security scans |
| `RemediationActivity` | Remediation | Remediation actions |

### Object Classes

Reusable objects used within event classes:

-   `Actor`, `User`, `Group`, `Account` - Identity objects
    
-   `Device`, `Endpoint`, `NetworkEndpoint` - Device and endpoint objects
    
-   `Process`, `File`, `Module`, `Kernel` - System objects
    
-   `Attack`, `Tactic`, `Technique`, `SubTechnique` - MITRE ATT&CK objects
    
-   `FindingInfo`, `Remediation`, `Vulnerability`, `Malware` - Security finding objects
    
-   `Cloud`, `Container`, `Image` - Cloud and container objects
    
-   `Metadata`, `Product`, `Observable`, `Enrichment` - Metadata objects
    
-   `Certificate`, `Tls`, `Fingerprint` - Cryptographic objects
    
-   `HttpRequest`, `HttpResponse`, `DnsQuery`, `Url`, `Packet` - Network protocol objects
    
-   `Location`, `Organization`, `Service`, `Token` - Context objects
    
-   `Cve`, `Cvss`, `Cwe`, `Epss` - Vulnerability reference objects
    

## Updating OCSF Schema Version

The Java POJOs in this component are generated from JSON Schema files using the jsonschema2pojo Maven plugin. The classes are generated at build time to `target/generated-sources/jsonschema2pojo` and included in the released JAR. A Python script is provided to regenerate the JSON schemas from the official OCSF specification when a new version is released.

### Prerequisites

Install the `ocsf-json-schema` Python package:

```bash
pip install ocsf-json-schema
```

### Generating Schemas and Java Classes

To update the OCSF model classes to a new version:

1.  Run the schema generation script from the `src/main/script` directory:
    
    ```bash
    cd src/main/script
    python3 generate-ocsf-schemas.py --version 1.8.0 --output ../resources/schema --clean
    ```
    
2.  Build and test to verify the changes (Java classes are generated automatically during build):
    
    ```bash
    mvn clean test
    ```
    
3.  Commit the updated JSON schema files.
    

> **Note**
> The script first tries to load the requested OCSF version from the bundled `ocsf-json-schema` Python package. If the version is not bundled yet (typical for the most recent OCSF release), the script automatically downloads the schema from `[https://schema.ocsf.io/{version}/export/schema](https://schema.ocsf.io/{version}/export/schema)`.

### Script Options

The script supports the following options:

  
| Option | Default | Description |
| --- | --- | --- |
| `--version`, `-v` | 1.8.0 | OCSF schema version to generate |
| `--output`, `-o` | ../resources/schema | Output directory for schema files |
| `--clean` | false | Remove existing schema files before generating |
| `--all-classes` | false | Generate all available event classes (not just the default list) |
| `--all-objects` | false | Generate all available objects (not just the default list) |

### Schema Generation Details

The script generates:

-   **OcsfEvent.json** - Base event class with common attributes (time, severity, class\_uid, etc.)
    
-   **Object schemas** - Reusable OCSF objects (Attack, FindingInfo, Device, User, etc.)
    
-   **Event class schemas** - Event classes that extend OcsfEvent (DetectionFinding, Authentication, etc.)
    

The generated schemas use:

-   JSON Schema Draft-07 format
    
-   File-based `$ref` references (e.g., `"$ref": "Attack.json"`)
    
-   `javaType` annotations for explicit Java class naming
    
-   `allOf` pattern for event class inheritance from OcsfEvent
    
-   `additionalProperties: true` for forward compatibility
    

## See Also

-   [OCSF Schema Browser](https://schema.ocsf.io/)
    
-   [OCSF Schema GitHub](https://github.com/ocsf/ocsf-schema)
    
-   [AWS Security Hub OCSF Documentation](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-ocsf.md)
    

## Spring Boot Auto-Configuration

When using ocsf with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-ocsf-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.ocsf.allow-unmarshall-type** | If enabled then the unmarshal type can be specified via the CamelOcsfUnmarshalType header. This should only be enabled when desired to be used. | false | Boolean |
| **camel.dataformat.ocsf.collection-type** | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows to use different collection types than java.util.Collection based as default. |  | String |
| **camel.dataformat.ocsf.enabled** | Whether to enable auto configuration of the ocsf data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.ocsf.object-mapper** | Lookup and use the existing ObjectMapper with the given id when using Jackson. |  | String |
| **camel.dataformat.ocsf.pretty-print** | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| **camel.dataformat.ocsf.unmarshal-type** | Class name of the OCSF event type to use when unmarshalling. Defaults to OcsfEvent. |  | String |
| **camel.dataformat.ocsf.use-default-object-mapper** | Whether to lookup and use default Jackson ObjectMapper from the registry. | true | Boolean |
| **camel.dataformat.ocsf.use-list** | To unmarshal to a List of OCSF events. | false | Boolean |
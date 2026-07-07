# OCSF

JVM since3.38.0 Native since3.38.0

Marshal and unmarshal OCSF (Open Cybersecurity Schema Framework) security events to/from JSON.

## What’s inside

-   [OCSF data format](../../../../components/next/dataformats/ocsf-dataformat.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-ocsf)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-ocsf</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

The OCSF (Open Cybersecurity Schema Framework) extension provides support for marshalling and unmarshalling security events following the OCSF specification.

## Basic Usage

### Marshalling OCSF Events

```java
from("direct:start")
    .marshal().ocsf()
    .to("kafka:security-events");
```

### Unmarshalling OCSF Events

```java
from("kafka:security-events")
    .unmarshal().ocsf()
    .to("direct:process");
```

### Unmarshalling to a Specific Event Class

```java
from("kafka:security-events")
    .unmarshal().ocsf(DetectionFinding.class)
    .to("direct:process");
```

## Supported OCSF Event Classes

This extension includes support for 34 OCSF event classes including:

-   **Findings**: `DetectionFinding`, `SecurityFinding`, `VulnerabilityFinding`, `ComplianceFinding`
    
-   **System Activity**: `FileActivity`, `ProcessActivity`, `KernelActivity`, `MemoryActivity`
    
-   **Network Activity**: `NetworkActivity`, `HttpActivity`, `DnsActivity`, `SshActivity`
    
-   **IAM**: `Authentication`, `AuthorizeSession`, `AccountChange`, `GroupManagement`
    
-   **Application Activity**: `ApiActivity`, `DatastoreActivity`, `WebResourcesActivity`
    

All event classes extend `OcsfEvent` which provides common attributes like `time`, `severity_id`, `class_uid`, and `metadata`.

## Example: Creating a Detection Finding

```java
import org.apache.camel.dataformat.ocsf.model.DetectionFinding;
import org.apache.camel.dataformat.ocsf.model.FindingInfo;
import org.apache.camel.dataformat.ocsf.OcsfConstants;

DetectionFinding finding = new DetectionFinding();
finding.setActivityId(OcsfConstants.ACTIVITY_CREATE);
finding.setSeverityId(OcsfConstants.SEVERITY_HIGH);
finding.setTime(System.currentTimeMillis());
finding.setIsAlert(true);

FindingInfo info = new FindingInfo();
info.setTitle("Malware Detection");
info.setDesc("Potential malware detected on endpoint");
finding.setFindingInfo(info);

from("direct:start")
    .setBody(constant(finding))
    .marshal().ocsf()
    .to("splunk-hec:...");
```

## Native Mode Support

The OCSF extension fully supports native mode compilation. All OCSF model classes are automatically registered for reflection during the build process.
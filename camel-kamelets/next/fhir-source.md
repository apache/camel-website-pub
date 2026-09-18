# ![fhir source](_images/kamelets/fhir-source.svg) FHIR Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from FHIR server.

## Configuration Options

The following table summarizes the configuration options available for the `fhir-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **password** | Password | **Required** The password to access the FHIR server. | string |  |  |
| **serverUrl** | Server URL | **Required** The FHIR server url. | string |  |  |
| **username** | Username | **Required** The username to access the FHIR server. | string |  |  |
| **encoding** | Encoding | Encoding to use for all request. Enum values: \* JSON \* XML | string | JSON |  |
| **fhirVersion** | FHIR Version | The FHIR Version to use. Enum values: \* DSTU2 \* DSTU2\_HL7ORG \* DSTU2\_1 \* DSTU3 \* R4 \* R5 | string | R4 |  |
| **prettyPrint** | Json Pretty Print | Define if the Json must be pretty print or not. | boolean | true |  |
| **url** | URL | The FHIR resource type url. | string | /Patient |  |

## Dependencies

At runtime, the `fhir-source` Kamelet relies upon the presence of the following dependencies:

-   camel:fhir
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:fhir-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## FHIR Source Kamelet Description

### Authentication

This Kamelet requires username and password authentication to access the FHIR server. The credentials are configured through the `username` and `password` properties.

### Configuration

The FHIR Source Kamelet supports the following configurations:

-   **Server URL**: The FHIR server URL endpoint (required)
    
-   **Resource URL**: The FHIR resource type URL (default: "/Patient")
    
-   **Encoding**: Response encoding format - JSON or XML (default: "JSON")
    
-   **FHIR Version**: The FHIR specification version to use (default: "R4")
    
-   **Pretty Print**: Whether to format JSON responses for readability (default: true)
    

### Output Format

The Kamelet outputs data in JSON format, marshalling FHIR resources according to the specified FHIR version and pretty print settings.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:fhir-source"
      parameters:
        serverUrl: "https://hapi.fhir.org/baseR4"
        username: "your-username"
        password: "your-password"
        url: "/Patient"
        fhirVersion: "R4"
        encoding: "JSON"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Different Resource Type

```yaml
- route:
    from:
      uri: "kamelet:fhir-source"
      parameters:
        serverUrl: "https://hapi.fhir.org/baseR4"
        username: "your-username"
        password: "your-password"
        url: "/Observation"
        fhirVersion: "R4"
        encoding: "JSON"
        prettyPrint: false
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This example searches for Observation resources from the FHIR server with compact JSON output.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/fhir-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/fhir-source.kamelet.yaml)
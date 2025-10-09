# ![fhir sink](_images/kamelets/fhir-sink.svg) FHIR Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Forward data to a FHIR endpoint.

## Configuration Options

The following table summarizes the configuration options available for the `fhir-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **methodName** | Method Name | **Required** What sub operation to use for the selected operation. | string |  |  |
| **serverUrl** | Server URL | **Required** The FHIR server base URL. | string |  |  |
| **accessToken** | Access Token | OAuth access token. | string |  |  |
| **apiName** | API Name | What kind of operation to perform. Enum values: \* CAPABILITIES \* CREATE \* DELETE \* HISTORY \* LOAD\_PAGE \* META \* OPERATION \* PATCH \* READ \* SEARCH \* TRANSACTION \* UPDATE \* VALIDATE | string |  |  |
| **encoding** | Encoding | Encoding to use for all request. One of: \[JSON\] \[XML\]. | string | JSON |  |
| **fhirVersion** | FHIR Version | The FHIR Version to use. Enum values: \* DSTU2 \* DSTU2\_HL7ORG \* DSTU2\_1 \* DSTU3 \* R4 \* R5 | string | R4 |  |
| **lazyStartProducer** | Lazy Start Producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | boolean | false |  |
| **log** | Log | Will log every requests and responses. | boolean | false |  |
| **password** | Password | Password to use for basic authentication. | string |  |  |
| **prettyPrint** | Pretty Print | Pretty print all request. | boolean | false |  |
| **proxyHost** | Proxy Host | The proxy host. | string |  |  |
| **proxyPassword** | Proxy Password | The proxy password. | string |  |  |
| **proxyPort** | Proxy Port | The proxy port. | integer |  |  |
| **proxyUser** | Proxy User | The proxy username. | string |  |  |
| **username** | Username | Username to use for basic authentication. | string |  |  |

## Dependencies

At runtime, the `fhir-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:fhir
    
-   camel:core
    
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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:fhir-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## FHIR Sink Kamelet Description

### FHIR Operations

This Kamelet supports various FHIR operations including CREATE, READ, UPDATE, DELETE, SEARCH, and others. You must specify both the API name and method name for the operation.

### FHIR Versions

Supports multiple FHIR versions: - DSTU2, DSTU2\_HL7ORG, DSTU2\_1 - DSTU3 - R4 (default) - R5

### Data Encoding

Supports both JSON (default) and XML encoding for FHIR resources. The Kamelet automatically handles marshalling and unmarshalling based on the configured encoding.

### Authentication

Supports multiple authentication methods: - OAuth 2.0 access tokens - Basic authentication with username and password

### Proxy Support

The Kamelet can be configured to work through HTTP proxies with optional authentication.

### Configuration Options

Additional configuration includes: - Pretty printing for requests - Request/response logging - Lazy producer startup

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/fhir-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/fhir-sink.kamelet.yaml)
# ![fhir sink](_images/kamelets/fhir-sink.svg) FHIR Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message, a FHIR resource such as a Patient or an Observation, to a FHIR server of healthcare data, to create, update, delete or validate it there.

Use it to write healthcare records into a FHIR server, for example to create a Patient for each new admission, or to update an Observation that a device measured. To read resources from a FHIR server, use `fhir-source`.

Input: the body is the FHIR resource, as JSON text, or as XML text with `encoding` set to `XML`, such as `{"resourceType": "Patient", "name": [{"family": "Doe"}]}`. It is sent with the operation set by `apiName` and `methodName`, which must be one that takes a resource: `CREATE` with `resource`, `UPDATE` with `resource`, `DELETE` with `resource`, or `VALIDATE` with `resource`.

Output: when it is used inside a route, the body afterwards is the outcome of the operation, as a Java object of the HAPI FHIR library, with the id of the resource; it is not JSON.

Good to know: a body that is not a valid FHIR resource of the chosen `fhirVersion` fails the message. Operations that do not take a resource, such as `READ` or `SEARCH`, fail.

## Configuration Options

The following table summarizes the configuration options available for the `fhir-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apiName** | API Name | **Required** The kind of operation, such as `CREATE` to add a new resource or `UPDATE` to change an existing one. Use one that takes a resource as input: `CREATE`, `UPDATE`, `DELETE` or `VALIDATE`. Enum values: \* CAPABILITIES \* CREATE \* DELETE \* HISTORY \* LOAD\_PAGE \* META \* OPERATION \* PATCH \* READ \* SEARCH \* TRANSACTION \* UPDATE \* VALIDATE | string |  |  |
| **methodName** | Method Name | **Required** The variant of the operation in `apiName`. Use `resource`, which takes the resource in the body. | string |  | resource |
| **serverUrl** | Server URL | **Required** The base address of the FHIR API of the server, the part before the resource type, starting with `http://` or `https://`. | string |  | https://fhir.example.com/fhir |
| **accessToken** | Access Token | An OAuth access token, sent as a Bearer token, for a server that uses OAuth, such as SMART on FHIR. Use it instead of `username` and `password`. | string |  |  |
| **encoding** | Encoding | How the resources are written: `JSON` or `XML`. The body must be in this format. | string | JSON | XML |
| **fhirVersion** | FHIR Version | The version of the FHIR standard that the server and the resources use. Most servers today use `R4`. Enum values: \* DSTU2 \* DSTU2\_HL7ORG \* DSTU2\_1 \* DSTU3 \* R4 \* R5 | string | R4 |  |
| **lazyStartProducer** | Lazy Start Producer | If true, the connection to the server is set up at the first message instead of when the integration starts, so that the integration can start while the server is not reachable. The first message then takes a little longer. | boolean | false |  |
| **log** | Log | If true, every request to the server and every response is written to the log, for troubleshooting. | boolean | false |  |
| **password** | Password | The password of `username`, for Basic authentication. | string |  |  |
| **prettyPrint** | Pretty Print | If true, the resources sent to the server are indented, which is easier to read in logs. | boolean | false |  |
| **proxyHost** | Proxy Host | The host name of an HTTP proxy to reach the server through. Use it with `proxyPort`. | string |  | proxy.example.com |
| **proxyPassword** | Proxy Password | The password of `proxyUser` for the HTTP proxy. | string |  |  |
| **proxyPort** | Proxy Port | The port of the HTTP proxy in `proxyHost`. | integer |  | 3128 |
| **proxyUser** | Proxy User | The user to log in to the HTTP proxy as, when the proxy needs a login. | string |  |  |
| **username** | Username | The user to log in to the server as, with Basic authentication. Leave it out for a server without login. | string |  |  |

## Dependencies

At runtime, the `fhir-sink` Kamelet relies upon the presence of the following dependencies:

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

This Kamelet sends the FHIR resource in the message body to the server. You must specify both the API name and the method name of the operation, and the operation must take the resource as input: `CREATE`, `UPDATE`, `DELETE` or `VALIDATE`, each with the method name `resource`. Operations that do not take a resource, such as READ or SEARCH, fail.

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
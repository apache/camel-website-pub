# ![soap source](_images/kamelets/soap-source.svg) SOAP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Serves a SOAP web service described by a WSDL file, and answers each call with the reply of the route.

Use it to keep existing SOAP clients working while the systems behind the service are replaced: the route gets each call and can call REST services or other systems to answer it. No Java code is generated from the WSDL. To call a SOAP service, use `soap-action`.

Output: the body is the content of the SOAP Body of the request as XML text: the request element of the operation, such as `<getOrder xmlns="http://example.com/orders"><orderId>7</orderId></getOrder>`. The header `CamelCxfOperationName` is the name of the operation, such as `getOrder`, and `CamelCxfOperationNamespace` its namespace. The HTTP headers of the request, such as `User-Agent`, are headers too.

The reply of the route, as XML text, is the content of the SOAP Body of the response: the response element of the operation, such as `<getOrderResponse xmlns="http://example.com/orders">…​</getOrderResponse>`. To answer with a SOAP fault, the route sets the header `SoapFault` to the text of the fault, and `SoapFaultCode` to `Client` when the request was wrong (`Sender` with SOAP 1.2; otherwise the code is `Server`, or `Receiver`); the body, if any, is the content of the detail of the fault as XML text, such as the fault element the WSDL declares. This is what `soap-action` gives with `faultAsBody`, so a fault of a called service can be passed on. The route can also reply with the SOAP fault itself, as XML text, such as `<soap:Fault xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"><faultcode>soap:Client</faultcode><faultstring>No such order</faultstring></soap:Fault>`, or a `Fault` of SOAP 1.2: the client gets it as a SOAP fault, with its code, text and detail. When the route fails, the client gets a SOAP fault with the text `Exchange processing failed`, which does not say why. The headers of the reply are not sent back to the client.

Good to know: the service is served at `address`, its WSDL at `address` followed by `?wsdl`, with SOAP 1.1 or 1.2 as the WSDL says. A request or a reply that does not match the XML schema of the WSDL is refused with a SOAP fault, unless `schemaValidation` is false, and so is a request for an operation the WSDL does not have, and a request with a DOCTYPE. There is no login unless `wsSecurityUsername` and `wsSecurityPassword` are set, which require a WS-Security UsernameToken in each request: the integration then needs the jar `org.apache.cxf:cxf-rt-ws-security` of the CXF version that Camel uses, such as `camel run --dep=mvn:org.apache.cxf:cxf-rt-ws-security:4.2.4` with Camel 4.24, or it fails to start with a message that says so. Protect the address with your network too. To work with JSON, turn the body into JSON with `xj-identity-action`, and build the reply as XML.

## Configuration Options

The following table summarizes the configuration options available for the `soap-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **address** | Address | **Required** The URL to serve the SOAP service at. Use `0.0.0.0` as the host to accept calls on every network interface of the machine. | string |  | http://0.0.0.0:8080/orders |
| **wsdlURL** | WSDL Location | **Required** Where to read the WSDL file from, which describes the operations and their XML schema. `file:` followed by a path, `classpath:` followed by a resource in the application, or an `https://` URL (an `http://` URL works too, but the WSDL decides what is called, so it should not travel unprotected). | string |  | classpath:orders.wsdl |
| **loggingEnabled** | Log Messages | Whether to write each SOAP request and response to the log. Do not turn it on when the messages hold personal data or secrets. | boolean | false |  |
| **portName** | Port Name | The port of the service to serve, as `\{namespace}name`. Only needed when the service has more than one port; otherwise the first one is used. | string |  | {http://example.com/orders}OrderPort |
| **publishedEndpointUrl** | Published URL | The URL that the WSDL served at `?wsdl` gives to the clients as the address of the service, such as the public URL of a load balancer. When it is not set, the WSDL gives the host that the client used in its request. | string |  | https://orders.example.com/orders |
| **schemaValidation** | Schema Validation | Whether to refuse a request, and a reply of the route, that does not match the XML schema of the WSDL. | boolean | true |  |
| **serviceName** | Service Name | The service of the WSDL to serve, as `\{namespace}name`. Only needed when the WSDL has more than one service; otherwise the first one is used. | string |  | {http://example.com/orders}OrderService |
| **wsSecurityPassword** | WS-Security Password | The password of `wsSecurityUsername`. | string |  |  |
| **wsSecurityPasswordType** | WS-Security Password Type | How the UsernameToken must carry the password. `Text` as it is, so only use it over HTTPS, or `Digest` as a SHA-1 digest of it, which is no replacement for HTTPS. A UsernameToken with the other type is refused. When the WSDL has a WS-SecurityPolicy, the policy decides instead. When it is not set, `Text`. Enum values: \* Text \* Digest | string |  | Digest |
| **wsSecurityUsername** | WS-Security Username | The user that may call the service. When it is set, each request must carry a WS-Security UsernameToken of this user and `wsSecurityPassword` in its SOAP header, or it is refused with a SOAP fault before the route sees it. | string |  |  |

## Dependencies

At runtime, the `soap-source` Kamelet relies upon the presence of the following dependencies:

-   camel:cxf-soap
    
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
      uri: "kamelet:soap-source"
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/soap-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/soap-source.kamelet.yaml)
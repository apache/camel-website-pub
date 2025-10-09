# CXF

JVM since2.12.0 Native since2.12.0

Expose SOAP WebServices using Apache CXF or connect to external WebServices using CXF WS client.

## What’s inside

-   [CXF component](../../../../components/4.14.x/cxf-component.md), URI syntax: `cxf:beanId:address`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-cxf-soap)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-cxf-soap</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### General

`camel-quarkus-cxf-soap` uses extensions from the [CXF Extensions for Quarkus](https://quarkiverse.github.io/quarkiverse-docs/quarkus-cxf/dev) project - `quarkus-cxf`. This means the set of supported use cases and WS specifications is largely given by `quarkus-cxf`.

> **Important**
> To learn about supported use cases and WS specifications, see the Quarkus CXF [Reference](https://quarkiverse.github.io/quarkiverse-docs/quarkus-cxf/dev/reference/index.md).

### Dependency management

The CXF and `quarkus-cxf` versions are [managed](../../user-guide/dependency-management.md) by Camel Quarkus. You do not need to select compatible versions for those projects.

### Client

With `camel-quarkus-cxf-soap` (no additional dependencies required), you can use CXF clients as producers in Camel routes:

```java
import org.apache.camel.builder.RouteBuilder;
import jakarta.enterprise.context.ApplicationScoped;
import jakarta.enterprise.inject.Produces;
import jakarta.inject.Named;

@ApplicationScoped
public class CxfSoapClientRoutes extends RouteBuilder {

    @Override
    public void configure() {

        /* You can either configure the client inline */
        from("direct:cxfUriParamsClient")
                .to("cxf://http://localhost:8082/calculator-ws?wsdlURL=wsdl/CalculatorService.wsdl&dataFormat=POJO&serviceClass=org.foo.CalculatorService");

        /* Or you can use a named bean produced below by beanClient() method */
        from("direct:cxfBeanClient")
                .to("cxf:bean:beanClient?dataFormat=POJO");

    }

    @Produces
    @ApplicationScoped
    @Named
    CxfEndpoint beanClient() {
        final CxfEndpoint result = new CxfEndpoint();
        result.setServiceClass(CalculatorService.class);
        result.setAddress("http://localhost:8082/calculator-ws");
        result.setWsdlURL("wsdl/CalculatorService.wsdl"); // a resource in the class path
        return result;
    }
}
```

The `CalculatorService` may look like the following:

```java
import jakarta.jws.WebMethod;
import jakarta.jws.WebService;

@WebService(targetNamespace = CalculatorService.TARGET_NS) (1)
public interface CalculatorService {

    public static final String TARGET_NS = "http://acme.org/wscalculator/Calculator";

    @WebMethod (1)
    public int add(int intA, int intB);

    @WebMethod (1)
    public int subtract(int intA, int intB);

    @WebMethod (1)
    public int divide(int intA, int intB);

    @WebMethod (1)
    public int multiply(int intA, int intB);
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>NOTE: JAX-WS annotations are required. The Simple CXF Frontend is not supported. Complex parameter types require JAXB annotations to work in properly in native mode.</td></tr></tbody></table>

> **Tip**
> You can test this client application against the [quay.io/l2x6/calculator-ws:1.2](https://quay.io/repository/l2x6/calculator-ws) container that implements this service endpoint interface:
>
> ```shell
> docker run -p 8082:8080 quay.io/l2x6/calculator-ws:1.2
> ```

> **Note**
> `quarkus-cxf` supports [injecting SOAP clients](https://quarkiverse.github.io/quarkiverse-docs/quarkus-cxf/dev/user-guide/first-soap-client.md) using `@io.quarkiverse.cxf.annotation.CXFClient` annotation. Refer to the [SOAP Clients](https://quarkiverse.github.io/quarkiverse-docs/quarkus-cxf/dev/user-guide/first-soap-client.md) chapter of `quarkus-cxf` user guide for more details.

### Server

With `camel-quarkus-cxf-soap`, you can expose SOAP endpoints as consumers in Camel routes. No additional dependencies are required for this use case.

```java
import org.apache.camel.builder.RouteBuilder;
import jakarta.enterprise.context.ApplicationScoped;
import jakarta.enterprise.inject.Produces;
import jakarta.inject.Named;

@ApplicationScoped
public class CxfSoapRoutes extends RouteBuilder {

    @Override
    public void configure() {
        /* A CXF Service configured through a CDI bean */
        from("cxf:bean:helloBeanEndpoint")
                .setBody().simple("Hello ${body} from CXF service");

        /* A CXF Service configured through Camel URI parameters */
        from("cxf:///hello-inline?wsdlURL=wsdl/HelloService.wsdl&serviceClass=org.foo.HelloService")
                        .setBody().simple("Hello ${body} from CXF service");
    }

    @Produces
    @ApplicationScoped
    @Named
    CxfEndpoint helloBeanEndpoint() {
        final CxfEndpoint result = new CxfEndpoint();
        result.setServiceClass(HelloService.class);
        result.setAddress("/hello-bean");
        result.setWsdlURL("wsdl/HelloService.wsdl");
        return result;
    }
}
```

The path under which these two services will be served depends on the value of `quarkus.cxf.path` [configuration property](https://quarkiverse.github.io/quarkiverse-docs/quarkus-cxf/dev/reference/extensions/quarkus-cxf.html#quarkus-cxf_quarkus.cxf.path) which can for example be set in `application.properties`:

application.properties

```properties
quarkus.cxf.path = /soap-services
```

With this configuration in place, our two services can be reached under `[http://localhost:8080/soap-services/hello-bean](http://localhost:8080/soap-services/hello-bean)` and `[http://localhost:8080/soap-services/hello-inline](http://localhost:8080/soap-services/hello-inline)` respectively.

The WSDL can be accessed by adding `?wsdl` to the above URLs.

> **Important**
> Do not use `quarkus.cxf.path = /` in your application unless you are 100% sure that no other extension will want to expose HTTP endpoints.
>
> Before `quarkus-cxf` 2.0.0 (i.e. before Camel Quarkus 3.0.0), the default value of `quarkus.cxf.path` was `/`. The default was changed because it prevented other Quarkus extensions from exposing any further HTTP endpoints. Among others, RESTEasy, Vert.x, SmallRye Health (no health endpoints exposed!) were impacted by this.

> **Note**
> `quarkus-cxf` supports alternative ways of exposing SOAP endpoints. Refer to the [SOAP Services](https://quarkiverse.github.io/quarkiverse-docs/quarkus-cxf/dev/user-guide/first-soap-web-service.md) chapter of `quarkus-cxf` user guide for more details.

### Logging of requests and responses

You can enable verbose logging of SOAP messages for both clients and servers with `org.apache.cxf.ext.logging.LoggingFeature`:

```java
import org.apache.camel.builder.RouteBuilder;
import org.apache.cxf.ext.logging.LoggingFeature;
import jakarta.enterprise.context.ApplicationScoped;
import jakarta.enterprise.inject.Produces;
import jakarta.inject.Named;

@ApplicationScoped
public class MyBeans {

    @Produces
    @ApplicationScoped
    @Named("prettyLoggingFeature")
    public LoggingFeature prettyLoggingFeature() {
        final LoggingFeature result = new LoggingFeature();
        result.setPrettyLogging(true);
        return result;
    }

    @Inject
    @Named("prettyLoggingFeature")
    LoggingFeature prettyLoggingFeature;

    @Produces
    @ApplicationScoped
    @Named
    CxfEndpoint cxfBeanClient() {
        final CxfEndpoint result = new CxfEndpoint();
        result.setServiceClass(CalculatorService.class);
        result.setAddress("https://acme.org/calculator");
        result.setWsdlURL("wsdl/CalculatorService.wsdl");
        result.getFeatures().add(prettyLoggingFeature);
        return result;
    }

    @Produces
    @ApplicationScoped
    @Named
    CxfEndpoint helloBeanEndpoint() {
        final CxfEndpoint result = new CxfEndpoint();
        result.setServiceClass(HelloService.class);
        result.setAddress("/hello-bean");
        result.setWsdlURL("wsdl/HelloService.wsdl");
        result.getFeatures().add(prettyLoggingFeature);
        return result;
    }
}
```

> **Note**
> The support for `org.apache.cxf.ext.logging.LoggingFeature` is provided by `io.quarkiverse.cxf:quarkus-cxf-rt-features-logging` as a `camel-quarkus-cxf-soap` dependency. You do not need to add it explicitly to your application.

### WS Specifications

The extent of supported WS specifications is given by the Quarkus CXF project.

`camel-quarkus-cxf-soap` covers only the following specifications via the `[io.quarkiverse.cxf:quarkus-cxf](https://quarkiverse.github.io/quarkiverse-docs/quarkus-cxf/dev/reference/extensions/quarkus-cxf.md)` extension:

-   JAX-WS
    
-   JAXB
    
-   WS-Addressing
    
-   WS-Policy
    
-   MTOM
    

If your application requires some other WS specification, such as WS-Security or WS-Trust, you must add an additional Quarkus CXF dependency covering it. Refer to Quarkus CXF [Reference](https://quarkiverse.github.io/quarkiverse-docs/quarkus-cxf/dev/reference/index.md) page to see which WS specifications are covered by which Quarkus CXF extensions.

> **Tip**
> Both Camel Quarkus and Quarkus CXF contain a number of [integration](https://github.com/apache/camel-quarkus/tree/main/integration-test-groups/cxf-soap) [tests](https://github.com/quarkiverse/quarkus-cxf/tree/main/integration-tests) which can serve as executable examples of applications that implement various WS specifications.

### Tooling

`quarkus-cxf` wraps the following two CXF tools:

-   `wsdl2Java` - for [generating service classes from WSDL](https://quarkiverse.github.io/quarkiverse-docs/quarkus-cxf/dev/user-guide/first-soap-client.html#wsdl2java)
    
-   `java2ws` - for [generating WSDL from Java classes](https://quarkiverse.github.io/quarkiverse-docs/quarkus-cxf/dev/user-guide/generate-wsdl-from-java.md)
    

> **Important**
> For `wsdl2Java` to work properly, your application will have to directly depend on `io.quarkiverse.cxf:quarkus-cxf`.

> **Tip**
> While `wsdlvalidator` is not supported, you can use `wsdl2Java` with the following configuration in `application.properties` to validate your WSDLs:
>
> application.properties
>
> ```properties
> quarkus.cxf.codegen.wsdl2java.additional-params = -validate
> ```

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.cxf.class-generation.exclude-patterns](#quarkus-camel-cxf-class-generation-exclude-patterns)`
For CXF service interfaces to work properly, some ancillary classes (such as request and response wrappers) need to be generated at build time. Camel Quarkus lets the `quarkus-cxf` extension to do this for all service interfaces found in the class path except the ones matching the patterns in this property.

`org.apache.cxf.ws.security.sts.provider.SecurityTokenService` is excluded by default due to [https://issues.apache.org/jira/browse/CXF-8834](https://issues.apache.org/jira/browse/CXF-8834)

 | List of `string` | `org.apache.cxf.ws.security.sts.provider.SecurityTokenService` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.
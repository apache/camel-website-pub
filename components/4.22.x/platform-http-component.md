# Platform HTTP

**Since Camel 3.0**

**Only consumer is supported**

The Platform HTTP is used to allow Camel to use the existing HTTP server from the runtime. For example, when running Camel on Spring Boot, Quarkus, or other runtimes.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-platform-http</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The Platform HTTP component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **handleWriteResponseError** (consumer) | When Camel is complete processing the message, and the HTTP server is writing response. This option controls whether Camel should catch any failure during writing response and store this on the Exchange, which allows onCompletion/UnitOfWork to regard the Exchange as failed and have access to the caused exception from the HTTP server. | false | boolean |
| **requestTimeout** (consumer) | The period in milliseconds after which the request should be timed out. |  | long |
| **serverRequestValidation** (consumer) | Whether HTTP server should do preliminary validation of incoming requests, validating if Content-Type/Accept header, matches what is allowed according to consumes/produces configuration (if set). If validation fails HTTP Status 415/406 is returned. The HTTP server performs this validation before Camel is involved, and as such if validation fails then Camel is never activated. Setting this option to false, allows Camel to process any incoming requests such as to do custom validation or all requests must be handled by Camel. | true | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **engine** (advanced) | An HTTP Server engine implementation to serve the requests. |  | PlatformHttpEngine |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Endpoint Options

The Platform HTTP endpoint is configured using URI syntax:

platform-http:path

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **path** (consumer) | **Required** The path under which this endpoint serves the HTTP requests, for proxy use 'proxy'. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **consumes** (consumer) | The content type this endpoint accepts as an input, such as application/xml or application/json. null or \*/\* mean no restriction. |  | String |
| **cookieDomain** (consumer) | Sets which server can receive cookies. |  | String |
| **cookieHttpOnly** (consumer) | Sets whether to prevent client side scripts from accessing created cookies. | false | boolean |
| **cookieMaxAge** (consumer) | Sets the maximum cookie age in seconds. |  | Long |
| **cookiePath** (consumer) | Sets the URL path that must exist in the requested URL in order to send the Cookie. | / | String |
| **cookieSameSite** (consumer) | 
Sets whether to prevent the browser from sending cookies along with cross-site requests.

Enum values:

-   STRICT
    
-   LAX
    
-   NONE
    





 | Lax | CookieSameSite |
| **cookieSecure** (consumer) | Sets whether the cookie is only sent to the server with an encrypted request over HTTPS. | false | boolean |
| **handleWriteResponseError** (consumer) | When Camel is complete processing the message, and the HTTP server is writing response. This option controls whether Camel should catch any failure during writing response and store this on the Exchange, which allows onCompletion/UnitOfWork to regard the Exchange as failed and have access to the caused exception from the HTTP server. | false | boolean |
| **httpMethodRestrict** (consumer) | A comma separated list of HTTP methods to serve, e.g. GET,POST . If no methods are specified, all methods will be served. |  | String |
| **matchOnUriPrefix** (consumer) | Whether or not the consumer should try to find a target consumer by matching the URI prefix if no exact match is found. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | true | boolean |
| **populateBodyWithForm** (consumer) | Whether to populate the message Body with a Map containing application/x-www-form-urlencoded form properties. | true | boolean |
| **produces** (consumer) | The content type this endpoint produces, such as application/xml or application/json. |  | String |
| **requestTimeout** (consumer) | The period in milliseconds after which the request should be timed out. |  | long |
| **returnHttpRequestHeaders** (consumer) | Whether to include HTTP request headers (Accept, User-Agent, etc.) into HTTP response produced by this endpoint. | false | boolean |
| **useBodyHandler** (consumer) | Whether to use BodyHandler for the request. If set to false then the request will no be read and parsed. | true | boolean |
| **useCookieHandler** (consumer) | Whether to enable the Cookie Handler that allows Cookie addition, expiry, and retrieval (currently only supported by camel-platform-http-vertx). | false | boolean |
| **useStreaming** (consumer) | Whether to use streaming for large requests and responses (currently only supported by camel-platform-http-vertx). | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **fileNameExtWhitelist** (consumer (advanced)) | A comma or whitespace separated list of file extensions. Uploads having these extensions will be stored locally. Null value or asterisk () will allow all files. |  | String |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter headers to and from Camel message. |  | HeaderFilterStrategy |
| **platformHttpEngine** (advanced) | An HTTP Server engine implementation to serve the requests of this endpoint. |  | PlatformHttpEngine |
| **oauthProfile** (security) | OAuth profile name for validating incoming Authorization: Bearer tokens. When set, the request is authenticated before the route is processed. This requires an OAuthTokenValidationFactory; camel-oauth provides the default implementation. |  | String |

## Usage

### Platform HTTP Provider

To use Platform HTTP, a provider (engine) is required to be available on the classpath. The purpose is to have drivers for different runtimes such as Quarkus, or Spring Boot.

To use it with different runtimes:

-   Quarkus
    
-   Spring Boot
    

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-platform-http</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel Quarkus version -->
</dependency>
```

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-platform-http-starter</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel version -->
</dependency>
```

### OAuth Bearer token validation

Platform HTTP consumers can validate incoming `Authorization: Bearer` tokens by setting the `oauthProfile` endpoint option. The profile is resolved through Camel’s `OAuthTokenValidationFactory` SPI. The [camel-oauth](others/oauth.md) component provides the default implementation for standalone Camel applications; runtimes such as Camel Spring Boot or Camel Quarkus can provide their own implementation backed by their native security stack.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-oauth</artifactId>
    <version>x.x.x</version>
</dependency>
```

> **Note**
> If `oauthProfile` is set but no `OAuthTokenValidationFactory` is available on the classpath, the route fails to start. Add `camel-oauth` for the default provider or include a runtime-specific provider from the platform integration.

Camel first checks whether the selected profile has a profile-specific validation factory:

```properties
camel.oauth.myprofile.validation-factory=#bean:myTokenValidationFactory
```

If this property is set, the referenced bean must exist and implement `OAuthTokenValidationFactory`. Otherwise, Camel looks for a single `OAuthTokenValidationFactory` in the registry before falling back to the classpath provider.

-   Java
    
-   XML
    
-   YAML
    

```java
from("platform-http:/secure?oauthProfile=myprofile")
    .to("direct:businessLogic");
```

```xml
<route>
  <from uri="platform-http:/secure?oauthProfile=myprofile"/>
  <to uri="direct:businessLogic"/>
</route>
```

```yaml
- route:
    from:
      uri: platform-http:/secure
      parameters:
        oauthProfile: myprofile
      steps:
        - to:
            uri: direct:businessLogic
```

```properties
camel.oauth.myprofile.jwks-endpoint=https://idp.example.com/.well-known/jwks.json
camel.oauth.myprofile.expected-issuer=https://idp.example.com
camel.oauth.myprofile.expected-audience=my-api
camel.oauth.myprofile.connect-timeout-seconds=5
camel.oauth.myprofile.read-timeout-seconds=10
```

See [camel-oauth](others/oauth.md) for OIDC discovery and opaque-token introspection profile examples.

> **Note**
> Opaque-token introspection performs a blocking outbound HTTP call for every request. For high-traffic endpoints, prefer JWT validation with JWKS when the identity provider publishes signing keys. See [camel-oauth](others/oauth.md) for timeout and validation profile options.

When `oauthProfile` is set, static profile configuration is resolved and validated at route startup. Updates to OAuth profile properties require restarting the route or Camel context before they take effect. Requests without a Bearer token or with an invalid token are rejected with HTTP 401 before the route is processed; missing credentials receive a `WWW-Authenticate: Bearer` response header and invalid tokens receive `WWW-Authenticate: Bearer error="invalid_token"`. Malformed `Authorization` headers are rejected with HTTP 400 and `WWW-Authenticate: Bearer error="invalid_request"`. Token validation infrastructure failures are rejected with HTTP 503. With the Vert.x platform-http engine, Bearer token validation runs before the request body handler, so unauthenticated requests are rejected before body buffering, form parsing, or file uploads. For valid tokens, the token validation result is stored on the exchange as the `CamelOAuthTokenValidationResult` exchange property. Route code can use the result to read the principal name, token scopes, and immutable token attributes/claims. The raw `Authorization` header is removed before the route is invoked and from OAuth rejection responses.

_Java-only: accessing OAuth token validation result in a processor_

```java
import org.apache.camel.component.platform.http.PlatformHttpConstants;
import org.apache.camel.spi.OAuthTokenValidationResult;

from("platform-http:/secure?oauthProfile=myprofile")
    .process(exchange -> {
        OAuthTokenValidationResult result = exchange.getProperty(
                "CamelOAuthTokenValidationResult",
                OAuthTokenValidationResult.class);
        exchange.getMessage().setHeader("X-Principal", result.getName());
    });
```

Configure `expected-issuer` and `expected-audience` for production resource-server routes, and use HTTPS for JWKS, OIDC discovery, and introspection endpoints. The camel-oauth provider rejects missing issuer/audience policy and plain HTTP endpoints by default; use its explicit opt-out properties only for legacy providers or local development. Do not return token validation diagnostic details directly to external clients.

### Implementing a reverse proxy

Platform HTTP component can act as a reverse proxy. In that case, some headers are populated from the absolute URL received on the request line of the HTTP request. Those headers are specific to the underlining platform.

At this moment, this feature is only supported for Quarkus implemented in `camel-platform-http-vertx` component.

### File Attachments handling

Since Apache Camel 4.10, multipart file uploads are easier and harmonized across all runtimes. When a single file is uploaded, the Apache Camel framework provides the following:

-   The Apache Camel message contains:
    
    -   The uploaded file in the message body
        
    -   The file name in the "CamelFileName" message header
        
    -   The file content type in the "CamelFileContentType" message header
        
    -   The file size in the "CamelFileLength" message header
        
    

In case of multiple uploads, the header "CamelAttachmentsSize" contains the number of files uploaded.
# Platform HTTP

JVM since0.3.0 Native since0.3.0

This extension allows for creating HTTP endpoints for consuming HTTP requests.

It is built on top of the Eclipse Vert.x HTTP server provided by the `quarkus-vertx-http` extension.

## What’s inside

-   [Platform HTTP component](../../../../components/4.18.x/platform-http-component.md), URI syntax: `platform-http:path`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-platform-http)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-platform-http</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Basic Usage

Serve all HTTP methods on the `/hello` endpoint:

```java
from("platform-http:/hello").setBody(simple("Hello ${header.name}"));
```

Serve only GET requests on the `/hello` endpoint:

```java
from("platform-http:/hello?httpMethodRestrict=GET").setBody(simple("Hello ${header.name}"));
```

### Using `platform-http` via Camel REST DSL

To be able to use Camel REST DSL with the `platform-http` component, add `camel-quarkus-rest` to your `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-rest</artifactId>
</dependency>
```

Then you can use the Camel REST DSL:

```java
rest()
    .get("/my-get-endpoint")
        .to("direct:handleGetRequest");

    .post("/my-post-endpoint")
        .to("direct:handlePostRequest");
```

### Handling `multipart/form-data` file uploads

You can restrict the uploads to certain file extensions by white listing them:

```java
from("platform-http:/upload/multipart?fileNameExtWhitelist=adoc,txt&httpMethodRestrict=POST")
    .to("log:multipart")
    .process(e -> {
        final AttachmentMessage am = e.getMessage(AttachmentMessage.class);
        if (am.hasAttachments()) {
            am.getAttachments().forEach((fileName, dataHandler) -> {
                try (InputStream in = dataHandler.getInputStream()) {
                    // do something with the input stream
                } catch (IOException ioe) {
                    throw new RuntimeException(ioe);
                }
            });
        }
    });
```

### Securing `platform-http` endpoints

Quarkus provides a variety of security and authentication mechanisms which can be used to secure `platform-http` endpoints. Refer to the [Quarkus Security documentation](https://quarkus.io/guides/security) for further details.

Within a route, it is possible to obtain the authenticated user and its associated `SecurityIdentity` and `Principal`:

```java
from("platform-http:/secure")
    .process(e -> {
        Message message = e.getMessage();
        QuarkusHttpUser user = message.getHeader(VertxPlatformHttpConstants.AUTHENTICATED_USER, QuarkusHttpUser.class);
        SecurityIdentity securityIdentity = user.getSecurityIdentity();
        Principal principal = securityIdentity.getPrincipal();
        // Do something useful with SecurityIdentity / Principal. E.g check user roles etc.
    });
```

Also check the `quarkus.http.body.*` configuration options in [Quarkus documentation](https://quarkus.io/guides/all-config#quarkus-vertx-http_quarkus-vertx-http-eclipse-vert.x-http), esp. `quarkus.http.body.handle-file-uploads`, `quarkus.http.body.uploads-directory` and `quarkus.http.body.delete-uploaded-files-on-end`.

### Implementing a reverse proxy

Platform HTTP component can act as a reverse proxy, in that case `Exchange.HTTP_URI`, `Exchange.HTTP_HOST` headers are populated from the absolute URL received on the request line of the HTTP request.

Here’s an example of an HTTP proxy that simply redirects the Exchange to the origin server.

```java
from("platform-http:proxy")
    .toD("http://"
        + "${headers." + Exchange.HTTP_HOST + "}");
```

### Error handling

If you need to customize the response returned to the client when exceptions are thrown from your routes, then you can use Camel error handling constructs like `doTry`, `doCatch` and `onException`.

For example, to configure a global exception handler in response to a specific Exception type being thrown.

```java
onException(InvalidOrderTotalException.class)
    .handled(true)
    .setHeader(Exchange.HTTP_RESPONSE_CODE).constant(500)
    .setHeader(Exchange.CONTENT_TYPE).constant("text/plain")
    .setBody().constant("The order total was not greater than 100");

from("platform-http:/orders")
    .choice().when().xpath("//order/total > 100")
        .to("direct:processOrder")
    .otherwise()
        .throwException(new InvalidOrderTotalException());
```

You can implement more fine-grained error handling by hooking into the Vert.x Web router initialization with a CDI observer.

```java
void initRouter(@Observes Router router) {
    // Custom 404 handler
    router.errorHandler(404, new Handler<RoutingContext>() {
        @Override
        public void handle(RoutingContext event) {
            event.response()
                .setStatusCode(404)
                .putHeader("Content-Type", "text/plain")
                .end("Sorry - resource not found");
        }
    });
}
```

Note that care should be taken when modifying the router configuration when extensions such as RestEASY are present, since they may register their own error handling logic.

## Additional Camel Quarkus configuration

### Platform HTTP server configuration

Configuration of the platform HTTP server is managed by Quarkus. Refer to the [Quarkus HTTP configuration guide](https://quarkus.io/guides/all-config#quarkus-vertx-http_quarkus-vertx-http-eclipse-vert.x-http) for the full list of configuration options.

To configure SSL for the Platform HTTP server, follow the [secure connections with SSL guide](https://quarkus.io/guides/http-reference#ssl). Note that configuring the server for SSL with `SSLContextParameters` is not currently supported.

### Character encodings

Check the [Character encodings section](../../user-guide/native-mode.html#charsets) of the Native mode guide if you expect your application to send or receive requests using non-default encodings.
# Platform Http Vertx

**Since Camel 3.2**

The camel-platform-http-vertx is a Vert.x based implementation of the `PlatformHttp` SPI.

## Vert.x Route

This implementation will by default lookup an instance of `VertxPlatformHttpRouter` on the registry however you can configure an existing instance using the getter/setter on the `VertxPlatformHttpEngine` class.

## Auto detection from classpath

To use this implementation all you need to do is to add the `camel-platform-http-vertx` dependency to the classpath, and the platform http component should auto-detect this.

## Message Headers

  
| Name | Type | Description |
| --- | --- | --- |
| `CamelVertxPlatformHttpAuthenticatedUser` | `io.vertx.ext.auth.User` | If an authenticated user is present on the Vert.x Web `RoutingContext`, this header is populated with a `User` object continaing the `Principal`. |

Camel also populates **all** request.parameter and Camel also populates **all** request.parameter and request.headers. For example, given a client request with the URL, `http://myserver/myserver?orderid=123`, the exchange will contain a header named `orderid` with the value 123. request.headers. For example, given a client request with the URL, `http://myserver/myserver?orderid=123`, the exchange will contain a header named `orderid` with the value 123.

## VertxPlatformHttpServer

In addition to the implementation of the `PlatformHttp` SPI based on Vert.x, this module provides a Vert.x based HTTP server compatible with the `VertxPlatformHttpEngine`:

```java
final int port = AvailablePortFinder.getNextAvailable();
final CamelContext context = new DefaultCamelContext();

VertxPlatformHttpServerConfiguration conf = new VertxPlatformHttpServerConfiguration();
conf.setBindPort(port);

context.addService(new VertxPlatformHttpServer(conf));
context.addRoutes(new RouteBuilder() {
    @Override
    public void configure() throws Exception {
        from("platform-http:/test")
            .routeId("get")
            .setBody().constant("Hello from Camel's PlatformHttp service");
    }
});

context.start();
```

## Implementing a reverse proxy

Platform HTTP component can act as a reverse proxy, in that case `Exchange.HTTP_URI`, `Exchange.HTTP_HOST` headers are populated from the absolute URL received on the request line of the HTTP request.

Here’s an example of a HTTP proxy that simply redirects the Exchange to the origin server.

```java
from("platform-http:proxy")
    .toD("http://"
        + "${headers." + Exchange.HTTP_HOST + "}");
```
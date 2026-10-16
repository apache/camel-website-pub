# Knative

JVM since2.14.0 Native since2.14.0

Send and receive events from Knative.

## What’s inside

-   [Knative component](../../../../components/next/knative-component.md), URI syntax: `knative:type/typeId`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-knative)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-knative</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

### vertx-websocket with Knative does not work with HTTP/2

The [vertx-websocket](vertx-websocket.md) extension is supported with Knative, but has important protocol compatibility constraints.

WebSocket connections require the HTTP/1.1 upgrade mechanism and are incompatible with HTTP/2. If your Knative application is intended to accept WebSocket connections, it **must not** allow negotiating the HTTP/2 protocol, or else clients will fail to upgrade to the WebSocket protocol.

This creates an incompatibility with the [grpc](grpc.md) extension, which requires HTTP/2.

> **Note**
> If you need to use gRPC with Knative, you must configure HTTP/2 support. See [Using HTTP2 and gRPC](https://docs.redhat.com/en/documentation/red_hat_openshift_serverless/1.31/html/serving/external-and-ingress-routing#using-http2-gRPC_kourier-gateway-service-type) for configuration instructions.

To use WebSockets with Knative:

-   Ensure your Knative service does not negotiate HTTP/2
    
-   Configure ingress gateways and load balancers to use HTTP/1.1 for WebSocket routes
    
-   Do not enable HTTP/2 support if your application accepts WebSocket connections
    

For platform-specific configuration, refer to:

-   [OpenShift Ingress Operator documentation](https://docs.openshift.com/container-platform/4.15/networking/ingress-operator.md)
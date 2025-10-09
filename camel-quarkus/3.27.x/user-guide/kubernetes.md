# Kubernetes

This guide describes different ways to configure and deploy a Camel Quarkus application on kubernetes. It also describes some specific use cases for Knative and Service Binding. == Kubernetes Quarkus supports generating resources for vanilla Kubernetes, OpenShift and Knative. Furthermore, Quarkus can deploy the application to a target Kubernetes cluster by applying the generated manifests to the target cluster’s API Server. More information in the [`Quarkus Kubernetes guide`](https://quarkus.io/guides/deploying-to-kubernetes).

## Knative

The Camel Quarkus extensions whose consumers support Knative deployment are:

-   [`camel-quarkus-cxf-soap`](../reference/extensions/cxf-soap.md)
    
-   [`camel-quarkus-grpc`](../reference/extensions/grpc.md)
    
-   [`camel-quarkus-knative`](../reference/extensions/knative.md)
    
-   [`camel-quarkus-netty-http`](../reference/extensions/netty-http.md)
    
-   [`camel-quarkus-platform-http`](../reference/extensions/platform-http.md)
    
-   [`camel-quarkus-rest`](../reference/extensions/rest.md)
    
-   [`camel-quarkus-servlet`](../reference/extensions/servlet.md)
    
-   [`camel-quarkus-telegram with webhook`](../reference/extensions/telegram.md)
    
-   [`camel-quarkus-vertx-websocket`](../reference/extensions/vertx-websocket.md)
    

## Service binding

Quarkus also supports the [Service Binding Specification for Kubernetes](https://quarkus.io/guides/deploying-to-kubernetes#service_binding) to bind services to applications.

The following Camel Quarkus extensions can be used with Service Binding:

-   [`camel-quarkus-kafka`](../reference/extensions/kafka.md)
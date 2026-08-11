# Kubernetes Namespaces

**Since Camel 2.17**

**Both producer and consumer are supported**

The Kubernetes Namespaces component is one of [Kubernetes Components](kubernetes-summary.md) which provides a producer to execute Kubernetes Namespace operations and a consumer to consume events related to Namespace events.

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

The Kubernetes Namespaces component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **kubernetesClient** (common) | **Autowired** To use an existing kubernetes client. |  | KubernetesClient |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Kubernetes Namespaces endpoint is configured using URI syntax:

kubernetes-namespaces:masterUrl

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **masterUrl** (common) | **Required** URL to a remote Kubernetes API server. This should only be used when your Camel application is connecting from outside Kubernetes. If you run your Camel application inside Kubernetes, then you can use local or client as the URL to tell Camel to run in local mode. If you connect remotely to Kubernetes, then you may also need some of the many other configuration options for secured connection with certificates, etc. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiVersion** (common) | The Kubernetes API Version to use. |  | String |
| **dnsDomain** (common) | The dns domain, used for ServiceCall EIP. |  | String |
| **kubernetesClient** (common) | Default KubernetesClient to use if provided. |  | KubernetesClient |
| **namespace** (common) | The namespace. |  | String |
| **portName** (common) | The port name, used for ServiceCall EIP. |  | String |
| **portProtocol** (common) | The port protocol, used for ServiceCall EIP. | tcp | String |
| **crdGroup** (consumer) | The Consumer CRD Resource Group we would like to watch. |  | String |
| **crdName** (consumer) | The Consumer CRD Resource name we would like to watch. |  | String |
| **crdPlural** (consumer) | The Consumer CRD Resource Plural we would like to watch. |  | String |
| **crdScope** (consumer) | The Consumer CRD Resource Scope we would like to watch. |  | String |
| **crdVersion** (consumer) | The Consumer CRD Resource Version we would like to watch. |  | String |
| **labelKey** (consumer) | The Consumer Label key when watching at some resources. |  | String |
| **labelValue** (consumer) | The Consumer Label value when watching at some resources. |  | String |
| **poolSize** (consumer) | The Consumer pool size. | 1 | int |
| **resourceName** (consumer) | The Consumer Resource Name we would like to watch. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **operation** (producer) | Producer operation to do on Kubernetes. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connectionTimeout** (advanced) | Connection timeout in milliseconds to use when making requests to the Kubernetes API server. |  | Integer |
| **caCertData** (security) | The CA Cert Data. |  | String |
| **caCertFile** (security) | The CA Cert File. |  | String |
| **clientCertData** (security) | The Client Cert Data. |  | String |
| **clientCertFile** (security) | The Client Cert File. |  | String |
| **clientKeyAlgo** (security) | The Key Algorithm used by the client. |  | String |
| **clientKeyData** (security) | The Client Key data. |  | String |
| **clientKeyFile** (security) | The Client Key file. |  | String |
| **clientKeyPassphrase** (security) | The Client Key Passphrase. |  | String |
| **oauthToken** (security) | The Auth Token. |  | String |
| **password** (security) | Password to connect to Kubernetes. |  | String |
| **trustCerts** (security) | Define if the certs we used are trusted anyway or not. | false | Boolean |
| **username** (security) | Username to connect to Kubernetes. |  | String |

## Message Headers

The Kubernetes Namespaces component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelKubernetesOperation** (producer) Constant: [`KUBERNETES_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_OPERATION) | The Producer operation. |  | String |
| **CamelKubernetesNamespaceName** (producer) Constant: [`KUBERNETES_NAMESPACE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_NAMESPACE_NAME) | The namespace name. |  | String |
| **CamelKubernetesNamespaceLabels** (producer) Constant: [`KUBERNETES_NAMESPACE_LABELS`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_NAMESPACE_LABELS) | The namespace labels. |  | Map |
| **CamelKubernetesNamespaceAnnotations** (producer) Constant: [`KUBERNETES_NAMESPACE_ANNOTATIONS`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_NAMESPACE_ANNOTATIONS) | The namespace annotations. |  | Map |
| **CamelKubernetesEventAction** (consumer) Constant: [`KUBERNETES_EVENT_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_EVENT_ACTION) | 
Action watched by the consumer.

Enum values:

-   ADDED
    
-   MODIFIED
    
-   DELETED
    
-   ERROR
    
-   BOOKMARK
    





 |  | Action |
| **CamelKubernetesEventTimestamp** (consumer) Constant: [`KUBERNETES_EVENT_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_EVENT_TIMESTAMP) | Timestamp of the action watched by the consumer. |  | long |

## Usage

### Supported producer operation

-   `listNamespaces`
    
-   `listNamespacesByLabels`
    
-   `getNamespace`
    
-   `createNamespace`
    
-   `updateNamespace`
    
-   `deleteNamespace`
    

## Examples

### Kubernetes Namespaces Producer Examples

-   `listNamespaces`: this operation lists the namespaces on a kubernetes cluster
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:list")
    .to("kubernetes-namespaces:///?kubernetesClient=#kubernetesClient&operation=listNamespaces")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:list"/>
  <to uri="kubernetes-namespaces:///?kubernetesClient=#kubernetesClient&amp;operation=listNamespaces"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:list
    steps:
      - to:
          uri: kubernetes-namespaces:///
          parameters:
            kubernetesClient: "#kubernetesClient"
            operation: listNamespaces
      - to:
          uri: mock:result
```

This operation returns a list of namespaces from your cluster

-   `listNamespacesByLabels`: this operation lists the namespaces by labels on a kubernetes cluster
    

_Java-only: sets a Map header for label selection_

```java
from("direct:listByLabels")
    .process(exchange -> {
        exchange.getIn().setHeader("CamelKubernetesNamespaceLabels",
            Map.of("key1", "value1", "key2", "value2"));
    })
    .to("kubernetes-namespaces:///?kubernetesClient=#kubernetesClient&operation=listNamespacesByLabels")
    .to("mock:result");
```

This operation returns a list of namespaces from your cluster, using a label selector (with key1 and key2, with value value1 and value2)

### Kubernetes Namespaces Consumer Example

-   Java
    
-   XML
    
-   YAML
    

```java
from("kubernetes-namespaces://{{kubernetes-host}}?oauthToken={{kubernetes-token}}")
    .to("log:result");
```

```xml
<route>
  <from uri="kubernetes-namespaces://{{kubernetes-host}}?oauthToken={{kubernetes-token}}"/>
  <to uri="log:result"/>
</route>
```

```yaml
- route:
    from:
      uri: kubernetes-namespaces://{{kubernetes-host}}
      parameters:
        oauthToken: "{{kubernetes-token}}"
    steps:
      - to:
          uri: log:result
```

This consumer returns a message per event received for all Namespaces in the cluster.

You can narrow the scope of the consumer using the following query parameter combinations:

-   `labelKey` + `labelValue` - Watch Namespaces with the specified label.
    
-   `resourceName` - Watch the Namespace with the specified name.
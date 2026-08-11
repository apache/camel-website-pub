# OpenShift Builds

**Since Camel 2.17**

**Only producer is supported**

The Openshift Builds component is one of [Kubernetes Components](kubernetes-summary.md) which provides a producer to execute Openshift builds operations.

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

The OpenShift Builds component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **kubernetesClient** (producer) | **Autowired** To use an existing kubernetes client. |  | KubernetesClient |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OpenShift Builds endpoint is configured using URI syntax:

openshift-builds:masterUrl

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **masterUrl** (producer) | **Required** URL to a remote Kubernetes API server. This should only be used when your Camel application is connecting from outside Kubernetes. If you run your Camel application inside Kubernetes, then you can use local or client as the URL to tell Camel to run in local mode. If you connect remotely to Kubernetes, then you may also need some of the many other configuration options for secured connection with certificates, etc. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiVersion** (producer) | The Kubernetes API Version to use. |  | String |
| **dnsDomain** (producer) | The dns domain, used for ServiceCall EIP. |  | String |
| **kubernetesClient** (producer) | Default KubernetesClient to use if provided. |  | KubernetesClient |
| **namespace** (producer) | The namespace. |  | String |
| **operation** (producer) | Producer operation to do on Kubernetes. |  | String |
| **portName** (producer) | The port name, used for ServiceCall EIP. |  | String |
| **portProtocol** (producer) | The port protocol, used for ServiceCall EIP. | tcp | String |
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

The OpenShift Builds component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelKubernetesOperation** (producer) Constant: [`KUBERNETES_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_OPERATION) | The Producer operation. |  | String |
| **CamelKubernetesNamespaceName** (producer) Constant: [`KUBERNETES_NAMESPACE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_NAMESPACE_NAME) | The namespace name. |  | String |
| **CamelKubernetesBuildsLabels** (producer) Constant: [`KUBERNETES_BUILDS_LABELS`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_BUILDS_LABELS) | The OpenShift build labels. |  | Map |
| **CamelKubernetesBuildName** (producer) Constant: [`KUBERNETES_BUILD_NAME`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_BUILD_NAME) | The OpenShift build name. |  | String |

## Usage

### Supported producer operation

-   `listBuilds`
    
-   `listBuildsByLabels`
    
-   `getBuild`
    

## Examples

### Openshift Builds Producer Examples

-   `listBuilds`: this operation lists the builds on an Openshift cluster
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:list")
    .to("openshift-builds:///?kubernetesClient=#kubernetesClient&operation=listBuilds")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:list"/>
  <to uri="openshift-builds:///?kubernetesClient=#kubernetesClient&amp;operation=listBuilds"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:list
      steps:
        - to:
            uri: openshift-builds:///
            parameters:
              kubernetesClient: "#kubernetesClient"
              operation: listBuilds
        - to:
            uri: mock:result
```

This operation returns a List of Builds from your Openshift cluster

-   `listBuildsByLabels`: this operation lists the builds by labels on an Openshift cluster
    

_Java-only: sets a Map header for label selection_

```java
from("direct:listByLabels")
    .process(exchange -> {
        exchange.getIn().setHeader("CamelKubernetesBuildsLabels",
            Map.of("key1", "value1", "key2", "value2"));
    })
    .to("openshift-builds:///?kubernetesClient=#kubernetesClient&operation=listBuildsByLabels")
    .to("mock:result");
```

This operation returns a list of builds from your cluster using a label selector (with key1 and key2, with value value1 and value2)
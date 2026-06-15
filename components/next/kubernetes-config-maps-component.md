# Kubernetes ConfigMap

**Since Camel 2.17**

**Both producer and consumer are supported**

The Kubernetes ConfigMap component is one of [Kubernetes Components](kubernetes-summary.md) which provides a producer to execute Kubernetes ConfigMap operations and a consumer to consume events related to ConfigMap objects.

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

The Kubernetes ConfigMap component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **kubernetesClient** (common) | **Autowired** To use an existing kubernetes client. |  | KubernetesClient |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Kubernetes ConfigMap endpoint is configured using URI syntax:

kubernetes-config-maps:masterUrl

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **masterUrl** (common) | **Required** URL to a remote Kubernetes API server. This should only be used when your Camel application is connecting from outside Kubernetes. If you run your Camel application inside Kubernetes, then you can use local or client as the URL to tell Camel to run in local mode. If you connect remotely to Kubernetes, then you may also need some of the many other configuration options for secured connection with certificates, etc. |  | String |

### Query Parameters (33 parameters)

   
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

The Kubernetes ConfigMap component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelKubernetesOperation** (producer) Constant: [`KUBERNETES_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_OPERATION) | The Producer operation. |  | String |
| **CamelKubernetesNamespaceName** (producer) Constant: [`KUBERNETES_NAMESPACE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_NAMESPACE_NAME) | The namespace name. |  | String |
| **CamelKubernetesConfigMapsLabels** (producer) Constant: [`KUBERNETES_CONFIGMAPS_LABELS`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_CONFIGMAPS_LABELS) | The ConfigMap labels. |  | Map |
| **CamelKubernetesConfigMapName** (producer) Constant: [`KUBERNETES_CONFIGMAP_NAME`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_CONFIGMAP_NAME) | The ConfigMap name. |  | String |
| **CamelKubernetesConfigData** (producer) Constant: [`KUBERNETES_CONFIGMAP_DATA`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_CONFIGMAP_DATA) | The ConfigMap Data. |  | Map |
| **CamelKubernetesConfigMapsAnnotations** (producer) Constant: [`KUBERNETES_CONFIGMAPS_ANNOTATIONS`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_CONFIGMAPS_ANNOTATIONS) | The ConfigMap annotations. |  | Map |
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

-   `listConfigMaps`
    
-   `listConfigMapsByLabels`
    
-   `getConfigMap`
    
-   `createConfigMap`
    
-   `updateConfigMap`
    
-   `deleteConfigMap`
    

## Examples

### Kubernetes ConfigMaps Producer Examples

-   `listConfigMaps`: this operation lists the configmaps
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:list")
    .to("kubernetes-config-maps:///?kubernetesClient=#kubernetesClient&operation=listConfigMaps")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:list"/>
  <to uri="kubernetes-config-maps:///?kubernetesClient=#kubernetesClient&amp;operation=listConfigMaps"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:list
      steps:
        - to:
            uri: kubernetes-config-maps:///
            parameters:
              kubernetesClient: "#kubernetesClient"
              operation: listConfigMaps
        - to:
            uri: mock:result
```

This operation returns a List of ConfigMaps from your cluster

-   `listConfigMapsByLabels`: this operation lists the configmaps selected by label
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:listByLabels")
    .setHeader(KubernetesConstants.KUBERNETES_CONFIGMAPS_LABELS, constant("key1=value1,key2=value2"))
    .to("kubernetes-config-maps:///?kubernetesClient=#kubernetesClient&operation=listConfigMapsByLabels")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:listByLabels"/>
  <setHeader name="CamelKubernetesConfigMapsLabels">
    <constant>key1=value1,key2=value2</constant>
  </setHeader>
  <to uri="kubernetes-config-maps:///?kubernetesClient=#kubernetesClient&amp;operation=listConfigMapsByLabels"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:listByLabels
      steps:
        - setHeader:
            name: CamelKubernetesConfigMapsLabels
            expression:
              constant:
                expression: key1=value1,key2=value2
        - to:
            uri: kubernetes-config-maps:///
            parameters:
              kubernetesClient: "#kubernetesClient"
              operation: listConfigMapsByLabels
        - to:
            uri: mock:result
```

This operation returns a List of ConfigMaps from your cluster, using a label selector (with key1 and key2, with value value1 and value2)

### Kubernetes ConfigMaps Consumer Example

```java
fromF("kubernetes-config-maps://%s?oauthToken=%s", host, authToken)
    .process(new KubernetesProcessor()).to("mock:result");

    public class KubernetesProcessor implements Processor {
        @Override
        public void process(Exchange exchange) throws Exception {
            Message in = exchange.getIn();
            ConfigMap cm = exchange.getIn().getBody(ConfigMap.class);
            log.info("Got event with configmap name: " + cm.getMetadata().getName() + " and action " + in.getHeader(KubernetesConstants.KUBERNETES_EVENT_ACTION));
        }
    }
```

This consumer returns a message per event received for all ConfigMaps from all namespaces in the cluster.

You can narrow the scope of the consumer using the following query parameter combinations:

-   `labelKey` + `labelValue` - Watch ConfigMaps with the specified label in any namespace.
    
-   `namespace` - Watch all ConfigMaps in the specified namespace.
    
-   `namespace` + `resourceName` - Watch the ConfigMap with the specified name in the given namespace.
    
-   `namespace` + `labelKey` + `labelValue` - Watch ConfigMaps with the specified label in the given namespace.
    

## Using configmap properties function with Kubernetes

The `camel-kubernetes` component include the following configmap related functions:

-   `configmap` - A function to lookup the string property from Kubernetes ConfigMaps.
    
-   `configmap-binary` - A function to lookup the binary property from Kubernetes ConfigMaps.
    

Camel reads Configmaps from the Kubernetes API Server. And when RBAC is enabled on the cluster, the ServiceAccount that is used to run the application needs to have the proper permissions for such access.

Before the Kubernetes property placeholder functions can be used they need to be configured with either (or both)

-   path - A _mount path_ that must be mounted to the running pod, to load the configmaps or secrets from local disk.
    
-   kubernetes client - **Autowired** An `io.fabric8.kubernetes.client.KubernetesClient` instance to use for connecting to the Kubernetes API server.
    

Camel will first use _mount paths_ (if configured) to lookup, and then fallback to use the `KubernetesClient`.

### Using configmap with Kubernetes

Given a configmap named `myconfig` in Kubernetes that has two entries:

```properties
drink = beer
first = Carlsberg
```

Then these values can be used in your Camel routes such as:

```xml
<camelContext>
  <route>
    <from uri="direct:start"/>
    <log message="What {{configmap:myconfig/drink}} do you want?"/>
    <log message="I want {{configmap:myconfig/first}}"/>
  </route>
</camelContext>
```

You can also provide a default value in case a key does not exist:

```xml
    <log message="I want {{configmap:myconfig/second:Heineken}}"/>
```

## Automatic Camel context reloading on Configmaps Refresh

Being able to reload Camel context on a Configmap Refresh could be done by specifying the following properties:

```properties
camel.vault.kubernetescm.refreshEnabled=true
camel.vault.kubernetescm.configmaps=Configmap
camel.main.context-reload-enabled = true
```

where `camel.vault.kubernetescm.refreshEnabled` will enable the automatic context reload and `camel.vault.kubernetescm.configmaps` is a regex representing or a comma separated lists of the configmaps we want to track for updates.

Whenever a configmap listed in the property, will be updated in the same namespace of the running application, the Camel context will be reloaded, refreshing the configmap value.

## Spring Boot Auto-Configuration

When using kubernetes-config-maps with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-kubernetes-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 91 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.kubernetes-config-maps.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-config-maps.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-config-maps.enabled** | Whether to enable auto configuration of the kubernetes-config-maps component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-config-maps.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-config-maps.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-cronjob.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-cronjob.enabled** | Whether to enable auto configuration of the kubernetes-cronjob component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-cronjob.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-cronjob.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-custom-resources.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-custom-resources.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-custom-resources.enabled** | Whether to enable auto configuration of the kubernetes-custom-resources component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-custom-resources.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-custom-resources.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-deployments.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-deployments.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-deployments.enabled** | Whether to enable auto configuration of the kubernetes-deployments component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-deployments.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-deployments.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-events.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-events.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-events.enabled** | Whether to enable auto configuration of the kubernetes-events component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-events.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-events.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-hpa.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-hpa.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-hpa.enabled** | Whether to enable auto configuration of the kubernetes-hpa component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-hpa.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-hpa.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-job.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-job.enabled** | Whether to enable auto configuration of the kubernetes-job component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-job.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-job.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-namespaces.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-namespaces.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-namespaces.enabled** | Whether to enable auto configuration of the kubernetes-namespaces component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-namespaces.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-namespaces.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-nodes.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-nodes.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-nodes.enabled** | Whether to enable auto configuration of the kubernetes-nodes component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-nodes.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-nodes.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-persistent-volumes-claims.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-persistent-volumes-claims.enabled** | Whether to enable auto configuration of the kubernetes-persistent-volumes-claims component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-persistent-volumes-claims.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-persistent-volumes-claims.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-persistent-volumes.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-persistent-volumes.enabled** | Whether to enable auto configuration of the kubernetes-persistent-volumes component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-persistent-volumes.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-persistent-volumes.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-pods.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-pods.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-pods.enabled** | Whether to enable auto configuration of the kubernetes-pods component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-pods.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-pods.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-replication-controllers.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-replication-controllers.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-replication-controllers.enabled** | Whether to enable auto configuration of the kubernetes-replication-controllers component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-replication-controllers.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-replication-controllers.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-resources-quota.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-resources-quota.enabled** | Whether to enable auto configuration of the kubernetes-resources-quota component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-resources-quota.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-resources-quota.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-secrets.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-secrets.enabled** | Whether to enable auto configuration of the kubernetes-secrets component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-secrets.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-secrets.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-service-accounts.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-service-accounts.enabled** | Whether to enable auto configuration of the kubernetes-service-accounts component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-service-accounts.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-service-accounts.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-services.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-services.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-services.enabled** | Whether to enable auto configuration of the kubernetes-services component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-services.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-services.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openshift-build-configs.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openshift-build-configs.enabled** | Whether to enable auto configuration of the openshift-build-configs component. This is enabled by default. |  | Boolean |
| **camel.component.openshift-build-configs.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.openshift-build-configs.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openshift-builds.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openshift-builds.enabled** | Whether to enable auto configuration of the openshift-builds component. This is enabled by default. |  | Boolean |
| **camel.component.openshift-builds.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.openshift-builds.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openshift-deploymentconfigs.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openshift-deploymentconfigs.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.openshift-deploymentconfigs.enabled** | Whether to enable auto configuration of the openshift-deploymentconfigs component. This is enabled by default. |  | Boolean |
| **camel.component.openshift-deploymentconfigs.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.openshift-deploymentconfigs.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
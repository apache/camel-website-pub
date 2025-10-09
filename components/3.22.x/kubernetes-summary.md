# Kubernetes

**Since Camel 2.17**

The Kubernetes components integrate your application with Kubernetes standalone or on top of Openshift.

## Kubernetes components

See the following for usage of each component:

[Kubernetes ConfigMap](kubernetes-config-maps-component.md)

Perform operations on Kubernetes ConfigMaps and get notified on ConfigMaps changes.

[Kubernetes Custom Resources](kubernetes-custom-resources-component.md)

Perform operations on Kubernetes Custom Resources and get notified on Deployment changes.

[Kubernetes Deployments](kubernetes-deployments-component.md)

Perform operations on Kubernetes Deployments and get notified on Deployment changes.

[Kubernetes Event](kubernetes-events-component.md)

Perform operations on Kubernetes Events and get notified on Events changes.

[Kubernetes HPA](kubernetes-hpa-component.md)

Perform operations on Kubernetes Horizontal Pod Autoscalers (HPA) and get notified on HPA changes.

[Kubernetes Job](kubernetes-job-component.md)

Perform operations on Kubernetes Jobs.

[Kubernetes Namespaces](kubernetes-namespaces-component.md)

Perform operations on Kubernetes Namespaces and get notified on Namespace changes.

[Kubernetes Nodes](kubernetes-nodes-component.md)

Perform operations on Kubernetes Nodes and get notified on Node changes.

[Kubernetes Persistent Volume](kubernetes-persistent-volumes-component.md)

Perform operations on Kubernetes Persistent Volumes and get notified on Persistent Volume changes.

[Kubernetes Persistent Volume Claim](kubernetes-persistent-volumes-claims-component.md)

Perform operations on Kubernetes Persistent Volumes Claims and get notified on Persistent Volumes Claim changes.

[Kubernetes Pods](kubernetes-pods-component.md)

Perform operations on Kubernetes Pods and get notified on Pod changes.

[Kubernetes Replication Controller](kubernetes-replication-controllers-component.md)

Perform operations on Kubernetes Replication Controllers and get notified on Replication Controllers changes.

[Kubernetes Resources Quota](kubernetes-resources-quota-component.md)

Perform operations on Kubernetes Resources Quotas.

[Kubernetes Secrets](kubernetes-secrets-component.md)

Perform operations on Kubernetes Secrets.

[Kubernetes Service Account](kubernetes-service-accounts-component.md)

Perform operations on Kubernetes Service Accounts.

[Kubernetes Services](kubernetes-services-component.md)

Perform operations on Kubernetes Services and get notified on Service changes.

[Openshift Build Config](openshift-build-configs-component.md)

Perform operations on OpenShift Build Configs.

[Openshift Builds](openshift-builds-component.md)

Perform operations on OpenShift Builds.

[Openshift Deployment Configs](openshift-deploymentconfigs-component.md)

Perform operations on Openshift Deployment Configs and get notified on Deployment Config changes.

## Installation

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-kubernetes</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Usage

### Producer examples

Here we show some examples of producer using camel-kubernetes.

### Create a pod

```java
from("direct:createPod")
    .toF("kubernetes-pods://%s?oauthToken=%s&operation=createPod", host, authToken);
```

By using the KubernetesConstants.KUBERNETES\_POD\_SPEC header you can specify your PodSpec and pass it to this operation.

### Delete a pod

```java
from("direct:createPod")
    .toF("kubernetes-pods://%s?oauthToken=%s&operation=deletePod", host, authToken);
```

By using the KubernetesConstants.KUBERNETES\_POD\_NAME header you can specify your Pod name and pass it to this operation.

## Using Kubernetes ConfigMaps and Secrets

The `camel-kubernetes` component also provides [Property Placeholder](../../manual/using-propertyplaceholder.md) functions that loads the property values from Kubernetes _ConfigMaps_ or _Secrets_.

For more information see [Property Placeholder](../../manual/using-propertyplaceholder.md).

## Spring Boot Auto-Configuration

When using kubernetes with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-kubernetes-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 102 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.cluster.kubernetes.attributes** | Custom service attributes. |  | Map |
| **camel.cluster.kubernetes.cluster-labels** | Set the labels used to identify the pods composing the cluster. |  | Map |
| **camel.cluster.kubernetes.config-map-name** | Set the name of the ConfigMap used to do optimistic locking (defaults to 'leaders'). |  | String |
| **camel.cluster.kubernetes.connection-timeout-millis** | Connection timeout in milliseconds to use when making requests to the Kubernetes API server. |  | Integer |
| **camel.cluster.kubernetes.enabled** | Sets if the Kubernetes cluster service should be enabled or not, default is false. | false | Boolean |
| **camel.cluster.kubernetes.id** | Cluster Service ID. |  | String |
| **camel.cluster.kubernetes.jitter-factor** | A jitter factor to apply in order to prevent all pods to call Kubernetes APIs in the same instant. |  | Double |
| **camel.cluster.kubernetes.kubernetes-namespace** | Set the name of the Kubernetes namespace containing the pods and the configmap (autodetected by default). |  | String |
| **camel.cluster.kubernetes.lease-duration-millis** | The default duration of the lease for the current leader. |  | Long |
| **camel.cluster.kubernetes.master-url** | Set the URL of the Kubernetes master (read from Kubernetes client properties by default). |  | String |
| **camel.cluster.kubernetes.order** | Service lookup order/priority. |  | Integer |
| **camel.cluster.kubernetes.pod-name** | Set the name of the current pod (autodetected from container host name by default). |  | String |
| **camel.cluster.kubernetes.renew-deadline-millis** | The deadline after which the leader must stop its services because it may have lost the leadership. |  | Long |
| **camel.cluster.kubernetes.retry-period-millis** | The time between two subsequent attempts to check and acquire the leadership. It is randomized using the jitter factor. |  | Long |
| **camel.component.kubernetes-config-maps.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-config-maps.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-config-maps.enabled** | Whether to enable auto configuration of the kubernetes-config-maps component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-config-maps.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-config-maps.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-custom-resources.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-custom-resources.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-custom-resources.enabled** | Whether to enable auto configuration of the kubernetes-custom-resources component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-custom-resources.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-custom-resources.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-deployments.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-deployments.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-deployments.enabled** | Whether to enable auto configuration of the kubernetes-deployments component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-deployments.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-deployments.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-events.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-events.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-events.enabled** | Whether to enable auto configuration of the kubernetes-events component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-events.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-events.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-hpa.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-hpa.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-hpa.enabled** | Whether to enable auto configuration of the kubernetes-hpa component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-hpa.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-hpa.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-job.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-job.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-job.enabled** | Whether to enable auto configuration of the kubernetes-job component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-job.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-job.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-namespaces.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-namespaces.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-namespaces.enabled** | Whether to enable auto configuration of the kubernetes-namespaces component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-namespaces.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-namespaces.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-nodes.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-nodes.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
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
| **camel.component.kubernetes-pods.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-pods.enabled** | Whether to enable auto configuration of the kubernetes-pods component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-pods.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-pods.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-replication-controllers.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-replication-controllers.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
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
| **camel.component.kubernetes-services.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
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
| **camel.component.openshift-deploymentconfigs.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.openshift-deploymentconfigs.enabled** | Whether to enable auto configuration of the openshift-deploymentconfigs component. This is enabled by default. |  | Boolean |
| **camel.component.openshift-deploymentconfigs.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.openshift-deploymentconfigs.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
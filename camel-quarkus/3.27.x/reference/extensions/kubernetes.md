# Kubernetes

JVM since1.0.0 Native since1.0.0

Perform operations against Kubernetes API

## What’s inside

-   [Kubernetes ConfigMap component](../../../../components/4.14.x/kubernetes-config-maps-component.md), URI syntax: `kubernetes-config-maps:masterUrl`
    
-   [Kubernetes Cronjob component](../../../../components/4.14.x/kubernetes-cronjob-component.md), URI syntax: `kubernetes-cronjob:masterUrl`
    
-   [Kubernetes Custom Resources component](../../../../components/4.14.x/kubernetes-custom-resources-component.md), URI syntax: `kubernetes-custom-resources:masterUrl`
    
-   [Kubernetes Deployments component](../../../../components/4.14.x/kubernetes-deployments-component.md), URI syntax: `kubernetes-deployments:masterUrl`
    
-   [Kubernetes Event component](../../../../components/4.14.x/kubernetes-events-component.md), URI syntax: `kubernetes-events:masterUrl`
    
-   [Kubernetes HPA component](../../../../components/4.14.x/kubernetes-hpa-component.md), URI syntax: `kubernetes-hpa:masterUrl`
    
-   [Kubernetes Job component](../../../../components/4.14.x/kubernetes-job-component.md), URI syntax: `kubernetes-job:masterUrl`
    
-   [Kubernetes Namespaces component](../../../../components/4.14.x/kubernetes-namespaces-component.md), URI syntax: `kubernetes-namespaces:masterUrl`
    
-   [Kubernetes Nodes component](../../../../components/4.14.x/kubernetes-nodes-component.md), URI syntax: `kubernetes-nodes:masterUrl`
    
-   [Kubernetes Persistent Volume component](../../../../components/4.14.x/kubernetes-persistent-volumes-component.md), URI syntax: `kubernetes-persistent-volumes:masterUrl`
    
-   [Kubernetes Persistent Volume Claim component](../../../../components/4.14.x/kubernetes-persistent-volumes-claims-component.md), URI syntax: `kubernetes-persistent-volumes-claims:masterUrl`
    
-   [Kubernetes Pods component](../../../../components/4.14.x/kubernetes-pods-component.md), URI syntax: `kubernetes-pods:masterUrl`
    
-   [Kubernetes Replication Controller component](../../../../components/4.14.x/kubernetes-replication-controllers-component.md), URI syntax: `kubernetes-replication-controllers:masterUrl`
    
-   [Kubernetes Resources Quota component](../../../../components/4.14.x/kubernetes-resources-quota-component.md), URI syntax: `kubernetes-resources-quota:masterUrl`
    
-   [Kubernetes Secrets component](../../../../components/4.14.x/kubernetes-secrets-component.md), URI syntax: `kubernetes-secrets:masterUrl`
    
-   [Kubernetes Service Account component](../../../../components/4.14.x/kubernetes-service-accounts-component.md), URI syntax: `kubernetes-service-accounts:masterUrl`
    
-   [Kubernetes Services component](../../../../components/4.14.x/kubernetes-services-component.md), URI syntax: `kubernetes-services:masterUrl`
    
-   [OpenShift Build Config component](../../../../components/4.14.x/openshift-build-configs-component.md), URI syntax: `openshift-build-configs:masterUrl`
    
-   [OpenShift Builds component](../../../../components/4.14.x/openshift-builds-component.md), URI syntax: `openshift-builds:masterUrl`
    
-   [OpenShift Deployment Configs component](../../../../components/4.14.x/openshift-deploymentconfigs-component.md), URI syntax: `openshift-deploymentconfigs:masterUrl`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-kubernetes)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-kubernetes</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

### Automatic registration of a Kubernetes Client instance

The extension automatically registers a Kubernetes Client bean named `kubernetesClient`. You can reference the bean in your routes like this:

```java
from("direct:pods")
    .to("kubernetes-pods:///?kubernetesClient=#kubernetesClient&operation=listPods")
```

Or you can omit referring to the client bean entirely and the Kubernetes component will automatically use the Kubernetes client that was autowired.

```java
from("direct:pods")
    .to("kubernetes-pods:local?operation=listPods")
```

By default, the client is configured from the local kubeconfig file. You can customize the client configuration via properties within `application.properties`:

```properties
quarkus.kubernetes-client.master-url=https://my.k8s.host
quarkus.kubernetes-client.namespace=my-namespace
```

The full set of configuration options are documented in the [Quarkus Kubernetes Client guide](https://quarkus.io/guides/kubernetes-client#quarkus-kubernetes-client_configuration).

If you want to suppress this behavior, you can disable autowiring and all configuration will be driven from the documented component and endpoint options.

To disable autowiring at the component level, add the following configuration to `application.properties`.

```properties
camel.component.kubernetes-pods.autowired-enabled=false
```

To disable autowiring at the endpoint level.

```java
from("direct:pods")
    .to("kubernetes-pods:https://my.cluster.host?autowiredEnabled=false&operation=listPods")
```

### OpenShift specific components

When using any of the OpenShift specific components:

-   `openenshift-build-configs`
    
-   `openenshift-builds`
    
-   `openshift-deploymentconfigs`
    

You must add the following dependency to your application.

```xml
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-openshift-client</artifactId>
</dependency>
```

### Having only a single consumer in a cluster consuming from a given endpoint

This functionality is provided by the `camel-quarkus-kubernetes-cluster-service` extension. Refer to the [extension documentation](kubernetes-cluster-service.md) for more information.
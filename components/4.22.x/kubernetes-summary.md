# Kubernetes

**Since Camel 2.17**

The Kubernetes components integrate your application with Kubernetes standalone or on top of Openshift.

## Kubernetes components

See the following for usage of each component:

[Kubernetes ConfigMap](kubernetes-config-maps-component.md)

Perform operations on Kubernetes ConfigMaps and get notified on ConfigMaps changes.

[Kubernetes Cronjob](kubernetes-cronjob-component.md)

Perform operations on Kubernetes CronJob.

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

[OpenShift Build Config](openshift-build-configs-component.md)

Perform operations on OpenShift Build Configs.

[OpenShift Builds](openshift-builds-component.md)

Perform operations on OpenShift Builds.

[OpenShift Deployment Configs](openshift-deploymentconfigs-component.md)

Perform operations on OpenShift Deployment Configs and get notified on Deployment Config changes.

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

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createPod")
    .to("kubernetes-pods://{{kubernetes-host}}?oauthToken={{kubernetes-token}}&operation=createPod");
```

```xml
<route>
  <from uri="direct:createPod"/>
  <to uri="kubernetes-pods://{{kubernetes-host}}?oauthToken={{kubernetes-token}}&amp;operation=createPod"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createPod
    steps:
      - to:
          uri: kubernetes-pods://{{kubernetes-host}}
          parameters:
            oauthToken: "{{kubernetes-token}}"
            operation: createPod
```

By using the `CamelKubernetesPodSpec` header, you can specify your PodSpec and pass it to this operation.

### Delete a pod

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deletePod")
    .to("kubernetes-pods://{{kubernetes-host}}?oauthToken={{kubernetes-token}}&operation=deletePod");
```

```xml
<route>
  <from uri="direct:deletePod"/>
  <to uri="kubernetes-pods://{{kubernetes-host}}?oauthToken={{kubernetes-token}}&amp;operation=deletePod"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:deletePod
    steps:
      - to:
          uri: kubernetes-pods://{{kubernetes-host}}
          parameters:
            oauthToken: "{{kubernetes-token}}"
            operation: deletePod
```

By using the `CamelKubernetesPodName` header, you can specify your Pod name and pass it to this operation.

## Using Kubernetes ConfigMaps and Secrets

The `camel-kubernetes` component also provides [Property Placeholder](../../manual/using-propertyplaceholder.md) functions that load the property values from Kubernetes _ConfigMaps_ or _Secrets_.

For more information, see [Property Placeholder](../../manual/using-propertyplaceholder.md).
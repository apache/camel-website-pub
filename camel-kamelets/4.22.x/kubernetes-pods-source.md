# ![kubernetes pods source](_images/kamelets/kubernetes-pods-source.svg) Kubernetes Pods Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume Events from Kubernetes Pods

## Configuration Options

The following table summarizes the configuration options available for the `kubernetes-pods-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **masterUrl** | Kubernetes Master URL | **Required** The Kubernetes Cluster Master URL. | string |  |  |
| **token** | Oauth Token | **Required** The Auth Token to connect to Kubernetes Cluster. | string |  |  |
| **resourceName** | Resource Name | The Resource Name we want to watch. | string |  |  |

## Dependencies

At runtime, the `kubernetes-pods-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kubernetes
    
-   camel:kamelet
    
-   camel:jackson
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:kubernetes-pods-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kubernetes-pods-source Kamelet Description

### Authentication methods

This Kamelet connects to Kubernetes using:

-   Service account authentication (recommended in cluster)
    
-   Kubeconfig file authentication
    
-   Token-based authentication
    

### Output format

The Kamelet watches Kubernetes pods resources and produces event data in JSON format when resources are created, updated, or deleted.

### Configuration

The Kamelet supports various Kubernetes connection parameters:

-   `namespace`: The Kubernetes namespace to watch (optional)
    
-   Authentication and connection configuration
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kubernetes-pods-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kubernetes-pods-source
    properties:
      namespace: "default"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kubernetes-pods-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kubernetes-pods-source.kamelet.yaml)
# ![kubernetes namespaces source](_images/kamelets/kubernetes-namespaces-source.svg) Kubernetes Namespaces Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Watches the namespaces of a Kubernetes cluster and sends a message each time a namespace is created, changed or deleted.

Use it to react when teams or applications are added to or removed from a cluster, for example to set up monitoring, quotas or access for each new namespace. For pods or nodes, use `kubernetes-pods-source` or `kubernetes-nodes-source`.

Output: the body is the namespace as JSON text, in the same shape as `kubectl get namespace <name> -o json`. The `CamelKubernetesEventAction` header says what happened: `ADDED`, `MODIFIED` or `DELETED`.

Good to know: when it starts, it first sends an `ADDED` message for every namespace that already exists. The token must be allowed to list and watch namespaces, which is a cluster-wide permission.

## Configuration Options

The following table summarizes the configuration options available for the `kubernetes-namespaces-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **masterUrl** | Kubernetes Master URL | **Required** The address of the Kubernetes API server, as a URL that starts with `https://`, such as the `server` of the cluster in your kubeconfig file. | string |  | https://my-cluster.example.com:6443 |
| **token** | Token | **Required** A bearer token to log in to the Kubernetes API with, such as the token of a service account created with `kubectl create token <service-account>`. | string |  |  |

## Dependencies

At runtime, the `kubernetes-namespaces-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:kubernetes-namespaces-source"
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

## Kubernetes-namespaces-source Kamelet Description

### Authentication methods

This Kamelet connects to the Kubernetes API server given by `masterUrl` with a bearer token, the `token` option, such as the token of a service account created with `kubectl create token <service-account>`. The token must be allowed to list and watch namespaces.

### Output format

The Kamelet watches Kubernetes namespaces resources and produces a message when one is created, updated, or deleted. The body is the resource as JSON text, and the `CamelKubernetesEventAction` header says what happened (`ADDED`, `MODIFIED` or `DELETED`).

### Configuration

The Kamelet requires `masterUrl` and `token`, and watches all the namespaces of the cluster.

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kubernetes-namespaces-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kubernetes-namespaces-source
    properties:
      masterUrl: "https://my-cluster.example.com:6443"
      token: "{{kubernetes-token}}"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kubernetes-namespaces-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kubernetes-namespaces-source.kamelet.yaml)
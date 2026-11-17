# ![kubernetes nodes source](_images/kamelets/kubernetes-nodes-source.svg) Kubernetes Nodes Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Watches the nodes (the machines) of a Kubernetes cluster and sends a message each time a node is added, changed or removed.

Use it to react to changes in the capacity or the health of a cluster, for example to alert when a node is not ready or when a node joins or leaves. For pods or namespaces, use `kubernetes-pods-source` or `kubernetes-namespaces-source`.

Output: the body is the node as JSON text, in the same shape as `kubectl get node <name> -o json`. The `CamelKubernetesEventAction` header says what happened: `ADDED`, `MODIFIED` or `DELETED`.

Good to know: when it starts, it first sends an `ADDED` message for every node that already exists. The status of a node is updated often, so expect many `MODIFIED` messages. The token must be allowed to list and watch nodes, which is a cluster-wide permission.

## Configuration Options

The following table summarizes the configuration options available for the `kubernetes-nodes-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **masterUrl** | Kubernetes Master URL | **Required** The address of the Kubernetes API server, as a URL that starts with `https://`, such as the `server` of the cluster in your kubeconfig file. | string |  | https://my-cluster.example.com:6443 |
| **token** | Token | **Required** A bearer token to log in to the Kubernetes API with, such as the token of a service account created with `kubectl create token <service-account>`. | string |  |  |
| **resourceName** | Resource Name | The name of the one node to watch. When it is not set, all the nodes are watched. | string |  | worker-1 |

## Dependencies

At runtime, the `kubernetes-nodes-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:kubernetes-nodes-source"
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

## Kubernetes-nodes-source Kamelet Description

### Authentication methods

This Kamelet connects to the Kubernetes API server given by `masterUrl` with a bearer token, the `token` option, such as the token of a service account created with `kubectl create token <service-account>`. The token must be allowed to list and watch nodes.

### Output format

The Kamelet watches Kubernetes nodes resources and produces a message when one is created, updated, or deleted. The body is the resource as JSON text, and the `CamelKubernetesEventAction` header says what happened (`ADDED`, `MODIFIED` or `DELETED`).

### Configuration

The Kamelet requires `masterUrl` and `token`. Set `resourceName` to watch only one node.

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kubernetes-nodes-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kubernetes-nodes-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kubernetes-nodes-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kubernetes-nodes-source.kamelet.yaml)
# Camel K operator installation

Camel K allows us to run Camel integrations directly on a Kubernetes cluster. To use it, you need to be connected to a cloud environment or to a local cluster created for development purposes (ie, Minikube or Kind).

## Container registry configuration

You will need a container registry available in order to push and pull the generated Camel applications. The easiest way to configure it is to store the configuration on a Configmap which will be used by the operator:

```none
kubectl create configmap camel-k-operator-configmap-configuration \
  --from-literal=REGISTRY_ADDRESS="docker.io" \
  --from-literal=REGISTRY_SECRET="my-docker-secret"
```

Have a further look at the [production ready registry configuration documentation](registry.md).

You can now install and run the Camel K operator. You can do it via any of the following methodologies:

## Installation via Kustomize

[Kustomize](https://kustomize.io) provides a declarative approach to the configuration customization of a Camel-K installation. Kustomize works either with a standalone executable or as a built-in to `kubectl`. The [/install](https://github.com/apache/camel-k/tree/main/install) directory provides a series of base and overlays configuration that you can use. You can create your own overlays or customize the one available in the repository to accommodate your need.

$ kubectl create ns camel-k
$ kubectl apply -k github.com/apache/camel-k/install/overlays/all-namespaces?ref=v2.10.1 --server-side

You can specify as `ref` parameter the version you’re willing to install (ie, `v2.10.1`). The command above will install a descoped (global) operator in the camel-k namespace. This is the suggested configuration in order to manage Integrations in all namespaces.

## Installation via Helm Hub

Camel K is available in Helm Hub:

```none
$ helm repo add camel-k https://apache.github.io/camel-k/charts/
$ helm install camel-k camel-k/camel-k -n camel-k
```

More instructions on the [Camel K Helm](https://hub.helm.sh/charts/camel-k/camel-k) page.

## Installation via Operator Hub

Camel K is also available in Operator Hub. You will need the OLM framework to be properly installed in your cluster. More instructions on the [Camel K Operator Hub](https://operatorhub.io/operator/camel-k) page.

```none
$ kubectl create -f https://operatorhub.io/install/camel-k.yaml
```

You can edit the `Subscription` custom resource, setting the channel you want to use. From Camel K version 2 onward, we’re going to provide an installation channel for each major version we’re releasing (ie, `stable-v2`). This will simplify the upgrade process if you choose to perform an automatic upgrade.

> **Note**
> Some Kubernetes clusters such as Openshift may let you to perform the same operation from a GUI as well. Refer to the cluster instruction to learn how to perform such action from user interface.

## Installation topology

When you decide to install the operator, you can decide to install the following topology:

-   Global operator: a single global operator watching all namespaces.
    
-   Own namespace operator: a namespaces operator watching its own namespace only.
    
-   Single namespace operator: an operator installed in a namespace and watching another namespace.
    
-   Multi namespace operator: an operator installed in a namespace and watching multiple namespaces.
    

The namespace(s) to watch is configured via `WATCH_NAMESPACE` variable in the operator `Deployment` resource. You can provide an empty value (watch all namespaces), a single value (watch either the own namespace or any other namespace) or a comma separated value (watching as many namespaces as provided).

It’s important to notice that when running the single or multiple namespace operator, you _may_ need to provide the RBACs which are expected by the operator to run properly. For such a configuration you can take as a reference the `Kustomize` examples available in `/install/overlays/single-namespace/` and `/install/overlays/multi-namespace/`. The last topology is probably the most secure as it will avoid the operator to access to any resource outside those namespaces for which you’ve provided the proper security rules.

> **Note**
> RBAC custom configuration may vary depending on the installation methodology.

## Setup the operator configuration

Each installation method have its proper way to setup configuration. A common one is the creation of a `Configmap` named `camel-k-operator-configmap-configuration` and a `Secret` named `camel-k-operator-secret-configuration` in the same namespace where the operator is installed. If available, the operator will read the environment variable from these resources.

## Verify that the operator is up and running

In order to verify that the operator is up and running, you should be able to see a Camel K operator `Pod` running in the namespace used, for example:

```none
kubectl get pods -n camel-k
NAME                                READY   STATUS    RESTARTS   AGE
camel-k-operator-5b686db99f-c2k2s   1/1     Running   0          3m46s
```

## Run some integration

Once you’ve completed any of the above installation procedure, you’ll be ready to [run some integrations](../running/running.md).

## Special clusters requirements

Camel K installation is usually straightforward, but for certain cluster types you need to apply specific configuration settings before installing it. You need customized instructions for the following cluster types:

-   [Google Kubernetes Engine (GKE)](platform/gke.md)
    
-   [IBM Kubernetes Services (IKS)](platform/iks.md)
    

## Fine Tuning

Camel K installation can be configured with certain special settings available for experienced users. You can manage resources such as limiting memory and CPU, provide a policy for `Pod` scheduling and `Toleration`. Please have a look at [Camel K fine tuning](advanced/advanced.md) to learn more about advanced configuration.
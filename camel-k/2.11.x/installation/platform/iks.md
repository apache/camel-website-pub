# Installing Camel K on IBM Kubernetes Service (IKS)

This guide assumes you’ve already created an IBM Kubernetes cluster on [https://cloud.ibm.com](https://cloud.ibm.com), also installed the [IBM Command line tool](https://cloud.ibm.com/docs/cli?topic=cli-install-ibmcloud-cli) and `kubectl` command.

On the list of kubernetes clusters for you account, you need to select the cluster and copy the (_clusterId_) to add the cluster: `ibmcloud ks cluster config --cluster <clusterid>`

After executing the configuration string, you should be able to execute:

```none
kubectl get pods --all-namespaces
```

> **Note**
> IKS provide an internal container registry feature. Camel K is able to leverage that registry.
>
> You could create a customized namespace on [IBM container registry](../registry/special/icr.md) in order to host your integration images. Please take note of the namespace and region created to configure them on the installation step.

You can now install via [standard installation](../installation.md).
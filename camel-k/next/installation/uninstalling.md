# Uninstalling Camel K

We’re sad to see you go, but If you really need to, it is possible to completely uninstall Camel K from your cluster. The uninstalling procedure typically removes the operator but keeps Custom Resource Definition and any Integration which was previously running. They can be removed by the user by an additional cleaning operation.

## Uninstall via Helm

The Helm procedure takes care to delete only the operator Deployment:

```none
$ helm uninstall camel-k
```

Check instructions on [Camel K Helm](https://hub.helm.sh/charts/camel-k/camel-k) page to remove CRDs and any other installation resource.

## Uninstall via Operator Hub

In order to uninstall via OLM, you’ll need to identify and remove the Subscription custom resource related to Camel K. Check instructions on [uninstall an operator](https://olm.operatorframework.io/docs/tasks/uninstall-operator/) page from OLM.

## Uninstall via Kustomize

Uninstalling via Kustomize may require you to store the configuration you’ve used at install time and delete the applied resources. However this is something we discourage as it may remove also the application that are running and you may not want to delete (see generic cleaning for an alternative approach).

> **Warning**
> this operation may remove CRDs and any application that is still running.

```none
$ kustomize build 'overlays/my-configuration' | kubectl delete -f -
```

## Uninstall cleaning cluster resources

Another alternative is to delete the resources the operator is using in a controlled way by cleaning them one by one.

## Uninstall operator only (keeps CRDs and any running Integration)

In order to remove the operator and any configuration resource it uses you’ll need to perform the following cleaning operation. Here we’re assuming you have installed an operator in the namespace camel-k:

```none
$ kubectl delete deploy -l app=camel-k -n camel-k
$ kubectl delete configmap,secret,sa,rolebindings,clusterrolebindings,roles,clusterroles,integrationplatform -l app=camel-k -n camel-k
```

Notice that you need to perform two operation to let the Kubernetes finalizers running in the Deployment object to complete before removing any required additional resource (ie, the ServiceAccount holding such privileges).

> **Note**
> CRDs and Integration will be maintained alive and running.

## Resources created by the operator

During its lifecycle the operator can create ServiceAccounts, Roles and RoleBindings resources in the namespaces where it operates. They are typically labeled as "app=camel-k", so, if you want to uninstall the operator you can identify all those resources created in the namespaces with that label. You can identify those resources by running:

```none
kubectl get sa,role,rolebinding -l 'app=camel-k' --all-namespaces
```

You can clean these resources accordingly.

## Uninstall CRDs (and running Integration)

In order to remove the CRDs you need to execute:

```none
$ kubectl delete crd -l app=camel-k
```

> **Note**
> Integration will be garbage collected by the cluster and so any running application.

## Verify your cluster

To verify that all resources have been removed you can use the following command:

```none
kubectl get all,configmap,rolebindings,clusterrolebindings,secrets,sa,roles,clusterroles,crd -l 'app=camel-k'
NAME                                   READY   STATUS        RESTARTS   AGE
clusterrole.rbac.authorization.k8s.io/camel-k:edit   2020-05-28T20:31:39Z

NAME                                                                                  CREATED AT
customresourcedefinition.apiextensions.k8s.io/builds.camel.apache.org                 2020-05-28T20:31:39Z
customresourcedefinition.apiextensions.k8s.io/camelcatalogs.camel.apache.org          2020-05-28T20:31:39Z
customresourcedefinition.apiextensions.k8s.io/integrationkits.camel.apache.org        2020-05-28T20:31:39Z
customresourcedefinition.apiextensions.k8s.io/integrationplatforms.camel.apache.org   2020-05-28T20:31:39Z
customresourcedefinition.apiextensions.k8s.io/integrations.camel.apache.org           2020-05-28T20:31:39Z
customresourcedefinition.apiextensions.k8s.io/integrationprofiles.camel.apache.org    2020-05-28T20:31:39Z
```
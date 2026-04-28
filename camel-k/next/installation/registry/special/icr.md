# Configuring a Namespace on IBM Container Registry (ICR)

You can use a namespace of IBM Container Registry to host Camel K images.

In order to push images to `icr.io`, you need to provide valid credentials (secret) to Camel K.

## Creating a Namespace

The fast way to obtain a namespace on ICR is by [IBM Command line tool](https://cloud.ibm.com/docs/cli?topic=cli-install-ibmcloud-cli):

-   Install [IBM Command line tool](https://cloud.ibm.com/docs/cli?topic=cli-install-ibmcloud-cli):
    
    ```console
    $ ibmcloud plugin install container-registry -r 'IBM Cloud'
    ```
    
-   Log in to your IBM Cloud account:
    
    ```console
    $ ibmcloud login -a https://cloud.ibm.com
    ```
    
-   Ensure that you’re targeting the correct IBM Cloud Container Registry region:
    
    ```console
    $ ibmcloud cr region-set us-south
    ```
    
-   Choose a name for your namespace, and create that namespace:
    
    ```console
    $ ibmcloud cr namespace-add <my_namespace>
    ```
    

## Providing Registry Secret

Once you have a registry namespace, create a secret with the credentials in order for Camel K to access it.

Firstly, make sure to log in to ICR so that the local Docker config file has the credentials for it:

```console
$ ibmcloud cr login
```

Then create a secret with the Docker config file `$HOME/.docker/config.json` (or in case of Podman, `$XDG_RUNTIME_DIR/containers/auth.json`):

```console
$ kubectl create secret generic my-icr-secret --from-file=.dockerconfigjson=$HOME/.docker/config.json --type=kubernetes.io/dockerconfigjson
```

Now you can provide the secret to the Camel K operator via:

```none
REGISTRY_ADDRESS: <region>.icr.io
REGISTRY_ORGANIZATION: <my_namespace>
REGISTRY_SECRET: secret
```
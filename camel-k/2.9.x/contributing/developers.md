# Contributing to Camel K

We love contributions!

The [main project](https://github.com/apache/camel-k/) is written in [go](https://golang.org/) and contains some parts written in Java for the [integration runtime](https://github.com/apache/camel-k-runtime/). Camel K is built on top of Kubernetes through **Custom Resource Definitions**.

## How can I contribute?

There are many ways you can contribute to Camel K, not only software development, as well as with the rest of Camel community:

-   Contribute actively to development (see the section below)
    
-   Use it and report any feedback, improvement or bug you may find via [Github](https://github.com/apache/camel-k/), [mailing list](/community/mailing-list/) or [chat](https://camel.zulipchat.com).
    
-   Contribute by writing missing documentation or blog posts about the features around Camel K
    
-   [Tweet](https://twitter.com/ApacheCamel), like and socialize Camel K in your preferred social network
    
-   Enjoy the talks that the contributors submit in various conferences around the world.
    

## Requirements

In order to build the project, you need to comply with the following requirements:

-   **Go version 1.22+**: needed to compile and test the project. Refer to the [Go website](https://golang.org/) for the installation.
    
-   **GNU Make**: used to define composite build actions. This should be already installed or available as a package if you have a good OS ([https://www.gnu.org/software/make/](https://www.gnu.org/software/make/)).
    
-   **JDK version 17+**: the build requires JDK version 17 or above. This corresponds to the JDK version of the integration base image.
    
-   **Maven version 3.8+**: the build requires Maven 3.8 or above. This corresponds to the version defined in the `build/Dockerfile`.
    
-   **MinGW**: needed to compile the project on Windows. Refer to the [MinGW website](https://www.mingw-w64.org/) for the installation.
    
-   **Windows Subsystem for Linux (WSL)**: for running Linux binary executables natively on Windows. Refer to [WSL Website](https://docs.microsoft.com/en-us/windows/wsl/install) for installation. Alternatively, you can use [Cygwin](https://www.cygwin.com/) or [Git Bash](https://www.educative.io/edpresso/how-to-install-git-bash-in-windows).
    
-   **Docker**: the image build requires [Docker](https://www.docker.com/) and the [buildx plugin](https://github.com/docker/buildx).
    

> **Note**
> MacOS users will need to use **gnu-sed** to successfully run the Make build scripts (e.g. for generating the Camel K bundle). Please install gnu-sed on your machine (e.g. `brew install gnu-sed`) and set your PATH accordingly to use gnu-sed with: `export PATH="/usr/local/opt/gnu-sed/libexec/gnubin:$PATH"`

The Camel K Java runtime (camel-k-runtime) requires:

-   **Java 17**: needed for compilation
    
-   **Maven**: needed for building
    

## Running checks

Checks rely on `golangci-lint` being installed in version `1.55.2`, to install it look at the [Local Installation](https://golangci-lint.run/welcome/install/) instructions.

You can run checks via `make lint`.

## Checking Out the Sources

You can create a fork of [this project](https://github.com/apache/camel-k) from GitHub, then clone your fork with the `git` command line tool.

## Structure

This is a high-level overview of the project structure:

Table 1. Structure  
| Path | Content |
| --- | --- |
| [/build](https://github.com/apache/camel-k/tree/main/build) | Contains the Docker and Maven build configuration. |
| [/cmd](https://github.com/apache/camel-k/tree/main/cmd) | Contains the entry points (the **main** functions) for the **camel-k** binary (manager) and the **kamel** client tool. |
| [/docs](https://github.com/apache/camel-k/tree/main/docs) | Contains the documentation website based on [Antora](https://antora.org/). |
| [/e2e](https://github.com/apache/camel-k/tree/main/e2e) | Include integration tests to ensure that the software interacts correctly with Kubernetes and OpenShift. |
| [/examples](https://github.com/apache/camel-k/tree/main/examples) | Camel K examples were moved to separate git repository [camel-k-examples](https://github.com/apache/camel-k-examples). |
| [/helm/camel-k](https://github.com/apache/camel-k/tree/main/helm/camel-k) | Contains Helm chart for Camel K installation on any Kubernetes cluster. |
| [/install](https://github.com/apache/camel-k/tree/main/install) | Contains installation files. |
| [/java](https://github.com/apache/camel-k/tree/main/java) | Contains crds and Maven logging. |
| [/pkg](https://github.com/apache/camel-k/tree/main/pkg) | This is where the code resides. The code is divided in multiple subpackages. |
| [/proposals](https://github.com/apache/camel-k/tree/main/proposals) | Contains variety of proposals for Camel K. |
| [/release-utils/scripts](https://github.com/apache/camel-k/tree/main/release-utils/scripts) | Contains scripts for creating release. |
| [/script](https://github.com/apache/camel-k/tree/main/script) | Contains scripts used during make operations for building the project. |

## Building

To build the whole project you now need to run:

```none
make
```

This executes a full build of the Go code. If you need to build the components separately you can execute:

To build the `kamel` client tool only:

```none
make build-kamel
```

Currently the build is not entirely supported on Windows. If you’re building on a Windows system, here’s a temporary workaround:

1.  Copy the `script/Makefile` to the root of the project.
    
2.  Run `make -f script/Makefile`.
    
3.  If the above command fails, run `make build-kamel`.
    
4.  Rename the `kamel` binary in the root to `kamel.exe`.
    

After a successful build, if you’re connected to a Docker daemon, you can build the operator Docker image by running:

```none
make images
```

The above command produces a `camel-k` image with the name `apache/camel-k`. Sometimes you might need to produce `camel-k` images that need to be pushed to the custom repository e.g. `docker.io/myrepo/camel-k`, to do that you can pass a parameter `STAGING_IMAGE` to `make` as shown below:

```none
make STAGING_IMAGE='docker.io/myrepo/camel-k' images-push-staging
```

## Testing

Unit tests are executed automatically as part of the build. They use the standard go testing framework.

Integration tests (aimed at ensuring that the code integrates correctly with Kubernetes and OpenShift), need special care. Integration tests are all in the [/e2e](https://github.com/apache/camel-k/tree/main/e2e) dir.

For more detail on integration testing, refer to the following documentation:

-   [End To End local integration test](e2e.md)
    

## Running

If you want to install everything you have in your source code and see it running on Kubernetes, you need to run the following command:

### For Minikube

First remove any camel k operator you may have installed, otherwise it will conflict with the new one we will build and install.

-   Enable the `registry` minikube addon: `minikube addons enable registry`
    
-   Set the access to the internal minikube registry: `eval $(minikube docker-env)`
    
-   Run `make images` to build the project and install the image in the internal minikube registry
    
-   Install camel-k-operator: `make install-k8s-global`
    

### For Red Hat CodeReady Containers (CRC)

-   You need to have [Docker](https://docs.docker.com/get-docker/) installed and running (or connected to a Docker daemon)
    
-   You need to set up Docker daemon to [trust](https://docs.docker.com/registry/insecure/) CRC’s insecure Docker registry which is exposed by default through the route `default-route-openshift-image-registry.apps-crc.testing`. One way of doing that is to instruct the Docker daemon to trust the certificate:
    
    -   `oc extract secret/router-ca --keys=tls.crt -n openshift-ingress-operator`: to extract the certificate
        
    -   `sudo cp tls.crt /etc/docker/certs.d/default-route-openshift-image-registry.apps-crc.testing/ca.crt`: to copy the certificate for Docker daemon to trust
        
    -   `docker login -u kubeadmin -p $(oc whoami -t) default-route-openshift-image-registry.apps-crc.testing`: to test that the certificate is trusted
        
    
-   Run `make install-openshift-global`
    

The commands assume you have an already running CRC instance and logged in correctly.

### For remote Kubernetes/OpenShift clusters

If you have changed anything locally and want to apply the changes to a remote cluster, first push your `camel-k` image to a custom repository (see [Building](#building)) and run the following command (the image name `docker.io/myrepo/camel-k:2.4.0-SNAPSHOT` should be changed accordingly):

```none
CUSTOM_IMAGE=docker.io/myrepo/camel-k CUSTOM_VERSION=2.4.0-SNAPSHOT make bundle
make install-k8s-global
```

### Local Helm installation

If you want to test Helm installation

-   Build the Helm chart: `make release-helm`
    
-   Build the project and the image: `make images`
    
-   Set the internal registry: `export REGISTRY_ADDRESS=$(kubectl -n kube-system get service registry -o jsonpath='{.spec.clusterIP}')`
    
-   Install with Helm (look at the latest version produced by `make release-helm`)
    

```none
helm install camel-k-dev docs/charts/camel-k-2.4.0-SNAPSHOT.tgz --set platform.build.registry.address=${REGISTRY_ADDRESS} --set platform.build.registry.insecure=true --set operator.image=apache/camel-k:2.4.0-SNAPSHOT
```

-   To uninstall: `helm uninstall camel-k-dev`
    

### Examples

Camel K examples are located in separate git repository [camel-k-examples](https://github.com/apache/camel-k-examples/). You can clone it and run the examples locally.

### Use

Now you can play with Camel K:

```none
./kamel run <camel-k-examples>/01-basic/Basic.java
```

## Local development environment

If you need to develop and test your Camel K operator locally, you can follow the [local development procedure](local-development.md).

## Debugging and Running from IDE

Sometimes it’s useful to debug the code from the IDE when troubleshooting.

**Debugging the `kamel` binary**

It should be straightforward: just execute the [/cmd/kamel/main.go](https://github.com/apache/camel-k/tree/main/cmd/kamel/main.go) file from the IDE (e.g. Goland) in debug mode.

**Debugging the operator**

It is a bit more complex (but not so much).

You are going to run the operator code **outside** OpenShift in your IDE so, first of all, you need to **stop the operator running inside**:

```none
// use kubectl in plain Kubernetes
oc scale deployment/camel-k-operator --replicas 0
```

You can scale it back to 1 when you’re done, and you have updated the operator image.

You can set up the IDE (e.g. Goland) to execute the [/cmd/manager/main.go](https://github.com/apache/camel-k/blob/main/cmd/manager/main.go) file in debug mode with `operator` as the argument.

When configuring the IDE task, make sure to add all required environment variables in the **IDE task configuration screen**:

-   Set the `KUBERNETES_CONFIG` environment variable to point to your Kubernetes configuration file (usually `<homedir>/.kube/config`).
    
-   Set the `WATCH_NAMESPACE` environment variable to a Kubernetes namespace you have access to.
    
-   Set the `OPERATOR_NAME` environment variable to `camel-k`.
    

After you set up the IDE task, with Java 11+ to be used by default, you can run and debug the operator process.

## Building Metadata for Publishing the Operator in Operator Hub

Publishing to an operator hub requires creation and submission of metadata, required in a specific [format](https://github.com/operator-framework/operator-registry/#manifest-format). The [operator-sdk](https://sdk.operatorframework.io/docs/cli) provides tools to help with the creation of this metadata.

### `bundles`

The latest packaging format used for deploying the operator to an OLM registry. This generates a CSV and related metadata files in a directory named `bundle`. The directory contains a Dockerfile that allows for building the bundle into a single image. It is this image that is submitted to the OLM registry.

To generate the bundle for camel-k, use the following command:

```none
make bundle
```

The bundle directory is created at the root of the camel-k project filesystem.
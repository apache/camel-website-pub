# Full fledged Pipeline

If you’re running a build process over any external pipeline, you likely want to use that CICD technology in conjunction with Camel K. The features provided by our [Camel K Pipeline](pipeline.md) may be limited in such situation. For those requirements we suggest to integrate one of the many CICD technologies around. One that we want to suggest and for which we provide an opinionated approach is [Tekton CICD](https://tekton.dev/).

## Integrate with Tekton

Since Camel K version 2 we are supporting a [`kamel-run` Task](https://hub.tekton.dev/tekton/task/kamel-run) included in [Tekton Hub](https://hub.tekton.dev/). You can find the instructions and some example to show you how to adopt this technology together with Camel K. The prerequisite is to have Camel K and Tekton operators up and running. The brief guide requires certain previous familiarity with Tekton technology as well.

## Integrate with other pipelines

There are many CICD tools and we cannot provide support for every technology. However, Camel K gives you the possibility to run your own build with the CICD technology of choice and operate the Camel application accordingly. What you need to do is to let the CICD technology to provide an Integration custom resource with the container image built by the pipeline, ie: `kamel run test.yaml -t container.image=docker.io/my-org/my-image:xyz`.

The above is known as [**Self managed build** Integration](../running/self-managed.md).
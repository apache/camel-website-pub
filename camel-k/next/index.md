# Camel K Documentation Index

Index of Camel K documentation pages.

# Apache Camel K

Apache Camel K is a lightweight integration framework built from Apache Camel that runs natively on Kubernetes and is specifically designed for serverless and microservice architectures. The Camel K [Kubernetes Operator](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/) is in charge to transform a user provided Integration custom resource into a Camel application running on the cloud.

Users of Camel K can instantly run integration code written in any Camel DSL without worrying about the building and deployment of the application on the cloud.

## How It Works

Just write a _helloworld.yaml_ integration file with the following content:

```yaml
apiVersion: camel.apache.org/v1
kind: Integration
metadata:
  name: helloworld
spec:
  flows:
  - from:
      uri: timer:yaml
      steps:
      - setBody:
          simple: Hello Camel from ${routeId}
      - log: ${body}
```

You can then execute the following command:

```none
kubectl -f helloworld.yaml
```

The integration code will immediately run in the cloud. Continue reading the documentation to [install and get started with Camel K](installation/installation.md).
# Camel dependencies matrix

Camel K was originally equipped with a dedicated runtime known as Camel K Runtime. This is a lightweight layer on top of Camel Quarkus. However, you can directly run plain regular Camel Quarkus runtime applications as well. This will become the standard only from version 3.x onward in order to avoid breaking backward compatibility. In the while you’re strongly encouraged to use `plain-quarkus` Camel runtime configuration to ease any future 3.x migration.

> **Note**
> you can use any available Camel Quarkus runtime version. Alternatively you can also build any other Camel runtimes building from a Git hosted repository.

Camel dependencies matrix       
| Camel K Version | Last release | (Default) Camel K Runtime | Camel Quarkus | Camel | Quarkus | Branch |
| --- | --- | --- | --- | --- | --- | --- |
| [Next (Pre-release)](../../next/index.md) | 2.10.0 | 3.15.3 | 3.33.1 | 4.18.0 | 3.33.2 | [main](https://github.com/apache/camel-k) |
| [2.10.x](../../2.10.x/index.md) | 2.10.1 | 3.15.3 | 3.15.3 | 4.8.5 | 3.15.4 | [release-2.10.x](https://github.com/apache/camel-k/tree/release-2.10.x) |
| [2.9.x (LTS)](../index.md) | 2.9.2 | 3.15.3 | 3.15.3 | 4.8.5 | 3.15.4 | [release-2.9.x](https://github.com/apache/camel-k/tree/release-2.9.x) |

## Other APIs version matrix

Below you can find a list of the main dependencies and APIs used by Camel K and the related compatibility.

Kubernetes and other dependencies      
| Camel K Version | Kubernetes API | Operator Framework API | Knative API | Prometheus Operator | Kustomize version |
| --- | --- | --- | --- | --- | --- |
| [Next (Pre-release)](../../next/index.md) | 0.36.1 | 0.44.0 | 0.49.1 | 0.91.0 | 5.7.1 |
| [2.10.x](../../2.10.x/index.md) | 0.35.3 | 0.42.0 | 0.48.1 | 0.90.1 | 5.7.1 |
| [2.9.x (LTS)](../index.md) | 0.34.2 | 0.37.0 | 0.47.0 | 0.87.1 | 4.5.4 |
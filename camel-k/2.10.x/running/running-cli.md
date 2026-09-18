# Camel K CLI: kamel

In the previous section you have learnt [how to run an Integration custom resource](running.md). In this page you will learn a simple utility we release beside the operator, the `kamel` CLI.

Releases of the Camel K CLI are available on:

-   Apache Mirrors (official): [https://downloads.apache.org/camel/camel-k/](https://downloads.apache.org/camel/camel-k/)
    
-   Github Releases: [https://github.com/apache/camel-k/releases](https://github.com/apache/camel-k/releases)
    
-   Homebrew (Mac and Linux): [https://formulae.brew.sh/formula/kamel](https://formulae.brew.sh/formula/kamel)
    

So, pick yours, set in your operating system path and be ready to run some Camel K Integration. The `kamel` cli will reuse the same cluster configuration you have set for your cluster via `kubectl`, `oc` or any other tool. So, you can log in to the cluster via those CLI and then using `kamel` afterwards.

Let’s try some application by creating a file with the following content.

run-hello.yaml

```yaml
- from:
    uri: "timer:tick?period=3000"
    steps:
      - setBody:
          constant: "Hello world from Camel K"
      - to: "log:info"
```

> **Note**
> you can also use Camel JBang and initialize any Camel DSL via `camel init run-hello.yaml`

You can now run it on the cluster by executing:

```none
kamel run run-hello.yaml
```

## Monitoring the application status

Camel K integrations follow a lifecycle composed of several steps before getting into the `Running` state. You can check the status of all integrations by executing the following command:

```none
kamel get
```

## Log the standard output

Once the application is running you can check the content of the Pods log by executing:

```none
kamel logs hello
```

> **Note**
> if the above example failed, have a look at [how to troubleshoot a Camel K Integration](../troubleshooting/troubleshooting.md).

## Dry Run

The CLI is a simple yet powerful facility which will do a lot of heavy lift for you, transforming a Camel route into an Integration specification which will be watched and reconciled by the operator. However, sometimes you don’t want to apply the result of an execution on the cluster. You may want only to check how the route is transformed or you want to run the conversion and apply the result later.

**Dry Run** is the mode you can find on `kamel run`. If you have familiarity with Kubernetes, you will see we use the same approach used by `kubectl`, exposing a `-o` parameter which accepts either `yaml` or `json`. The presence of this feature will let you simplify any deployment strategy (including GitOps) as you can just get the result of the Integration which will be eventually executed by the Camel K Operator.

> **Note**
> we make use of `stderr` for many CLI warning and this is automatically redirected to `stdout` to show immediately the result of any error to the user. If you’re running any automation, make sure to redirect the `stderr` to any channel to avoid altering the result of the dry run, Ie `kamel run /tmp/Test.java -o yaml 2>/dev/null`.

As an example, take the option available on the `kamel run test.yaml -t prometheus.enabled=true -o yaml` command:

```yaml
apiVersion: camel.apache.org/v1
kind: Integration
metadata:
  annotations:
    camel.apache.org/operator.id: camel-k
  name: test
spec:
  flows:
  - from:
      parameters:
        period: "1000"
      steps:
      - setBody:
          constant: Hello Camel from yaml
      - log: ${body}
      uri: timer:yaml
  traits:
    prometheus:
      enabled: true
status: {}
```

This can be saved for future processing (ie, stored to a GIT repository and later deployed to a cluster via some GitOps deployment strategy). Consider that any **modeline** option will be translated accordingly.

## Camel K Modeline

Integration files can contain **modeline** hooks that allow to customize the way integrations are executed via command line. For example:

Hello.java

```java
// camel-k: dependency=mvn:org.my:application:1.0 (1)

import org.apache.camel.builder.RouteBuilder;

public class Hello extends RouteBuilder {
  @Override
  public void configure() throws Exception {
      from("timer:java?period=1000")
        .bean(org.my.BusinessLogic) (2)
        .log("${body}");
  }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Modeline import of Maven library</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Usage of a business logic class from the external library</td></tr></tbody></table>

When the integration code above is executed using the `kamel run` CLI command, the modeline options declared in the file are appended to the list of arguments that are passed to the command.

The `kamel` CLI will alert you, printing the full command in the shell:

```console
$ kamel run Hello.java
Modeline options have been loaded from source files
Full command: kamel run Hello.java --dependency mvn:org.my:application:1.0
```

Multiple options can be specified for an integration. For example, the following modeline options enables 3scale and limits the integration container memory:

ThreeScaleRest.java

```java
// camel-k: trait=3scale.enabled=true trait=container.limit-memory=256Mi (1)

import org.apache.camel.builder.RouteBuilder;

public class ThreeScaleRest extends RouteBuilder {

  @Override
  public void configure() throws Exception {
      rest().get("/")
        .route()
        .setBody().constant("Hello");
  }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Enables both the <em>container</em> and <em>3scale</em> traits, to expose the route via 3scale and limit the container memory.</td></tr></tbody></table>

All options that are available for the `kamel run` command can be specified as modeline options. The following is a partial list of useful options:

Table 1. Useful Modeline Options  
| Option | Description |
| --- | --- |
| `build-property` | Add a build time property or properties file (syntax: _\[my-key=my-value|file:/path/to/my-conf.properties\]_ |
| `dependency` | An external library that should be included, e.g. for Maven dependencies `dependency=mvn:org.my:app:1.0` |
| `env` | Set an environment variable in the integration container, e.g. `env=MY_VAR=my-value` |
| `label` | Add a label to the integration pod, e.g., `label=my.company=hello` |
| `name` | The integration name |
| `open-api` | Add an OpenAPI v2 spec (file path) |
| `profile` | Trait profile used for deployment |
| `property` | Add a runtime property or properties file (syntax: _\[my-key=my-value|file:/path/to/my-conf.properties\]_) |
| `resource` | Add a runtime resource from a Configmap or Secret (syntax: _\[configmap|secret\]:name\[/key\]\[@path\]_, where name represents the configmap/secret name, key optionally represents the configmap/secret key to be filtered and path represents the destination path) |
| `trait` | Configure a trait, e.g. `trait=service.enabled=false` |

## Run an Integration from the Internet

The `kamel` cli will allow you to run any application available on the Internet. Just run `kamel run [https://path/to/route.yaml](https://path/to/route.yaml)` and the CLI will take care to recover the route remotely. It is also possible to run Integrations from a GitHub repository or Gist with dedicated URL syntax:

Syntax

```none
kamel run github:$user/$repo/$path?branch=$branch
```

As example, running the following command

```none
kamel run github:apache/camel-k-examples/generic-examples/languages/Sample.java
```

Declaring the branch query param is not required and defaults to `master` if not explicit set.

Similar approach is used for the Gists:

Syntax

```none
kamel run https://gist.github.com/${user-id}/${gist-id}
kamel run gist:${gist-id}
```

Camel k will add any file that is part of the Gist as a source. As example, assuming there are two files listed as part of a Gist, beans.yaml and routes.yaml, then the following command:

```none
kamel run gist:${gist-id}
```

is equivalent to:

```none
kamel run \
    https://gist.githubusercontent.com/${user-id}/${gist-id}/raw/${...}/beans.yaml \
    https://gist.githubusercontent.com/${user-id}/${gist-id}/raw/${...}/routes.yaml
```

> **Note**
> GitHub applies rate limiting to its APIs and as Authenticated requests get a higher rate limit, the `kamel` honour the env var GITHUB\_TOKEN and if it is found, then it is used for GitHub authentication.
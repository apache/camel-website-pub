# First steps

This guide outlines various ways to create a new Camel Quarkus application.

## Prerequisites

-   A `git` client
    
-   An IDE
    
-   JDK 21+ with `JAVA_HOME` configured appropriately
    
-   Apache Maven 3.8.2+ (3.9.16 is recommended)
    
-   GraalVM with the `native-image` command installed and the `GRAALVM_HOME` environment variable set. See [Building a native executable](https://quarkus.io/guides/building-native-image) section of the Quarkus documentation.
    
-   Alternatively, a container runtime such as Docker or Podman can be used to build native executables without a local GraalVM installation. Add `-Dquarkus.native.container-build=true` to the native build command if you choose this option.
    

## code.quarkus.io

Projects can be generated at [code.quarkus.io](https://code.quarkus.io). All the Camel Quarkus extensions can be found under the 'Integration' category. Use the 'search' field to help with finding extensions that you are interested in.

Simply select the component extensions that you want to work with and click the 'Generate your application' button to download a basic skeleton project. There is also the option to push the project directly to GitHub.

When the project archive download has completed successfully, unzip and import into your favorite IDE.

## Maven plugin

Quarkus provides a Maven plugin that enables you to quickly bootstrap projects. For example, to create a project skeleton that includes the `timer` and `log` component extensions:

```shell
mvn io.quarkus:quarkus-maven-plugin:4.0.0:create \
    -DprojectGroupId=org.acme \
    -DprojectArtifactId=getting-started \
    -Dextensions=camel-quarkus-log,camel-quarkus-timer

cd getting-started
```

> **Note**
> Windows users should omit the `\` if using `cmd`. When using `Powershell`, wrap the `-D` parameters in double quotes.

[Gradle](https://gradle.org/) support is also available. See the [Quarkus Gradle](https://quarkus.io/guides/gradle-tooling) guide for more information.

## IDE plugins

Quarkus has plugins for most of the popular development IDEs. They provide Quarkus language support, code / config completion, project creation wizards and much more. The plugins are available at each respective IDE marketplace.

-   [Eclipse plugin](https://marketplace.eclipse.org/content/quarkus-tools)
    
-   [IntelliJ plugin](https://plugins.jetbrains.com/plugin/13234-quarkus-tools)
    
-   [VSCode plugin](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-quarkus)
    

Check the documentation of the given plugin to discover how to create projects in your preferred IDE.

### Camel content assist

The following plugins provide support for content assist when editing Camel routes and `application.properties`:

-   [VS Code Language support for Camel](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-apache-camel) - a part of the [Camel extension pack](https://marketplace.visualstudio.com/items?itemName=redhat.apache-camel-extension-pack)
    
-   [Eclipse Desktop Language Support for Camel](https://marketplace.eclipse.org/content/language-support-apache-camel)
    
-   [Apache Camel IDEA plugin](https://plugins.jetbrains.com/plugin/9371-apache-camel) (not always up to date)
    
-   Users of other [IDEs supporting Language Server Protocol](https://microsoft.github.io/language-server-protocol/implementors/tools/) may choose to install and configure [Camel Language Server](https://github.com/camel-tooling/camel-language-server) manually
    

## Example projects

Camel Quarkus provides a GitHub repository containing a set of [example projects](examples.md).

[https://github.com/apache/camel-quarkus-examples](https://github.com/apache/camel-quarkus-examples)

The main branch is always aligned with the latest Camel Quarkus release.

### Step by step with the `rest-json` example

1.  Clone the Camel Quarkus examples repository:
    
    ```shell
    git clone https://github.com/apache/camel-quarkus-examples.git
    ```
    
2.  Copy the `rest-json` example out of the source tree:
    
    ```shell
    cp -r camel-quarkus-examples/rest-json .
    cd rest-json
    ```
    
3.  Open the `pom.xml` file in your IDE. Change the project `groupId`, `artifactId` & `version` as necessary.
    

#### Explore the application code

The application has three compile dependencies:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jackson</artifactId>
</dependency>
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-rest</artifactId>
</dependency>
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-direct</artifactId>
</dependency>
```

They are managed within the `io.quarkus.platform:quarkus-camel-bom` that is imported in `<dependencyManagement>`.

> **Note**
> More about [BOMs](dependency-management.md).

There are only three classes in the application: `Routes` defines the Camel routes, whereas `Fruit` and `Legume` are entities.

The application is configured by properties defined within `src/main/resources/application.properties`. E.g. the `camel.context.name` is set there.

#### Development mode

```shell
mvn clean compile quarkus:dev
```

This command compiles the project, starts your application and lets the Quarkus tooling watch for changes in your workspace. Any modifications in your project will automatically take effect in the running application.

Check the application in the browser, e.g. [http://localhost:8080/fruits](http://localhost:8080/fruits) for the `rest-json` example

Then change something in the code and see the changes applied by refreshing the browser.

Please refer to [Quarkus documentation](https://quarkus.io/guides/maven-tooling#dev-mode) for more details about the development mode.

#### Testing

There are two test classes in our example: `RestJsonTest` is for the JVM mode while `RestJsonIT` is there for the native mode.

The JVM mode tests are run by `maven-surefire-plugin` in the `test` Maven phase:

```shell
mvn clean test
```

The native mode tests are verified by `maven-failsafe-plugin` in the `verify` phase. Pass the `native` property to activate the profile that runs them:

```shell
mvn clean verify -Dnative
```

#### Package and run the application

##### JVM mode

`mvn package` prepares a thin `jar` for running on a stock JVM:

```shell
mvn clean package
```

The runnable `quarkus-run.jar` is created in the `target/quarkus-app` directory. You can run it as follows:

```shell
java -jar target/quarkus-app/quarkus-run.jar
```

The thin `jar` contains just the application code. To run it, the dependencies in `target/quarkus-app/lib` are required too.

##### Native mode

To prepare a native executable using GraalVM, run the following command:

```shell
mvn clean package -Dnative
```

The native executable is created in the `target` directory. Its name ends with `-runner`, it has no `.jar` extension, and it has the `x` (executable) permission set. Thus, it can be run directly:

```shell
./target/*-runner
```

Compare how quickly it starts and how little memory it consumes with the JVM mode application.

> **Tip**
> [Quarkus Native executable guide](https://quarkus.io/guides/building-native-image) contains more details including [steps for creating a container image](https://quarkus.io/guides/building-native-image#creating-a-container).

## What’s next?

We recommend to continue with [Dependency management](dependency-management.md).
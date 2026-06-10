# Getting Started

You can get started with Apache Camel in a variety of ways, such as:

-   Using online Project generators
    
-   Using the Camel CLI (command line)
    

And some more alternative methods:

-   Adding Camel to an existing project
    
-   Using IDE tooling wizards
    
-   Using UI tooling with visual designers
    
-   Using Maven Archetypes
    
-   Cloning an existing example to modify
    

## Using online Project generators

You can use [Spring Boot Initializer](https://start.spring.io/) which is the Spring Boot generator that also has Camel support. However, this generator does not allow users to have fine-grained control over which components, data formats, kamelets etc. they can use.

And there is [Code with Quarkus](https://code.quarkus.io/), the Quarkus generator, which has great support with Camel.

## Getting Started from command line (CLI)

The Camel CLI can either be installed and used together with JBang (step 1a), or as a pure standalone Camel installation (step 1b).

### Installing and using Camel CLI

Camel uses [JBang](https://www.jbang.dev/) for the Camel CLI. You can easily get up and running in a few steps.

**Step 1a**

First install [JBang](https://www.jbang.dev/download/) according to your platform.

Once JBang is installed, you should be able to make sure it works by calling the version command:

```bash
$ jbang version
0.138.0
```

After this then install Camel into JBang as follows:

```bash
$ jbang app install camel@apache/camel
```

Then you can check that Camel is installed and working by executing:

```bash
$ camel version
JBang version: 0.138.0
Camel CLI version: 4.18.0
```

### Installing and using Camel standalone CLI

**Step 1b**

Download the [Camel Launcher](camel-jbang-launcher.md) .zip distribution for a desired Camel release.

For example to download Camel 4.18.2 from [Maven Central](https://repo1.maven.org/maven2/org/apache/camel/camel-launcher/4.18.2/), then click and download the _.bin.zip_ file, and then unzip the file to a work folder:

```bash
$ unzip camel-launcher-4.18.2-bin.zip
$ cd camel-launcher-4.18.2
```

You can then execute the provided scripts from the bin folder:

```bash
$ bin/camel.sh version
JBang version: 0.138.0
Camel CLI version: 4.18.2
```

> **Tip**
> You can also unzip the camel-launcher to a shared folder, and add its bin to the `$PATH` environment so you can execute `camel` from anywhere in your terminal.

### Using Camel CLI

**Step 2**

Create your first Camel integration

```bash
$ camel init hello.yaml
```

> **Tip**
> You can also use Java or XML instead of YAML. For example `camel init hi.java`.

**Step 3**

Run the Camel integration

```bash
$ camel run hello.yaml
```

Bang the Camel integration is now running. You can use `ctrl` + `c` to stop the integration.

**Step 4**

Camel makes it easy to change your code on the fly. You can run in live coding mode, as shown:

```bash
$ camel run hello.yaml --dev
```

While in live coding mode, whenever you save changes to `hello.yaml`, Camel will automatically load the updated version.

**Step 5**

Make sure to check out the [Camel CLI](camel-jbang.md) documentation, for more details on the powers of the Camel CLI. You will also find information how you can _export_ what you have built with the Camel CLI into a vanilla Camel Spring Boot or Camel Quarkus project.

> **Tip**
> See the `camel wrapper` command which can be used to install and pin Camel CLI to a given version which is local for a given project/directory (similar to how Maven Wrapper works).

## Alternative ways of getting started with Camel

### Adding Camel to an existing project

You can add Camel to any Java project, such as adding the necessary Camel dependencies to the project build files (Maven or Gradle).

### Using IDE tooling wizards

Some IDEs have wizards for creating new projects, of which, some have support for Apache Camel via Spring Boot Initializer or Code with Quarkus.

### Using UI tooling with visual designers

There are a number of UI designers for Apache Camel that can help you get familiar with Camel, and provide clarification on what you can do with Camel.

Among others the following are open source and provide support for official Apache Camel distributions:

-   [Apache Camel Karavan](https://github.com/apache/camel-karavan) - Has an [online UI designer](https://karavan.space/) that runs in a web browser.
    
-   [Kaoto](https://kaoto.io/) - Has also an [online UI designer](https://kaotoio.github.io/kaoto/) that runs in a web browser.
    

Both Camel Karavan and Kaoto can be installed as Visual Studio plugins directly in this IDE.

### Using Maven Archetypes

Apache Camel comes with a set of [Camel Maven Archetypes](camel-maven-archetypes.md), you can use to create a new Camel project.

### Cloning an existing example to modify

There are tons of Camel examples hosted on GitHub that you can clone and modify, such as [Camel Spring Boot examples](https://github.com/apache/camel-spring-boot-examples).

## See Also

To get familiar and learn the basic concepts of Apache Camel, then its recommend to check out [Architecture](architecture.md) and follow the links from that page.
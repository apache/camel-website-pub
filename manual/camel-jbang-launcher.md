# Camel CLI Launcher

**Available as of Camel 4.13**

A self-contained executable JAR for running Camel CLI without JBang. Uses Spring Boot’s nested JAR loader for fast startup and isolated classpath.

Download from [Maven Central](https://repo1.maven.org/maven2/org/apache/camel/camel-launcher/).

## Using the fat-jar directly

```bash
java -jar camel-launcher-<version>.jar version
java -jar camel-launcher-<version>.jar run hello.java
```

## Using the distribution (recommended)

Extract the distribution archive:

```bash
unzip camel-launcher-<version>-bin.zip
# or
tar -xzf camel-launcher-<version>-bin.tar.gz
```

And then use the provided scripts:

```bash
# On Unix/Linux
./bin/camel.sh [command] [options]

# On Windows
bin\camel.bat [command] [options]
```

## Benefits

-   No JBang installation required
    
-   Faster startup (no dependency resolution, on-demand class loading)
    
-   Lower memory usage (only loads classes actually used)
    
-   No classpath conflicts (dependencies kept as separate nested JARs)
    
-   Pinned Camel version — upgrade by downloading a newer launcher
    

## Limitations

The `--camel-version` option is not supported — it requires JBang to dynamically download a different version. Use a different launcher JAR version instead, or install via JBang: `jbang app install camel@apache/camel`.

## More Information

See [Installing the Camel CLI Launcher](camel-jbang-launcher-install.md) for the website installer scripts, `camel self-update`, and \`camel doctor’s multi-install detection, and the general [Camel CLI](camel-jbang.md) documentation.
# Debug

**Since Camel 3.15**

The camel-debug enables Camel debugger for 3rd party tooling. This makes it easier to perform debugging in IDEs such as IDEA, Eclipse, VSCode

> **Important**
> The camel-debug is only for development purposes, it should **not** be used for production.

## Auto-detection from classpath

To use this implementation all you need to do is to add the `camel-debug` dependency to the classpath, and Camel should auto-detect this on startup and log as follows:

```text
Detected: camel-debug JAR (Enabling Camel Debugging)
```

## JMX remote connection

To make it possible for 3rd party tooling to connect to the running Camel application, and to perform debugging actions, then Camel will expose a JMX RMI connector port, that the tools can use to connect via that allows JMX remote management.

The service URL to connect is:

```text
service:jmx:rmi:///jndi/rmi://localhost:1099/jmxrmi/camel
```
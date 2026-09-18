# Debug

**Since Camel 3.15**

The camel-debug enables Camel debugger for third party tooling. This makes it easier to perform debugging in IDEs such as IDEA, Eclipse, VSCode

> **Important**
> The camel-debug is only for development purposes, it should **not** be used for production.

## Auto-detection from classpath

To use this implementation all you need to do is to add the `camel-debug` dependency to the classpath, and Camel should auto-detect this on startup and log as follows:

```text
Detected: camel-debug JAR (Enabling Camel Debugging)
```

## JMX remote connection

Camel will expose a JMX RMI connector port that the tools can use to connect via that allows JMX remote management. This is necessary to make it possible for third party tooling to connect to the running Camel application, and to perform debugging actions.

The service URL to connect is:

```text
service:jmx:rmi:///jndi/rmi://localhost:1099/jmxrmi/camel
```
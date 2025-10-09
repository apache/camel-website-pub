# Reactive Executor Tomcat

**Since Camel 3.17**

The `camel-reactive-executor-tomcat` is intended for users of Apache Tomcat, to let Camel applications shutdown cleanly when being un-deployed in Apache Tomcat.

## Auto-detection from classpath

To use this implementation all you need to do is to add the `camel-reactive-executor-tomcat` dependency to the classpath, and Camel should auto-detect this on startup and log as follows:

```text
Using ReactiveExecutor: camel-reactive-executor-tomcat
```
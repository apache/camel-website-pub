# Reactive Executor Tomcat

> **Warning**
> **Deprecated:** This reactive-executor-tomcat is deprecated and may be removed in a future release.

**Since Camel 3.17**

**Deprecated since Camel 4.22**

> **Warning**
> This component is deprecated and will be removed in a future release. Use the default `ReactiveExecutor` (built into `camel-core`) instead.

The `camel-reactive-executor-tomcat` was intended for users of Apache Tomcat, to let Camel applications shutdown cleanly when being un-deployed in Apache Tomcat.

The cross-thread `ThreadLocal` cleanup that distinguished this component from the default `ReactiveExecutor` relied on reflective access to the private `Thread.threadLocals` field. This approach is denied by the JDK module system since JDK 17 and is incompatible with virtual threads. Without that cleanup, this executor is functionally identical to the default.

To migrate, simply remove the `camel-reactive-executor-tomcat` dependency from your project. Camel will automatically use the built-in `DefaultReactiveExecutor`.

## Auto-detection from classpath

To use this implementation all you need to do is to add the `camel-reactive-executor-tomcat` dependency to the classpath, and Camel should auto-detect this on startup and log as follows:

```text
Using ReactiveExecutor: camel-reactive-executor-tomcat
```
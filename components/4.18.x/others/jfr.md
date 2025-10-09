# JFR

**Since Camel 3.8**

The Camel Java Flight Recorder (JFR) component is used for integrating Camel with Java Flight Recorder (JFR).

This allows you to monitor and troubleshoot your Camel applications with JFR.

The camel-jfr component emits lifecycle events for startup to JFR. This can, for example, be used to pinpoint which Camel routes may be slow to startup.

See the _startupRecorder_ options from [Camel Main](main.md)

## Example

To enable you just need to add `camel-jfr` to the classpath, and enable JFR recording.

JFR recordings can be started at:

-   When running the JVM using JVM arguments
    
-   When starting Camel by setting `camel.main.startup-recorder-recording=true`.
    

See the `flight-recorder` from the Camel Examples.

## Spring Boot Auto-Configuration

When using jfr with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jfr-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component has no Spring Boot auto configuration options.
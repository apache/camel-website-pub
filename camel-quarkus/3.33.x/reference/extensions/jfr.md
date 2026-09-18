# Jfr

JVM since1.7.0 Native since2.6.0

Diagnose Camel applications with Java Flight Recorder

## What’s inside

-   [JFR](../../../../components/4.18.x/others/jfr.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jfr)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jfr</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Starting flight recording

To enable Java Flight Recorder to start a recording and automatically dump the recording to disk after Camel startup is complete, use the following configuration in `application.properties`.

```properties
quarkus.camel.jfr.startup-recorder-recording=true
```

Alternatively you can pass some Java options to the runnable application JAR or the native executable to enable flight recording at application startup.

In JVM mode the application runnable JAR can be executed as follows.

```shell
java -XX:+FlightRecorder -XX:StartFlightRecording=filename=recording.jfr -jar quarkus-run.jar
```

In native mode, the native executable can be executed as follows.

```shell
./my-application-runner -XX:+FlightRecorder -XX:StartFlightRecording=filename=recording.jfr
```

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.jfr.startup-recorder-dir](#quarkus-camel-jfr-startup-recorder-dir)`
Directory to store the recording. By default, the current directory will be used. Use false to turn off saving the recording to disk.

 | `string` |  |
| `[quarkus.camel.jfr.startup-recorder-duration](#quarkus-camel-jfr-startup-recorder-duration)`

How long time to run the startup recorder. Use 0 (default) to keep the recorder running until the JVM is exited. Use -1 to stop the recorder right after Camel has been started (to only focus on potential Camel startup performance bottlenecks) Use a positive value to keep recording for N seconds. When the recorder is stopped then the recording is auto saved to disk (note: save to disk can be disabled by setting startupRecorderDir to false).

 | `long` |  |
| `[quarkus.camel.jfr.startup-recorder-max-depth](#quarkus-camel-jfr-startup-recorder-max-depth)`

To filter our sub steps at a maximum depth. Use -1 for no maximum. Use 0 for no sub steps. Use 1 for max 1 sub step, and so forth. The default is -1.

 | `int` |  |
| `[quarkus.camel.jfr.startup-recorder-profile](#quarkus-camel-jfr-startup-recorder-profile)`

To use a specific Java Flight Recorder profile configuration, such as default or profile. The default is default.

 | `string` |  |
| `[quarkus.camel.jfr.startup-recorder-recording](#quarkus-camel-jfr-startup-recorder-recording)`

To enable Java Flight Recorder to start a recording and automatic dump the recording to disk after startup is complete. This requires that camel-jfr is on the classpath. The default is false.

 | `boolean` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.
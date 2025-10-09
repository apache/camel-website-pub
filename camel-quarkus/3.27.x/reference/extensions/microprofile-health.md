# MicroProfile Health

JVM since0.3.0 Native since0.3.0

Expose Camel health checks via MicroProfile Health

## What’s inside

-   [Microprofile Health](../../../../components/4.14.x/others/microprofile-health.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-microprofile-health)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-microprofile-health</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

You can register health checks for your applications with the [Camel health check API](../../../../manual/health-check.md).

By default, classes extending `AbstractHealthCheck` are registered as both liveness and readiness checks. You can override the `isReadiness` method to control this behaviour.

Any checks provided by your application are automatically discovered and bound to the Camel registry. They will be available via the Quarkus health endpoints `/q/health/live` and `/q/health/ready`.

You can also provide custom `HealthCheckRepository` implementations and these are also automatically discovered and bound to the Camel registry for you.

Refer to the [Quarkus health guide](https://quarkus.io/guides/health-guide) for further information.

### Provided health checks

Some checks are automatically registered for your application.

#### Camel Context Health

Inspects the Camel Context status and causes the health check status to be `DOWN` if the status is anything other than 'Started'.

#### Camel Route Health

Inspects the status of each route and causes the health check status to be `DOWN` if any route status is not 'Started'.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.health.enabled](#quarkus-camel-health-enabled)`
Set whether to enable Camel health checks

 | `boolean` | `true` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.
# CronScheduledRoutePolicy

`CronScheduledRoutePolicy` is a [ScheduledRoutePolicy](scheduledroutepolicy.md) that facilitates route activation, deactivation, suspension and resumption of routes based on a [Quartz](../components/4.22.x/quartz-component.md) cron trigger.

> **Tip**
> Relationship to the Quartz component
>
> All Scheduled route policies share the scheduler created by the [Quartz](../components/4.22.x/quartz-component.md) component. In this way, scheduler, jobs and triggers can be managed in a common and consistent way.

## Using cron scheduled route policy

To use a `CronScheduledRoutePolicy` it is necessary to instantiate an object of the type `org.apache.camel.routepolicy.quartz.CronScheduledRoutePolicy`.

To perform a route operation at a given time, the following information must be provided.

### Starting a route

   
| Parameter Name | Type | Default Value | Description |
| --- | --- | --- | --- |
| routeStartTime | String |  | the initial scheduled date and time as a Cron Expression for route start |

### Stopping a route

   
| Parameter Name | Type | Default Value | Description |
| --- | --- | --- | --- |
| routeStopTime | String |  | the initial scheduled date and time as a Cron Expression for route stop |
| routeStopGracePeriod | int | 10000 | the time period to wait before initiating graceful route stop |
| timeUnit | `java.util.concurrent.TimeUnit` | MILLISECONDS | the time unit for the grace period |

### Suspending a route

   
| Parameter Name | Type | Default Value | Description |
| --- | --- | --- | --- |
| routeSuspendTime | String |  | the initial scheduled date and time as a Cron Expression for route suspension |

### Resuming a route

   
| Parameter Name | Type | Default Value | Description |
| --- | --- | --- | --- |
| routeResumeTime | String |  | the initial scheduled date and time as a Cron Expression for route resumption |

### Cron expression format

The cron expressions use the Quartz format, which starts with seconds: `seconds minutes hours day-of-month month day-of-week [year]`. One of `day-of-month` and `day-of-week` must be `?`. For example, `0 0 8 ? * MON-FRI` is at 8:00 from Monday to Friday. A Unix cron expression with five fields, such as `* * * * *`, is invalid, and Camel fails to start. See [Using Cron Triggers](../components/4.22.x/quartz-component.html#_using_cron_triggers) in the Quartz component.

## Configuring the route policy

Once the `org.apache.camel.routepolicy.quartz.CronScheduledRoutePolicy` is created it can be wired into the Camel route as follows. In this example, the route that consumes from a JMS queue is started at 8:00 and stopped at 18:00 every day:

-   Java
    
-   Spring XML
    
-   YAML
    

```java
CronScheduledRoutePolicy policy = new CronScheduledRoutePolicy();
policy.setRouteStartTime("0 0 8 * * ?");
policy.setRouteStopTime("0 0 18 * * ?");

from("jms:queue:orders")
    .routeId("orders").routePolicy(policy).noAutoStartup()
    .to("log:orders");
```

```xml
<bean id="policy" class="org.apache.camel.routepolicy.quartz.CronScheduledRoutePolicy">
    <property name="routeStartTime" value="0 0 8 * * ?"/>
    <property name="routeStopTime" value="0 0 18 * * ?"/>
</bean>

<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route id="orders" routePolicyRef="policy" autoStartup="false">
        <from uri="jms:queue:orders"/>
        <to uri="log:orders"/>
    </route>
</camelContext>
```

```yaml
- beans:
  - name: policy
    type: org.apache.camel.routepolicy.quartz.CronScheduledRoutePolicy
    properties:
      routeStartTime: "0 0 8 * * ?"
      routeStopTime: "0 0 18 * * ?"
- route:
    id: orders
    autoStartup: "false"
    routePolicyRef: policy
    from:
      uri: jms:queue:orders
      steps:
        - to:
            uri: log:orders
```

> **Important**
> Notice how the route to be scheduled **MUST** be configured to not [auto-startup](configuring-route-startup-ordering-and-autostartup.md), to let the route scheduler take control of starting and stopping the route accordingly.

> **Note**
> A route policy only starts, stops, suspends or resumes the route. It never creates or sends a message: while the route is started, its consumer (such as JMS or file) takes the messages. To run a task at a given time, use the [Quartz](../components/4.22.x/quartz-component.md), [Timer](../components/4.22.x/timer-component.md) or [Scheduler](../components/4.22.x/scheduler-component.md) component instead.

### Dependency

Maven users will need to add a camel-quartz dependency to their `pom.xml` to avail this capability.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-quartz</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```
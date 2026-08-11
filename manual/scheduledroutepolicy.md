# ScheduledRoutePolicy

A scheduled [Route Policy](route-policy.md) `org.apache.camel.routepolicy.quartz.ScheduledRoutePolicy` is an extensible abstract policy that is used to provide Camel routes scheduling capabilities at runtime.

Scheduling of routes typically involves the following capabilities:

-   _Route activation_ - Starting a route a given start time if the route is in a stopped state awaiting activation.
    
-   _Route de-activation_ - Shutting down an otherwise active and started route at a given time.
    
-   _Route suspension_ - Simply de-activating the route consumer endpoint URI declared on the `from(…​)` section of the route from listening on a given port. The route is still considered as started, however, clients will not be able to send requests along the route.
    
-   _Route resumption_ - Resuming the listener on a formerly suspended route consumer endpoint URI. This route is ready to accept requests following route resumption and client requests will be accepted by the route consumer to be forwarded along the route.
    

Camel offers two such concrete policies that offer scheduled route policy support in the `camel-quartz` component:

-   [SimpleScheduledRoutePolicy](simplescheduledroutepolicy.md) - An ability to offer route scheduling services using a Simple [Quartz](../components/4.22.x/quartz-component.md) trigger.
    
-   [CronScheduledRoutePolicy](cronscheduledroutepolicy.md) - An ability to offer route scheduling services using a Cron based [Quartz](../components/4.22.x/quartz-component.md) trigger.
    

## More Information

See [Route Policy](route-policy.md) and [Quartz](../components/4.22.x/quartz-component.md) component.
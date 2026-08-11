# Failover Load Balancer

This EIP allows using fail-over (in case of failures, the exchange will be tried on the next endpoint) with the [Load Balancer](loadBalance-eip.md) EIP.

## Options

The Failover Load Balancer eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **exception** | A list of class names for specific exceptions to monitor. If no exceptions are configured then all exceptions are monitored. |  | List |
| **roundRobin** | Whether to use round robin mode. If enabled, the load balancer keeps state and continues with the next endpoint in a round robin fashion. If not, it always starts from the first endpoint for every message. | false | Boolean |
| **sticky** | Whether to use sticky mode. If enabled, the load balancer keeps state and continues with the last known good endpoint. | false | Boolean |
| **maximumFailoverAttempts** | A value to indicate after X failover attempts we should exhaust (give up). Use -1 to indicate never give up and continuously try to failover. Use 0 to never failover. Use e.g. 3 to failover at most 3 times before giving up. | \-1 | String |
| **inheritErrorHandler** | Whether to inherit the error handler. If turned off, the load balancer will fail over immediately on an error instead of waiting for Camel error handler to exhaust retries. | true | Boolean |

## Exchange properties

The Failover Load Balancer eip has no exchange properties.

## Example

In the example below, calling the three http services is done with the load balancer:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .loadBalance().failover()
        .to("http:service1")
        .to("http:service2")
        .to("http:service3")
    .end();
```

```xml
<route>
    <from uri="direct:start"/>
    <loadBalance>
        <failoverLoadBalancer/>
        <to uri="http:service1"/>
        <to uri="http:service2"/>
        <to uri="http:service3"/>
    </loadBalance>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - loadBalance:
            steps:
              - failoverLoadBalancer: {}
              - to:
                  uri: http:service1
              - to:
                  uri: http:service2
              - to:
                  uri: http:service3
```

In the default mode, the fail-over load balancer will always start with the first processor (i.e., "http:service1"). And in case this fails, then try the next, until either it succeeded or all of them failed. If all failed, then Camel will throw the caused exception which means the Exchange is failed.

### Using round-robin mode

You can use the `roundRobin` mode to start again from the beginning, which then will keep trying until one succeed. To prevent endless retries, then it’s recommended to set a maximum fail-over value.

-   Java
    
-   XML
    
-   YAML
    

Setting this in Java DSL is not _pretty_ as there are three parameters:

```java
from("direct:start")
    .loadBalance().failover(10, false, true)
        .to("http:service1")
        .to("http:service2")
        .to("http:service3")
    .end();
```

Where `10` is the maximum fail-over attempts, And `false` is a special feature related to inheriting error handler. The last parameter `true` is to use round-robin mode.

In XML and YAML DSL it is easier.

```xml
<route>
    <from uri="direct:start"/>
    <loadBalance>
        <failoverLoadBalancer inheritErrorHandler="false" roundRobin="true" maximumFailoverAttempts="10"/>
        <to uri="http:service1"/>
        <to uri="http:service2"/>
        <to uri="http:service3"/>
    </loadBalance>
</route>
```

In XML and YAML DSL it is easier.

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - loadBalance:
            steps:
              - failoverLoadBalancer:
                  inheritErrorHandler: "false"
                  maximumFailoverAttempts: 10
                  roundRobin: "true"
              - to:
                  uri: http:service1
              - to:
                  uri: http:service2
              - to:
                  uri: http:service3
```

### Using sticky mode

The sticky mode is used for remember the last known good endpoint, so the next exchange will start from there, instead from the beginning.

For example, support that http:service1 is down, and that service2 is up. With sticky mode enabled, then Camel will keep starting from service2 until it fails, and then try service3.

If sticky mode is not enabled (it’s disabled by default), then Camel will always start from the beginning, which means calling service1.

-   Java
    
-   XML
    
-   YAML
    

Setting sticky mode in Java DSL is not _pretty_ as there are four parameters.

```java
from("direct:start")
    .loadBalance().failover(10, false, true, true)
        .to("http:service1")
        .to("http:service2")
        .to("http:service3")
    .end();
```

> **Note**
> The last `true` argument is to enable sticky mode.

In XML and YAML DSL it is easier.

```xml
<route>
    <from uri="direct:start"/>
    <loadBalance>
        <failoverLoadBalancer inheritErrorHandler="false" roundRobin="true" maximumFailoverAttempts="10" stickyMode="true"/>
        <to uri="http:service1"/>
        <to uri="http:service2"/>
        <to uri="http:service3"/>
    </loadBalance>
</route>
```

In XML and YAML DSL it is easier.

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - loadBalance:
            steps:
              - failoverLoadBalancer:
                  inheritErrorHandler: "false"
                  sticky: "true"
                  maximumFailoverAttempts: 10
                  roundRobin: "true"
              - to:
                  uri: http:service1
              - to:
                  uri: http:service2
              - to:
                  uri: http:service3
```

### Fail-over on specific exceptions

The fail-over load balancer can be configured to only apply for a specific set of exceptions. Suppose you only want to fail-over in case of `java.io.Exception` or `HttpOperationFailedException` then you can do:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .loadBalance().failover(IOException.class, HttpOperationFailedException.class)
        .to("http:service1")
        .to("http:service2")
        .to("http:service3")
    .end();
```

```xml
<route>
    <from uri="direct:start"/>
    <loadBalance>
        <failoverLoadBalancer>
            <exception>java.io.IOException</exception>
            <exception>org.apache.camel.http.base.HttpOperationFailedException</exception>
        </failoverLoadBalancer>
        <to uri="http:service1"/>
        <to uri="http:service2"/>
        <to uri="http:service3"/>
    </loadBalance>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - loadBalance:
            steps:
              - failoverLoadBalancer:
                  exception:
                    - java.io.IOException
                    - org.apache.camel.http.base.HttpOperationFailedException
              - to:
                  uri: http:service1
              - to:
                  uri: http:service2
              - to:
                  uri: http:service3
```
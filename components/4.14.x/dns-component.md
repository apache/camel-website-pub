# DNS

**Since Camel 2.7**

**Only producer is supported**

This is an additional component for Camel to run DNS queries, using DNSJava. The component is a thin layer on top of [DNSJava](http://www.xbill.org/dnsjava/). The component offers the following operations:

-   `ip`: to resolve a domain by its ip
    
-   `lookup`: to lookup information about the domain
    
-   `dig`: to run DNS queries
    

> **Note**
> **Requires SUN JVM**
>
> The DNSJava library requires running on the SUN JVM.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-dns</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

The URI scheme for a DNS component is as follows

dns://operation\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The DNS component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The DNS endpoint is configured using URI syntax:

dns:dnsType

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dnsType** (producer) | 
**Required** The type of the lookup.

Enum values:

-   dig
    
-   ip
    
-   lookup
    
-   wikipedia
    





 |  | DnsType |

### Query Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The DNS component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dns.class** (lookup dig) Constant: [`DNS_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-dns/latest/org/apache/camel/component/dns/DnsConstants.html#DNS_CLASS) | The DNS class of the lookup. Should match the values of org.xbill.dns.DClass. Optional. |  | String |
| **dns.name** (lookup) Constant: [`DNS_NAME`](https://javadoc.io/doc/org.apache.camel/camel-dns/latest/org/apache/camel/component/dns/DnsConstants.html#DNS_NAME) | **Required** The name to lookup. |  | String |
| **dns.domain** (ip) Constant: [`DNS_DOMAIN`](https://javadoc.io/doc/org.apache.camel/camel-dns/latest/org/apache/camel/component/dns/DnsConstants.html#DNS_DOMAIN) | **Required** The domain name. |  | String |
| **dns.server** (dig) Constant: [`DNS_SERVER`](https://javadoc.io/doc/org.apache.camel/camel-dns/latest/org/apache/camel/component/dns/DnsConstants.html#DNS_SERVER) | The server in particular for the query. If none is given, the default one specified by the OS will be used. Optional. |  | String |
| **dns.type** (lookup dig) Constant: [`DNS_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-dns/latest/org/apache/camel/component/dns/DnsConstants.html#DNS_TYPE) | The type of the lookup. Should match the values of org.xbill.dns.Type. Optional. |  | String |
| **term** (wikipedia) Constant: [`TERM`](https://javadoc.io/doc/org.apache.camel/camel-dns/latest/org/apache/camel/component/dns/DnsConstants.html#TERM) | **Required** The term. |  |  |

## Examples

### IP lookup

```xml
<route id="IPCheck">
    <from uri="direct:start"/>
    <to uri="dns:ip"/>
</route>
```

This looks up a domain’s IP. For example, _www.example.com_ resolves to 192.0.32.10.

The IP address to lookup must be provided in the header with key `"dns.domain"`.

### DNS lookup

```xml
<route id="IPCheck">
    <from uri="direct:start"/>
    <to uri="dns:lookup"/>
</route>
```

This returns a set of DNS records associated with a domain.  
The name to lookup must be provided in the header with key `"dns.name"`.

### DNS Dig

Dig is a Unix command-line utility to run DNS queries.

```xml
<route id="IPCheck">
    <from uri="direct:start"/>
    <to uri="dns:dig"/>
</route>
```

The query must be provided in the header with key `"dns.query"`.

### Dns Activation Policy

The `DnsActivationPolicy` can be used to dynamically start and stop routes based on dns state.

If you have instances of the same component running in different regions, you can configure a route in each region to activate only if dns is pointing to its region.

For example, you may have an instance in NYC and an instance in SFO. You would configure a service CNAME service.example.com to point to nyc-service.example.com to bring NYC instance up and SFO instance down. When you change the CNAME service.example.com to point to sfo-service.example.com — nyc instance would stop its routes and sfo will bring its routes up. This allows you to switch regions without restarting actual components.

```xml
 <bean id="dnsActivationPolicy" class="org.apache.camel.component.dns.policy.DnsActivationPolicy">
     <property name="hostname" value="service.example.com" />
     <property name="resolvesTo" value="nyc-service.example.com" />
     <property name="ttl" value="60000" />
     <property name="stopRoutesOnException" value="false" />
 </bean>

 <route id="routeId" autoStartup="false" routePolicyRef="dnsActivationPolicy">
 </route>
```

## Spring Boot Auto-Configuration

When using dns with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-dns-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.dns.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.dns.enabled** | Whether to enable auto configuration of the dns component. This is enabled by default. |  | Boolean |
| **camel.component.dns.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
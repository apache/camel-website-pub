# LDIF

**Since Camel 2.20**

**Only producer is supported**

The LDIF component allows you to do updates on an LDAP server from an LDIF body content.

This component uses a basic URL syntax to access the server. It uses the Apache DS LDAP library to process the LDIF. After processing the LDIF, the response body will be a list of statuses for success/failure of each entry.

> **Note**
> The Apache LDAP API is very sensitive to LDIF syntax errors. If in doubt, refer to the unit tests to see an example of each change type.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ldif</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

ldif:ldapServerBean\[?options\]

The _ldapServerBean_ portion of the URI refers to a [LdapConnection](https://directory.apache.org/api/gen-docs/latest/apidocs/org/apache/directory/ldap/client/api/LdapConnection.md). This should be constructed from a factory at the point of use to avoid connection timeouts. The LDIF component only supports producer endpoints, which means that an `ldif` URI cannot appear in the `from` at the start of a route.

For SSL configuration, refer to the `camel-ldap` component where there is an example of setting up a custom SocketFactory instance.

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

The LDIF component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The LDIF endpoint is configured using URI syntax:

ldif:ldapConnectionName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ldapConnectionName** (producer) | **Required** The name of the LdapConnection bean to pull from the registry. Note that this must be of scope prototype to avoid it being shared among threads or using a connection that has timed out. |  | String |

### Query Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Usage

### Body types:

The body can be a URL to an LDIF file or an inline LDIF file. To signify the difference in body types, an inline LDIF must start with:

version: 1

If not, the component will try to parse the body as a URL.

### Result

The result is returned in the Out body as a `ArrayList<java.lang.String>` object. This contains either `_success_` or an Exception message for each LDIF entry.

### LdapConnection

The URI, `ldif:ldapConnectionName`, references a bean with the ID, `ldapConnectionName`. The ldapConnection can be configured using a `LdapConnectionConfig` bean. Note that the scope must have a scope of `prototype` to avoid the connection being shared or picking up a stale connection.

The `LdapConnection` bean may be defined as follows in Spring XML:

```xml
<bean id="ldapConnectionOptions" class="org.apache.directory.ldap.client.api.LdapConnectionConfig">
  <property name="ldapHost" value="${ldap.host}"/>
  <property name="ldapPort" value="${ldap.port}"/>
  <property name="name" value="${ldap.username}"/>
  <property name="credentials" value="${ldap.password}"/>
  <property name="useSsl" value="false"/>
  <property name="useTls" value="false"/>
</bean>

<bean id="ldapConnectionFactory" class="org.apache.directory.ldap.client.api.DefaultLdapConnectionFactory">
  <constructor-arg index="0" ref="ldapConnectionOptions"/>
</bean>

<bean id="ldapConnection" factory-bean="ldapConnectionFactory" factory-method="newLdapConnection" scope="prototype"/>
```

## Examples

Following on from the Spring configuration above, the code sample below sends an LDAP request to filter search a group for a member. The Common Name is then extracted from the response.

_Java-only: sending LDIF content using the ProducerTemplate_

```java
ProducerTemplate<Exchange> template = exchange.getContext().createProducerTemplate();

List<?> results = (Collection<?>) template.sendBody("ldif:ldapConnection, "LDiff goes here");

if (results.size() > 0) {
  // Check for no errors

  for (String result : results) {
    if ("success".equalTo(result)) {
      // LDIF entry success
    } else {
      // LDIF entry failure
    }
  }
}
```

## Spring Boot Auto-Configuration

When using ldif with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-ldif-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.ldif.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ldif.enabled** | Whether to enable auto configuration of the ldif component. This is enabled by default. |  | Boolean |
| **camel.component.ldif.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
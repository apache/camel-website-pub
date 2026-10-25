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

The LDIF component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The LDIF endpoint is configured using URI syntax:

ldif:ldapConnectionName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ldapConnectionName** (producer) | **Required** The name of the LdapConnection bean to pull from the registry. Note that this must be of scope prototype to avoid it being shared among threads or using a connection that has timed out. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **allowUrlBody** (security) | Whether to allow a message body that is not LDIF content to be dereferenced as a URL and fetched. When disabled (default), a body that does not start with version: 1 is rejected with an IllegalArgumentException instead of being fetched as a URL, which avoids a content-sniffed URL fetch (SSRF) from untrusted body content. | false | boolean |

## Message Body

The message body at each side of the LDIF component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `text`, `bytes`, `stream` or `file` | The LDIF text, starting with version: 1, or bytes, a stream or a file of it. With allowUrlBody, a text that is not LDIF is read as the URL of the LDIF file; otherwise it fails, as does a Map or a POJO. |
| **Producer output** | `list` or `null` | A List of one status String per LDIF entry: success, or the error message from the server, which can be empty. No body or an empty body gives null. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

## Usage

### Body types:

The body can be a URL to an LDIF file or an inline LDIF file. To signify the difference in body types, an inline LDIF must start with:

version: 1

If not, the component reads the body as a URL, but only when the `allowUrlBody` option is enabled. By default, such a body is rejected.

### Result

The result is returned in the Out body as a `ArrayList<java.lang.String>` object. This contains either `success` or the error message for each LDIF entry.

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

In YAML, a Groovy script can make the connection:

```yaml
- beans:
    - name: ldapConnection
      type: org.apache.directory.ldap.client.api.LdapConnection
      scriptLanguage: groovy
      script: |
        def config = new org.apache.directory.ldap.client.api.LdapConnectionConfig()
        config.ldapHost = '{{ldap.host}}'
        config.ldapPort = {{ldap.port}}
        config.name = '{{ldap.username}}'
        config.credentials = '{{ldap.password}}'
        new org.apache.directory.ldap.client.api.DefaultLdapConnectionFactory(config).newLdapConnection()
```

A YAML bean is created once, and the component closes the connection after each message. The YAML route in the examples below therefore binds the connection again before each message. This works when the route processes one message at a time.

## Examples

Following on from the Spring configuration above, the code sample below sends LDIF content to the LDAP server, and checks the result of each entry.

_Java-only: sending LDIF content using the ProducerTemplate_

```java
ProducerTemplate template = exchange.getContext().createProducerTemplate();

List<String> results = template.requestBody("ldif:ldapConnection", "LDIF goes here", List.class);

for (String result : results) {
    if ("success".equals(result)) {
        // LDIF entry success
    } else {
        // LDIF entry failure
    }
}
```

The following YAML route applies each LDIF file of a folder to the server, with the connection of the YAML bean above, and logs the result:

```yaml
- route:
    from:
      uri: file:ldif
      steps:
        # the component closes the connection after each message, so bind it again
        - bean:
            ref: ldapConnection
            method: "bind()"
        - to:
            uri: ldif:ldapConnection
        - log:
            message: "LDIF result: ${body}"
```
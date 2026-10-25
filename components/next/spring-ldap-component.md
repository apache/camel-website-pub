# Spring LDAP

**Since Camel 2.11**

**Only producer is supported**

The Spring LDAP component provides a Camel wrapper for [Spring LDAP](http://www.springsource.org/ldap).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spring-ldap</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

spring-ldap:springLdapTemplate\[?options\]

Where **springLdapTemplate** is the name of the [Spring LDAP Template bean](http://static.springsource.org/spring-ldap/site/apidocs/org/springframework/ldap/core/LdapTemplate.md). In this bean, you configure the URL and the credentials for your LDAP access.

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

The Spring LDAP component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Spring LDAP endpoint is configured using URI syntax:

spring-ldap:templateName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **templateName** (producer) | **Required** Name of the Spring LDAP Template bean. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The LDAP operation to be performed.

Enum values:

-   SEARCH
    
-   BIND
    
-   UNBIND
    
-   AUTHENTICATE
    
-   MODIFY\_ATTRIBUTES
    
-   FUNCTION\_DRIVEN
    





 |  | LdapOperation |
| **scope** (producer) | 

The scope of the search operation.

Enum values:

-   object
    
-   onelevel
    
-   subtree
    





 | subtree | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Body

The message body at each side of the Spring LDAP component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `map` | A Map of the parameters of the operation: dn (not needed when the context source has a base DN), filter for search and authenticate, attributes (an Attributes) for bind, password for authenticate, modificationItems (a ModificationItem array) for modify\_attributes, and function and request for function\_driven. Another body, such as a JSON text, fails. |
| **Producer output** | `unchanged` | 
bind, unbind, authenticate and modify\_attributes leave the Map as it was; a failed authenticate throws an exception. search gives a List of the Attributes of the entries found, function\_driven what the function returns.

-   With `operation=SEARCH`: `list` (`java.util.List<javax.naming.directory.Attributes>`)
    
-   With `operation=FUNCTION_DRIVEN`: `unknown`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

The component supports producer endpoint only. An attempt to create a consumer endpoint will result in an `UnsupportedOperationException`.  
The body of the message must be a map (an instance of `java.util.Map`). Unless a base DN is specified by in the configuration of your ContextSource, this map must contain at least an entry with the key **`dn`** (not needed for function\_driven operation) that specifies the root node for the LDAP operation to be performed. Other entries of the map are operation-specific (see below).

The body of the message remains unchanged for the `bind`, `unbind`, `authenticate` and `modify_attributes` operations. For the `search` and `function_driven` operations, the body is set to the result of the search, see [http://static.springsource.org/spring-ldap/site/apidocs/org/springframework/ldap/core/LdapTemplate.html#search%28java.lang.String,%20java.lang.String,%20int,%20org.springframework.ldap.core.AttributesMapper%29](http://static.springsource.org/spring-ldap/site/apidocs/org/springframework/ldap/core/LdapTemplate.html#search%28java.lang.String,%20java.lang.String,%20int,%20org.springframework.ldap.core.AttributesMapper%29).

### Search

The message body must have an entry with the key **`filter`**. The value must be a `String` representing a valid LDAP filter, see [http://en.wikipedia.org/wiki/Lightweight\_Directory\_Access\_Protocol#Search\_and\_Compare](http://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol#Search_and_Compare).

The following route searches for people. The `ldapTemplate` bean and its context source are created as beans in YAML:

-   `initMethod` runs `afterPropertiesSet`, as Spring would. Without it, the context source has no LDAP environment.
    
-   In `constructors`, refer to the context source with `#bean:`.
    
-   The context source sets the base DN, so the map needs no `dn`.
    

The result is a list of `javax.naming.directory.Attributes`:

```yaml
- beans:
    - name: ldapContextSource
      type: org.springframework.ldap.core.support.LdapContextSource
      initMethod: afterPropertiesSet
      properties:
        url: ldap://localhost:389
        base: dc=example,dc=org
        userDn: cn=admin,dc=example,dc=org
        password: "{{ldap.password}}"
    - name: ldapTemplate
      type: org.springframework.ldap.core.LdapTemplate
      constructors:
        0: "#bean:ldapContextSource"
- route:
    from:
      uri: direct:find-people
      steps:
        - setBody:
            expression:
              groovy:
                expression: "[filter: '(objectClass=inetOrgPerson)']"
        - to:
            uri: spring-ldap:ldapTemplate
            parameters:
              operation: SEARCH
        - log:
            message: "Found ${body.size()} people: ${body}"
```

### Bind

The message body must have an entry with the key **`attributes`**. The value must be an instance of [javax.naming.directory.Attributes](http://docs.oracle.com/javase/6/docs/api/javax/naming/directory/Attributes.md) This entry specifies the LDAP node to be created.

### Unbind

No further entries necessary, the node with the specified **`dn`** is deleted.

### Authenticate

The message body must have entries with the keys **`filter`** and **`password`**. The values must be an instance of `String` representing a valid LDAP filter and a user password, respectively.

### Modify Attributes

The message body must have an entry with the key **`modificationItems`**. The value must be an instance of any array of type [javax.naming.directory.ModificationItem](http://docs.oracle.com/javase/6/docs/api/javax/naming/directory/ModificationItem.md)

### Function-Driven

The message body must have entries with the keys **`function`** and **`request`**. The **`function`** value must be of type `java.util.function.BiFunction<L, Q, S>`. The `L` type parameter must be of type `org.springframework.ldap.core.LdapOperations`. The **`request`** value must be the same type as the `Q` type parameter in the **`function`** and it must encapsulate the parameters expected by the LdapTemplate method being invoked within the **`function`**. The `S` type parameter represents the response type as returned by the LdapTemplate method being invoked. This operation allows dynamic invocation of LdapTemplate methods that are not covered by the operations mentioned above.

**Key definitions**

To avoid spelling errors, the following constants are defined in `org.apache.camel.springldap.SpringLdapProducer`:

-   `public static final String DN = "dn"`
    
-   `public static final String FILTER = "filter"`
    
-   `public static final String ATTRIBUTES = "attributes"`
    
-   `public static final String PASSWORD = "password";`
    
-   `public static final String MODIFICATION_ITEMS = "modificationItems";`
    
-   `public static final String FUNCTION = "function";`
    
-   `public static final String REQUEST = "request";`
# LDAP

**Since Camel 1.5**

**Only producer is supported**

The LDAP component allows you to perform searches in LDAP servers using filters as the message payload.

This component uses standard JNDI (`javax.naming` package) to access the server.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ldap</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

ldap:ldapServerBean\[?options\]

The _ldapServerBean_ portion of the URI refers to a [DirContext](https://docs.oracle.com/en/java/javase/17/docs/api/java.naming/javax/naming/directory/DirContext.md) bean in the registry. The LDAP component only supports producer endpoints, which means that an `ldap` URI cannot appear in the `from` at the start of a route.

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

The LDAP component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The LDAP endpoint is configured using URI syntax:

ldap:dirContextName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dirContextName** (producer) | **Required** Name of either a javax.naming.directory.DirContext, or java.util.Hashtable, or Map bean to lookup in the registry. If the bean is either a Hashtable or Map then a new javax.naming.directory.DirContext instance is created for each use. If the bean is a javax.naming.directory.DirContext then the bean is used as given. The latter may not be possible in all situations where the javax.naming.directory.DirContext must not be shared, and in those situations it can be better to use java.util.Hashtable or Map instead. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **base** (producer) | The base DN for searches. | ou=system | String |
| **pageSize** (producer) | When specified the ldap module uses paging to retrieve all results (most LDAP Servers throw an exception when trying to retrieve more than 1000 entries in one query). To be able to use this a LdapContext (subclass of DirContext) has to be passed in as ldapServerBean (otherwise an exception is thrown). |  | Integer |
| **returnedAttributes** (producer) | Comma-separated list of attributes that should be set in each entry of the result. |  | String |
| **scope** (producer) | 
Specifies how deeply to search the tree of entries, starting at the base DN.

Enum values:

-   object
    
-   onelevel
    
-   subtree
    





 | subtree | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Usage

### Result

The result is returned to Out body as a `List<javax.naming.directory.SearchResult>` object.

### DirContext

The URI, `ldap:ldapserver`, references a bean with the ID `ldapserver`. The `ldapserver` bean may be defined as follows:

-   Java (Quarkus)
    
-   XML (Spring)
    

```java
public class LdapServerProducer {

    @Produces
    @Dependent
    @Named("ldapserver")
    public DirContext createLdapServer() throws Exception {
        Hashtable<String, String> env = new Hashtable<>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, "com.sun.jndi.ldap.LdapCtxFactory");
        env.put(Context.PROVIDER_URL, "ldap://localhost:10389");
        env.put(Context.SECURITY_AUTHENTICATION, "none");

        return new InitialDirContext(env);
    }
}
```

```xml
<bean id="ldapserver" class="javax.naming.directory.InitialDirContext" scope="prototype">
  <constructor-arg>
    <props>
      <prop key="java.naming.factory.initial">com.sun.jndi.ldap.LdapCtxFactory</prop>
      <prop key="java.naming.provider.url">ldap://localhost:10389</prop>
      <prop key="java.naming.security.authentication">none</prop>
    </props>
  </constructor-arg>
</bean>
```

The preceding example declares a regular Sun-based LDAP `DirContext` that connects anonymously to a locally hosted LDAP server.

> **Note**
> `DirContext` objects are **not** required to support concurrency by contract. It is therefore important to manage the directory context’s lifecycle appropriately. In the Spring framework, `prototype` scoped objects are instantiated each time they are looked up to ensure concurrency and avoid sharing the same context between multiple threads.
>
> For Camel Quarkus applications, you can achieve similar behavior by using the `@Dependent` annotation. When you annotate a component or bean with `@Dependent`, a new instance of the component is created for each injection point or usage, which effectively provides the same concurrency guarantees as Spring’s `prototype` scope. This ensures that each part of your application interacts with a separate and isolated `DirContext` instance, preventing unintended thread interference.

### Security concerns related to LDAP injection

> **Important**
> The camel-ldap component uses the message body to filter the search results. Therefore, the message body should be protected from LDAP injection. To assist with this, you can use `org.apache.camel.component.ldap.LdapHelper` utility class that has method(s) to escape string values to be LDAP injection safe.

See the following link for information about [LDAP Injection](https://cheatsheetseries.owasp.org/cheatsheets/LDAP_Injection_Prevention_Cheat_Sheet.md).

## Examples

Following on from the configuration above, the code sample below sends an LDAP request to filter search a group for a member. The Common Name is then extracted from the response.

_Java-only: Java test API (ProducerTemplate)_

```java
ProducerTemplate template = exchange.getContext().createProducerTemplate();

Collection<SearchResult> results = template.requestBody(
    "ldap:ldapserver?base=ou=mygroup,ou=groups,ou=system",
    "(member=uid=huntc,ou=users,ou=system)", Collection.class);

if (results.size() > 0) {
  // Extract what we need from the device's profile

  Iterator<SearchResult> resultIter = results.iterator();
  SearchResult searchResult = (SearchResult) resultIter.next();
  Attributes attributes = searchResult.getAttributes();
  Attribute deviceCNAttr = attributes.get("cn");
  String deviceCN = (String) deviceCNAttr.get();
  // ...
}
```

If no specific filter is required (for example, you need to look up a single entry), specify a wildcard filter expression. If the LDAP entry has a Common Name, use a filter expression like:

(cn=\*)

### Binding using credentials

A Camel end user donated this sample code he used to bind to the ldap server using credentials.

_Java-only: Java programmatic CamelContext and LDAP context setup_

```java
Properties props = new Properties();
props.setProperty(Context.INITIAL_CONTEXT_FACTORY, "com.sun.jndi.ldap.LdapCtxFactory");
props.setProperty(Context.PROVIDER_URL, "ldap://localhost:389");
props.setProperty(Context.URL_PKG_PREFIXES, "com.sun.jndi.url");
props.setProperty(Context.REFERRAL, "ignore");
props.setProperty(Context.SECURITY_AUTHENTICATION, "simple");
props.setProperty(Context.SECURITY_PRINCIPAL, "cn=Manager");
props.setProperty(Context.SECURITY_CREDENTIALS, "secret");

DefaultRegistry reg = new DefaultRegistry();
reg.bind("myldap", new InitialLdapContext(props, null));

from("direct:start").to("ldap:myldap?base=ou=test");
```

## Configuring SSL

All that is required is to create a custom socket factory and reference it in the `InitialDirContext` bean. See the sample below.

**SSL Configuration**

-   Java (Quarkus)
    
-   XML (Spring)
    

```java
public class LdapServerProducer {

    @Produces
    @Dependent
    @Named("ldapserver")
    public DirContext createLdapServer() throws Exception {
        Hashtable<String, String> env = new Hashtable<>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, "com.sun.jndi.ldap.LdapCtxFactory");
        env.put(Context.PROVIDER_URL, "ldaps://" + InetAddress.getLocalHost().getCanonicalHostName() + ":10636");
        env.put(Context.SECURITY_AUTHENTICATION, "none");
        env.put("java.naming.ldap.factory.socket", CustomSSLSocketFactory.class.getName());

        return new InitialDirContext(env);
    }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
    http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">

    <sslContextParameters xmlns="http://camel.apache.org/schema/spring" id="sslContextParameters" >
        <keyManagers keyPassword="{{keystore.pwd}}">
            <keyStore resource="{{keystore.url}}" password="{{keystore.pwd}}"/>
        </keyManagers>
    </sslContextParameters>

    <bean id="customSocketFactory" class="com.example.ldap.CustomSocketFactory">
        <constructor-arg index="0" ref="sslContextParameters"/>
    </bean>

    <bean id="ldapserver" class="javax.naming.directory.InitialDirContext" scope="prototype">
        <constructor-arg>
            <props>
                <prop key="java.naming.factory.initial">com.sun.jndi.ldap.LdapCtxFactory</prop>
                <prop key="java.naming.provider.url">ldaps://127.0.0.1:10636</prop>
                <prop key="java.naming.security.protocol">ssl</prop>
                <prop key="java.naming.security.authentication">none</prop>
                <prop key="java.naming.ldap.factory.socket">com.example.ldap.CustomSocketFactory</prop>
            </props>
        </constructor-arg>
    </bean>
</beans>
```

**Custom Socket Factory**

-   Java (Quarkus)
    
-   XML (Spring)
    

```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.InetAddress;
import java.net.Socket;
import java.net.UnknownHostException;
import java.security.KeyStore;

import javax.net.SocketFactory;
import javax.net.ssl.SSLContext;
import javax.net.ssl.SSLSocketFactory;
import javax.net.ssl.TrustManagerFactory;

import org.eclipse.microprofile.config.ConfigProvider;

public class CustomSSLSocketFactory extends SSLSocketFactory {

    private SSLSocketFactory delegate;

    public CustomSSLSocketFactory() throws Exception {
        String trustStoreFilename = ConfigProvider.getConfig().getValue("ldap.trustStore", String.class);
        String trustStorePassword = ConfigProvider.getConfig().getValue("ldap.trustStorePassword", String.class);
        KeyStore keyStore = KeyStore.getInstance(KeyStore.getDefaultType());
        try (InputStream in = new FileInputStream(trustStoreFilename)) {
            keyStore.load(in, trustStorePassword.toCharArray());
        }
        TrustManagerFactory tmf = TrustManagerFactory.getInstance("SunX509");
        tmf.init(keyStore);
        SSLContext ctx = SSLContext.getInstance("TLS");
        ctx.init(null, tmf.getTrustManagers(), null);
        delegate = ctx.getSocketFactory();
    }

    public static SocketFactory getDefault() {
        try {
            return new CustomSSLSocketFactory();
        } catch (Exception ex) {
            ex.printStackTrace();
            return null;
        }
    }

    @Override
    public Socket createSocket(Socket s, String host, int port, boolean autoClose) throws IOException {
        return delegate.createSocket(s, host, port, autoClose);
    }

    @Override
    public String[] getDefaultCipherSuites() {
        return delegate.getDefaultCipherSuites();
    }

    @Override
    public String[] getSupportedCipherSuites() {
        return delegate.getSupportedCipherSuites();
    }

    @Override
    public Socket createSocket(String host, int port) throws IOException, UnknownHostException {
        return delegate.createSocket(host, port);
    }

    @Override
    public Socket createSocket(InetAddress address, int port) throws IOException {
        return delegate.createSocket(address, port);
    }

    @Override
    public Socket createSocket(String host, int port, InetAddress localAddress, int localPort)
            throws IOException, UnknownHostException {
        return delegate.createSocket(host, port, localAddress, localPort);
    }

    @Override
    public Socket createSocket(InetAddress address, int port, InetAddress localAddress, int localPort)
            throws IOException {
        return delegate.createSocket(address, port, localAddress, localPort);
    }
}
```

The constructor uses the `ConfigProvider` to read the `ldap.trustStore` and `ldap.trustStorePassword` configuration properties, which could be specified in the `application.properties` file as follows:

```properties
ldap.trustStore=/path/to/truststore.jks
ldap.trustStorePassword=secret
```

```java
package com.example.ldap;

import java.io.IOException;
import java.net.InetAddress;
import java.net.Socket;
import java.security.KeyStore;

import javax.net.SocketFactory;
import javax.net.ssl.SSLContext;
import javax.net.ssl.SSLSocketFactory;
import javax.net.ssl.TrustManagerFactory;

import org.apache.camel.support.jsse.SSLContextParameters;

/**
 * The CustomSocketFactory. Loads the KeyStore and creates an instance of SSLSocketFactory
 */
public class CustomSocketFactory extends SSLSocketFactory {

    private static SSLSocketFactory socketFactory;

    /**
     * Called by the getDefault() method.
     */
    public CustomSocketFactory() {
    }

    /**
     * Called by Spring Boot DI to initialize an instance of SocketFactory
     */
    public CustomSocketFactory(SSLContextParameters sslContextParameters) {
        try {
            KeyStore keyStore = sslContextParameters.getKeyManagers().getKeyStore().createKeyStore();
            TrustManagerFactory tmf = TrustManagerFactory.getInstance("SunX509");
            tmf.init(keyStore);
            SSLContext ctx = SSLContext.getInstance("TLS");
            ctx.init(null, tmf.getTrustManagers(), null);
            socketFactory = ctx.getSocketFactory();
        } catch (Exception ex) {
            ex.printStackTrace(System.err);
        }
    }

    /**
     * Getter for the SocketFactory
     */
    public static SocketFactory getDefault() {
        return new CustomSocketFactory();
    }

    @Override
    public String[] getDefaultCipherSuites() {
        return socketFactory.getDefaultCipherSuites();
    }

    @Override
    public String[] getSupportedCipherSuites() {
        return socketFactory.getSupportedCipherSuites();
    }

    @Override
    public Socket createSocket(Socket socket, String string, int i, boolean bln) throws IOException {
        return socketFactory.createSocket(socket, string, i, bln);
    }

    @Override
    public Socket createSocket(String string, int i) throws IOException {
        return socketFactory.createSocket(string, i);
    }

    @Override
    public Socket createSocket(String string, int i, InetAddress ia, int i1) throws IOException {
        return socketFactory.createSocket(string, i, ia, i1);
    }

    @Override
    public Socket createSocket(InetAddress ia, int i) throws IOException {
        return socketFactory.createSocket(ia, i);
    }

    @Override
    public Socket createSocket(InetAddress ia, int i, InetAddress ia1, int i1) throws IOException {
        return socketFactory.createSocket(ia, i, ia1, i1);
    }
}
```
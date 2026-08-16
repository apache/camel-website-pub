# Servlet

JVM since0.2.0 Native since0.0.2

Serve HTTP requests by a Servlet.

## What’s inside

-   [Servlet component](../../../../components/4.22.x/servlet-component.md), URI syntax: `servlet:contextPath`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-servlet)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-servlet</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Configuring CamelHttpTransportServlet

#### Minimal configuration

The simplest way to configure `CamelHttpTransportServlet` is with configuration properties. The most minimal setup requires that you define one or more URL patterns for the Servlet with `quarkus.camel.servlet.url-patterns`.

For example with configuration like the following.

```properties
quarkus.camel.servlet.url-patterns = /*
```

And a Camel route.

```java
from("servlet://greet")
    .setBody().constant("Hello World");
```

Produces the message `Hello World`.

#### Advanced configuration

**Servlet name**

To give a specific name to the Servlet you can use the `quarkus.camel.servlet.servlet-name` configuration option.

```properties
quarkus.camel.servlet.servlet-name = My Custom Name
```

**Servlet class**

You may use a custom Servlet class (E.g. one that extends `CamelHttpTransportServlet`) in your Camel routes.

```properties
quarkus.camel.servlet.servlet-class = org.acme.MyCustomServlet
```

**Multiple named Servlets**

For more advanced use cases you can configure multiple 'named' Servlets.

```properties
quarkus.camel.servlet.my-servlet-a.servlet-name = my-custom-a
quarkus.camel.servlet.my-servlet-a.url-patterns = /custom/a/*

quarkus.camel.servlet.my-servlet-b.servlet-name = my-custom-b
quarkus.camel.servlet.my-servlet-b.servlet-class = org.acme.CustomServletB
quarkus.camel.servlet.my-servlet-b.url-patterns = /custom/b/*
```

```java
from("servlet://greet?servletName=my-custom-a")
    .setBody().constant("Hello World");

from("servlet://goodbye?servletName=my-custom-b")
    .setBody().constant("Goodbye World");
```

**Finer control of Servlet configuration**

If you need more control of the Servlet configuration, for example to configure custom init parameters, then you can do this with a custom Servlet class through the `jakarta.servlet.annotation.WebServlet` annotation options.

```java
import jakarta.servlet.annotation.WebServlet;
import org.apache.camel.component.servlet.CamelHttpTransportServlet;

@WebServlet(
    urlPatterns = {"/*"},
    initParams = {
        @WebInitParam(name = "myParam", value = "myValue")
    }
)
public class MyCustomServlet extends CamelHttpTransportServlet {
}
```

Or you can configure the `CamelHttpTransportServlet` using a `web-app` descriptor placed into `src/main/resources/META-INF/web.xml`.

```xml
<web-app>
  <servlet>
    <servlet-name>CamelServlet</servlet-name>
    <servlet-class>org.apache.camel.component.servlet.CamelHttpTransportServlet</servlet-class>
  </servlet>

  <servlet-mapping>
    <servlet-name>CamelServlet</servlet-name>
    <url-pattern>/services/*</url-pattern>
  </servlet-mapping>
</web-app>
```

## transferException option in native mode

To use the `transferException` option in native mode, you must enable support for object serialization. Refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

You will also need to enable serialization for the exception classes that you intend to serialize. For example.

```java
@RegisterForReflection(targets = { IllegalStateException.class, MyCustomException.class }, serialization = true)
```

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.servlet.url-patterns](#quarkus-camel-servlet-url-patterns)`
A comma separated list of path patterns under which the CamelServlet should be accessible. Example path patterns: `/*`, `/services/*`

 | List of `string` |  |
| `[quarkus.camel.servlet.servlet-class](#quarkus-camel-servlet-servlet-class)`

A fully qualified name of a servlet class to serve paths that match `url-patterns`

 | `string` | `org.apache.camel.component.servlet.CamelHttpTransportServlet` |
| `[quarkus.camel.servlet.servlet-name](#quarkus-camel-servlet-servlet-name)`

A servletName as it would be defined in a `web.xml` file or in the `jakarta.servlet.annotation.WebServlet#name()` annotation.

 | `string` | `CamelServlet` |
| `[quarkus.camel.servlet.load-on-startup](#quarkus-camel-servlet-load-on-startup)`

Sets the loadOnStartup priority on the Servlet. A loadOnStartup is a value greater than or equal to zero, indicates to the container the initialization priority of the Servlet. If loadOnStartup is a negative integer, the Servlet is initialized lazily.

 | `int` | `-1` |
| `[quarkus.camel.servlet.async](#quarkus-camel-servlet-async)`

Enables Camel to benefit from asynchronous Servlet support.

 | `boolean` | `false` |
| `[quarkus.camel.servlet.force-await](#quarkus-camel-servlet-force-await)`

When set to `true` used in conjunction with `quarkus.camel.servlet.async = true`, this will force route processing to run synchronously.

 | `boolean` | `false` |
| `[quarkus.camel.servlet.executor-ref](#quarkus-camel-servlet-executor-ref)`

The name of a bean to configure an optional custom thread pool for handling Camel Servlet processing.

 | `string` |  |
| `[quarkus.camel.servlet.multipart.location](#quarkus-camel-servlet-multipart-location)`

An absolute path to a directory on the file system to store files temporarily while the parts are processed or when the size of the file exceeds the specified file-size-threshold configuration value.

 | `string` |  |
| `[quarkus.camel.servlet.multipart.max-file-size](#quarkus-camel-servlet-multipart-max-file-size)`

The maximum size allowed in bytes for uploaded files. The default size (-1) allows an unlimited size.

 | `long` | `-1` |
| `[quarkus.camel.servlet.multipart.max-request-size](#quarkus-camel-servlet-multipart-max-request-size)`

The maximum size allowed in bytes for a multipart/form-data request. The default size (-1) allows an unlimited size.

 | `long` | `-1` |
| `[quarkus.camel.servlet.multipart.file-size-threshold](#quarkus-camel-servlet-multipart-file-size-threshold)`

The file size in bytes after which the file will be temporarily stored on disk.

 | `int` | `0` |
| `[quarkus.camel.servlet."named-servlets".url-patterns](#quarkus-camel-servlet-named-servlets-url-patterns)`

A comma separated list of path patterns under which the CamelServlet should be accessible. Example path patterns: `/*`, `/services/*`

 | List of `string` |  |
| `[quarkus.camel.servlet."named-servlets".servlet-class](#quarkus-camel-servlet-named-servlets-servlet-class)`

A fully qualified name of a servlet class to serve paths that match `url-patterns`

 | `string` | `org.apache.camel.component.servlet.CamelHttpTransportServlet` |
| `[quarkus.camel.servlet."named-servlets".servlet-name](#quarkus-camel-servlet-named-servlets-servlet-name)`

A servletName as it would be defined in a `web.xml` file or in the `jakarta.servlet.annotation.WebServlet#name()` annotation.

 | `string` | `CamelServlet` |
| `[quarkus.camel.servlet."named-servlets".load-on-startup](#quarkus-camel-servlet-named-servlets-load-on-startup)`

Sets the loadOnStartup priority on the Servlet. A loadOnStartup is a value greater than or equal to zero, indicates to the container the initialization priority of the Servlet. If loadOnStartup is a negative integer, the Servlet is initialized lazily.

 | `int` | `-1` |
| `[quarkus.camel.servlet."named-servlets".async](#quarkus-camel-servlet-named-servlets-async)`

Enables Camel to benefit from asynchronous Servlet support.

 | `boolean` | `false` |
| `[quarkus.camel.servlet."named-servlets".force-await](#quarkus-camel-servlet-named-servlets-force-await)`

When set to `true` used in conjunction with `quarkus.camel.servlet.async = true`, this will force route processing to run synchronously.

 | `boolean` | `false` |
| `[quarkus.camel.servlet."named-servlets".executor-ref](#quarkus-camel-servlet-named-servlets-executor-ref)`

The name of a bean to configure an optional custom thread pool for handling Camel Servlet processing.

 | `string` |  |
| `[quarkus.camel.servlet."named-servlets".multipart.location](#quarkus-camel-servlet-named-servlets-multipart-location)`

An absolute path to a directory on the file system to store files temporarily while the parts are processed or when the size of the file exceeds the specified file-size-threshold configuration value.

 | `string` |  |
| `[quarkus.camel.servlet."named-servlets".multipart.max-file-size](#quarkus-camel-servlet-named-servlets-multipart-max-file-size)`

The maximum size allowed in bytes for uploaded files. The default size (-1) allows an unlimited size.

 | `long` | `-1` |
| `[quarkus.camel.servlet."named-servlets".multipart.max-request-size](#quarkus-camel-servlet-named-servlets-multipart-max-request-size)`

The maximum size allowed in bytes for a multipart/form-data request. The default size (-1) allows an unlimited size.

 | `long` | `-1` |
| `[quarkus.camel.servlet."named-servlets".multipart.file-size-threshold](#quarkus-camel-servlet-named-servlets-multipart-file-size-threshold)`

The file size in bytes after which the file will be temporarily stored on disk.

 | `int` | `0` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.
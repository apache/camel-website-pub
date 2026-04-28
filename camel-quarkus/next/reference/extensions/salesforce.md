# Salesforce

JVM since0.2.0 Native since0.0.2

Communicate with Salesforce using Java DTOs.

## What’s inside

-   [Salesforce component](../../../../components/next/salesforce-component.md), URI syntax: `salesforce:operationName:topicName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-salesforce)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-salesforce</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Generating Salesforce DTOs with the `salesforce-maven-plugin`

To generate Salesforce DTOs for your project, use the `salesforce-maven-plugin`. The example code snippet below creates a single DTO for the `Account` object.

```xml
<plugin>
    <groupId>org.apache.camel.maven</groupId>
    <artifactId>camel-salesforce-maven-plugin</artifactId>
    <version>4.20.0</version>
    <executions>
        <execution>
            <goals>
                <goal>generate</goal>
            </goals>
            <configuration>
                <clientId>${env.SALESFORCE_CLIENTID}</clientId>
                <clientSecret>${env.SALESFORCE_CLIENTSECRET}</clientSecret>
                <userName>${env.SALESFORCE_USERNAME}</userName>
                <password>${env.SALESFORCE_PASSWORD}</password>
                <loginUrl>https://login.salesforce.com</loginUrl>
                <packageName>org.apache.camel.quarkus.component.salesforce.generated</packageName>
                <outputDirectory>src/main/java</outputDirectory>
                <includes>
                    <include>Account</include>
                </includes>
            </configuration>
        </execution>
    </executions>
</plugin>
```

### Native mode support for Pub / Sub API with POJO `pubSubDeserializeType`

When using the Camel Salesforce Pub / Sub API and `pubSubDeserializeType` is configured as `POJO`, you must register any classes configured on the `pubSubPojoClass` option for reflection.

For example, given the following route.

```java
from("salesforce:pubSubSubscribe:/event/TestEvent__e?pubSubDeserializeType=POJO&pubSubPojoClass=org.foo.TestEvent")
    .log("Received Salesforce POJO topic message: ${body}");
```

Class `org.foo.TestEvent` would need to be registered for reflection.

```java
package org.foo;

import io.quarkus.runtime.annotations.RegisterForReflection;

@RegisterForReflection
public class TestEvent {
    // Getters / setters etc
}
```

Refer to the [Native mode](../../user-guide/native-mode.html#reflection) user guide for more information.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).
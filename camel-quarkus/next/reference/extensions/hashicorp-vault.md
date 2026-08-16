# Hashicorp Vault

JVM since2.11.0 Native since3.15.0

Manage secrets in HashiCorp Vault Service

## What’s inside

-   [HashiCorp Vault component](../../../../components/4.22.x/hashicorp-vault-component.md), URI syntax: `hashicorp-vault:secretsEngine`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-hashicorp-vault)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-hashicorp-vault</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Using a POJO for the `createSecret` operation in native mode

It is possible to use a POJO as the message body for the `createSecret` operation. In native mode, you must register any such POJO classes for reflection. E.g. via the `@RegisterForReflection` annotation or configuration property `quarkus.camel.native.reflection.include-patterns`.

For example.

```java
@RegisterForReflection
public class Credentials {
    private String username;
    private String password;

    // Getters & setters
}
```

```java
from("direct:createSecret")
    .process(new Processor() {
        @Override
        public void process(Exchange exchange) {
            Credentials credentials = new Credentials();
            credentials.setUsername("admin");
            credentials.setPassword("2s3cr3t");
            exchange.getMessage().setBody(credentials);
        }
    })
    .to("hashicorp-vault:secret?operation=createSecret&token=my-token&secretPath=my-secret")
```

Refer to the [Native mode](../../user-guide/native-mode.html#reflection) user guide for more information.
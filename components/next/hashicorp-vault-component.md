# HashiCorp Vault

**Since Camel 3.18**

**Only producer is supported**

The hashicorp-vault component that integrates [HashiCorp Vault](https://www.vaultproject.io/).

## URI Format

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-hashicorp-vault</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The HashiCorp Vault component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The HashiCorp Vault endpoint is configured using URI syntax:

hashicorp-vault:secretsEngine

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **secretsEngine** (producer) | Vault Name to be used. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cloud** (producer) | Determine if the Hashicorp Vault is deployed on Hashicorp Cloud or not. | false | boolean |
| **host** (producer) | Hashicorp Vault instance host to be used. |  | String |
| **namespace** (producer) | If the Hashicorp Vault instance is deployed on Hashicorp Cloud, this field will determine the namespace. |  | String |
| **operation** (producer) | 
Operation to be performed.

Enum values:

-   createSecret
    
-   getSecret
    
-   deleteSecret
    
-   listSecrets
    





 |  | HashicorpVaultOperation |
| **port** (producer) | Hashicorp Vault instance port to be used. | 8200 | String |
| **scheme** (producer) | Hashicorp Vault instance scheme to be used. | https | String |
| **secretPath** (producer) | Hashicorp Vault instance secret Path to be used. |  | String |
| **vaultTemplate** (producer) | **Autowired** Instance of Vault template. |  | VaultTemplate |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **authentication** (security) | 

How to log in to HashiCorp Vault: token (a fixed token), approle (a role ID and a secret ID), kubernetes (the service account token of the pod), jwt (a JWT, such as a workload identity token) or cert (the TLS client certificate of the keyStore). The token is renewed before it expires, and the endpoint logs in again when the token can no longer be renewed.

Enum values:

-   token
    
-   approle
    
-   kubernetes
    
-   jwt
    
-   cert
    





 | token | String |
| **authMountPath** (security) | The path the login method is mounted at in HashiCorp Vault (without auth/), when it is not the default path of the login method: approle, kubernetes or jwt. |  | String |
| **jwt** (security) | The JWT to log in with, for the jwt and kubernetes logins. For a JWT that is replaced over time, such as a projected service account token, use jwtFile instead. |  | String |
| **jwtFile** (security) | The file to read the JWT from at every login, for the jwt and kubernetes logins. The kubernetes login reads /var/run/secrets/kubernetes.io/serviceaccount/token when neither jwt nor jwtFile is set. |  | String |
| **keyStore** (security) | The file with the TLS client certificate and its private key, which the endpoint presents to HashiCorp Vault: for the cert login, or for a Vault that requires client certificates. A PKCS12 or JKS key store, or PEM with the certificate and the PKCS#8 private key. |  | String |
| **keyStorePassword** (security) | The password of the key store and of its private key, when it is a PKCS12 or JKS key store. |  | String |
| **role** (security) | The HashiCorp Vault role to log in as, for the kubernetes and jwt logins. The jwt login can leave it out when the login method has a default role. |  | String |
| **roleId** (security) | The role ID of the AppRole, for the approle login. |  | String |
| **secretId** (security) | The secret ID of the AppRole, for the approle login. |  | String |
| **token** (security) | Token to be used, for the token login. |  | String |
| **trustStore** (security) | The file with the certificates to trust for the TLS connection to HashiCorp Vault, such as the CA certificate of a private CA: a PKCS12 or JKS trust store, or PEM certificates. When not set, the JVM trusts the certificate as for any other TLS connection. |  | String |
| **trustStorePassword** (security) | The password of the trust store, when it is a PKCS12 or JKS trust store. |  | String |

## Message Headers

The HashiCorp Vault component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHashicorpVaultProducerOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-hashicorp-vault/latest/org/apache/camel/component/hashicorp/vault/HashicorpVaultConstants.html#OPERATION) | Overrides the desired operation to be used in the producer. |  | String |
| **CamelHashicorpVaultSecretPath** (producer) Constant: [`SECRET_PATH`](https://javadoc.io/doc/org.apache.camel/camel-hashicorp-vault/latest/org/apache/camel/component/hashicorp/vault/HashicorpVaultConstants.html#SECRET_PATH) | Set the desired secret path as header. |  | String |
| **CamelHashicorpVaultSecretVersion** (producer) Constant: [`SECRET_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-hashicorp-vault/latest/org/apache/camel/component/hashicorp/vault/HashicorpVaultConstants.html#SECRET_VERSION) | Set the desired secret version as header. |  | String |

## Message Body

The message body at each side of the HashiCorp Vault component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `map`, `pojo`, `text`, `bytes`, `stream` or `file` | 
The fields of the secret for createSecret, the default operation: a Map of the keys and values, a POJO written as JSON, or text, bytes, a stream or a file with a JSON object. A List or no body fails. The other operations take the secret from the secretPath option or the CamelHashicorpVaultSecretPath header.

-   With `operation=getSecret`: `any`
    
-   With `operation=deleteSecret`: `any`
    
-   With `operation=listSecrets`: `any`
    





 |
| **Producer output** | `unchanged` | 

getSecret gives a Map with the fields of the secret under data and its version under metadata, or no body when the secret does not exist or is deleted. listSecrets gives a List of the names of the secrets in the engine; createSecret and deleteSecret leave the body unchanged.

-   With `operation=getSecret`: `map` or `null`
    
-   With `operation=listSecrets`: `list` (`java.util.List<java.lang.String>`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Authentication and HashiCorp Vault on-premise vs HashiCorp Cloud

The component supports operations at the producer level. Specifically, it provides the following functionalities:

-   `createSecret`
    
-   `getSecret`
    
-   `deleteSecret`
    
-   `listSecrets`
    

The component can interact with HashiCorp Vault, which may be deployed either as an on-premise/local instance or as a HashiCorp Vault Cloud instance (Enterprise version).

### Configuration for HashiCorp Vault Cloud

When using a HashiCorp Vault Cloud instance, in addition to the standard parameters such as `host`, `port`, `scheme`, and `token`, you must configure the following additional parameters:

-   `cloud`:: A boolean flag that must be explicitly set to `true` to indicate that the HashiCorp Vault instance is hosted in the cloud.
    
-   `namespace`:: The namespace of your secrets engine. The operations work on `<namespace>/<secretsEngine>`; without a namespace they work on the secrets engine itself, as on-premise.
    

### Logging in to HashiCorp Vault

The `authentication` option chooses how the component logs in to HashiCorp Vault:

 
| Login | Settings |
| --- | --- |
| `token` (the default) | `token`: a token created in Vault beforehand. |
| `approle` | `roleId` and `secretId`: the role ID and a secret ID of an AppRole. |
| `kubernetes` | `role`: the Vault role of the application. The login sends the service account token of the pod, which it reads from `/var/run/secrets/kubernetes.io/serviceaccount/token`, or from the file set with `jwtFile`. |
| `jwt` | `jwt`, or `jwtFile` to read the JWT from a file. `role` is the Vault role to log in as, which can be left out when the JWT login of Vault has a default role. |
| `cert` | `keyStore`: the TLS client certificate, see [TLS](#_tls). `role` is the name of the certificate role in Vault; without it, Vault tries every certificate role that trusts the certificate. The login needs the `https` scheme. |

When the login method is not mounted at its default path in Vault (`approle`, `kubernetes`, `jwt` or `cert`), set the path with `authMountPath`, without `auth/`.

Camel renews the token before it expires, and logs in again when the token can no longer be renewed, such as when it reached its maximum time to live. A JWT read from a file is read again at every login, so a token that the platform replaces in the file, such as a projected service account token, is picked up. When the endpoint stops, Camel revokes the token of its login. A token given for the token login is renewed when it is renewable, but never revoked.

On HashiCorp Cloud (`cloud=true` and a `namespace`), the login is made in the namespace, as are the renewal and the revocation of the token.

For example, an endpoint that logs in with an AppRole, whose role ID and secret ID are in environment variables:

```java
from("direct:start")
    .to("hashicorp-vault:secret?operation=getSecret&host=vault.example.com&authentication=approle"
        + "&roleId={{env:VAULT_ROLE_ID}}&secretId=RAW({{env:VAULT_SECRET_ID}})")
    .log("${body}");
```

### TLS

With the `https` scheme, the component trusts the certificate of Vault as any other TLS connection of the JVM does. For a Vault whose certificate is signed by a private CA, set `trustStore` to the certificates to trust: a PKCS12 or JKS trust store with its `trustStorePassword`, or a PEM file with the CA certificates, such as the file that the `VAULT_CACERT` environment variable of the Vault CLI points to.

To present a client certificate to Vault, for the `cert` login or for a Vault that requires client certificates, set `keyStore`: a PKCS12 or JKS key store with its `keyStorePassword`, or a PEM file with the certificate and its private key. The key of a PEM file is not encrypted, in PKCS#8 (`-----BEGIN PRIVATE KEY-----`) or, for an RSA key, in PKCS#1 (`-----BEGIN RSA PRIVATE KEY-----`).

For example, the properties function logs in with a client certificate:

```properties
camel.vault.hashicorp.host = vault.example.com
camel.vault.hashicorp.port = 8200
camel.vault.hashicorp.scheme = https
camel.vault.hashicorp.trustStore = /etc/vault/ca.pem
camel.vault.hashicorp.authentication = cert
camel.vault.hashicorp.role = my-application
camel.vault.hashicorp.keyStore = /etc/vault/client.pem
```

### OpenBao

The component, the properties function and the secret refresh task also work with [OpenBao](https://openbao.org/), the open source fork of HashiCorp Vault, which keeps the API of Vault. OpenBao has the token, AppRole, Kubernetes, JWT and TLS certificate logins built in.

## Examples

### Using the producer operations

The producer works on a secrets engine, given as the path of the endpoint (`secret` is the default key/value engine), and connects with the `host`, `port`, `scheme` and `token` endpoint options. The `operation` option selects what to do, and `secretPath` names the secret to work on; the `CamelHashicorpVaultProducerOperation` and `CamelHashicorpVaultSecretPath` headers override them per message.

#### Creating a secret

The message body is the map of key/value pairs to store as the secret. A POJO is written as JSON, and text, bytes, a stream or a file must hold a JSON object of the fields. A message without a body fails, instead of writing a new, empty version of the secret:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createSecret")
    .to("hashicorp-vault:secret?operation=createSecret&secretPath=database&host=localhost&port=8200&scheme=http&token={{vault.token}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:createSecret"/>
        <to uri="hashicorp-vault:secret?operation=createSecret&amp;secretPath=database&amp;host=localhost&amp;port=8200&amp;scheme=http&amp;token={{vault.token}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:createSecret
      steps:
        - to:
            uri: hashicorp-vault:secret?operation=createSecret&secretPath=database&host=localhost&port=8200&scheme=http&token={{vault.token}}
```

#### Getting a secret

The message body becomes a Map with the fields of the secret under `data` and its version details under `metadata`, or no body when the secret does not exist; the `CamelHashicorpVaultSecretVersion` header reads a given version (a number) instead of the latest:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getSecret")
    .to("hashicorp-vault:secret?operation=getSecret&secretPath=database&host=localhost&port=8200&scheme=http&token={{vault.token}}")
    .log("The database secret is ${body}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:getSecret"/>
        <to uri="hashicorp-vault:secret?operation=getSecret&amp;secretPath=database&amp;host=localhost&amp;port=8200&amp;scheme=http&amp;token={{vault.token}}"/>
        <log message="The database secret is ${body}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:getSecret
      steps:
        - to:
            uri: hashicorp-vault:secret?operation=getSecret&secretPath=database&host=localhost&port=8200&scheme=http&token={{vault.token}}
        - log:
            message: "The database secret is ${body}"
```

The secret can also be chosen per message with the `CamelHashicorpVaultSecretPath` header:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getSecret")
    .setHeader(HashicorpVaultConstants.SECRET_PATH, constant("database"))
    .to("hashicorp-vault:secret?operation=getSecret&host=localhost&port=8200&scheme=http&token={{vault.token}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:getSecret"/>
        <setHeader name="CamelHashicorpVaultSecretPath">
            <constant>database</constant>
        </setHeader>
        <to uri="hashicorp-vault:secret?operation=getSecret&amp;host=localhost&amp;port=8200&amp;scheme=http&amp;token={{vault.token}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:getSecret
      steps:
        - setHeader:
            name: CamelHashicorpVaultSecretPath
            expression:
              constant:
                expression: database
        - to:
            uri: hashicorp-vault:secret?operation=getSecret&host=localhost&port=8200&scheme=http&token={{vault.token}}
```

#### Deleting a secret

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deleteSecret")
    .to("hashicorp-vault:secret?operation=deleteSecret&secretPath=database&host=localhost&port=8200&scheme=http&token={{vault.token}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:deleteSecret"/>
        <to uri="hashicorp-vault:secret?operation=deleteSecret&amp;secretPath=database&amp;host=localhost&amp;port=8200&amp;scheme=http&amp;token={{vault.token}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:deleteSecret
      steps:
        - to:
            uri: hashicorp-vault:secret?operation=deleteSecret&secretPath=database&host=localhost&port=8200&scheme=http&token={{vault.token}}
```

#### Listing the secrets

The message body becomes the list of the names of the secrets in the engine:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:listSecrets")
    .to("hashicorp-vault:secret?operation=listSecrets&host=localhost&port=8200&scheme=http&token={{vault.token}}")
    .log("The secrets are ${body}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:listSecrets"/>
        <to uri="hashicorp-vault:secret?operation=listSecrets&amp;host=localhost&amp;port=8200&amp;scheme=http&amp;token={{vault.token}}"/>
        <log message="The secrets are ${body}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:listSecrets
      steps:
        - to:
            uri: hashicorp-vault:secret?operation=listSecrets&host=localhost&port=8200&scheme=http&token={{vault.token}}
        - log:
            message: "The secrets are ${body}"
```

### Using HashiCorp Vault Property Function

To use this function, you’ll need to provide credentials for HashiCorp Vault as environment variables:

```bash
export CAMEL_VAULT_HASHICORP_TOKEN=token
export CAMEL_VAULT_HASHICORP_HOST=host
export CAMEL_VAULT_HASHICORP_PORT=port
export CAMEL_VAULT_HASHICORP_SCHEME=http/https
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.hashicorp.token = token
camel.vault.hashicorp.host = host
camel.vault.hashicorp.port = port
camel.vault.hashicorp.scheme = scheme
```

In case the running HashiCorp Vault instance you’re pointing is running on HashiCorp Cloud, the configuration will require two additional parameters:

```bash
export CAMEL_VAULT_HASHICORP_TOKEN=token
export CAMEL_VAULT_HASHICORP_HOST=host
export CAMEL_VAULT_HASHICORP_PORT=port
export CAMEL_VAULT_HASHICORP_SCHEME=http/https
export CAMEL_HASHICORP_VAULT_CLOUD=true
export CAMEL_HASHICORP_VAULT_NAMESPACE=namespace
```

You can also set the same in the `application.properties` file such as:

```properties
camel.vault.hashicorp.token = token
camel.vault.hashicorp.host = host
camel.vault.hashicorp.port = port
camel.vault.hashicorp.scheme = scheme
camel.vault.hashicorp.cloud = true
camel.vault.hashicorp.namespace = namespace
```

This will make the Properties function works even in the HashiCorp Cloud deployment option.

The properties function logs in with a token by default. To log in another way, set the options of [Logging in to HashiCorp Vault](#_logging_in_to_hashicorp_vault) with the `camel.vault.hashicorp` prefix. For example, an application in a Kubernetes pod logs in with the service account of the pod:

```properties
camel.vault.hashicorp.host = vault.example.com
camel.vault.hashicorp.port = 8200
camel.vault.hashicorp.scheme = https
camel.vault.hashicorp.authentication = kubernetes
camel.vault.hashicorp.role = my-application
```

The properties function also reads these options from the environment variables `CAMEL_HASHICORP_VAULT_AUTHENTICATION`, `CAMEL_HASHICORP_VAULT_ROLE_ID`, `CAMEL_HASHICORP_VAULT_SECRET_ID`, `CAMEL_HASHICORP_VAULT_ROLE`, `CAMEL_HASHICORP_VAULT_JWT`, `CAMEL_HASHICORP_VAULT_JWT_FILE` and `CAMEL_HASHICORP_VAULT_AUTH_MOUNT_PATH`, and the settings of [TLS](#_tls) from `CAMEL_HASHICORP_VAULT_TRUST_STORE`, `CAMEL_HASHICORP_VAULT_TRUST_STORE_PASSWORD`, `CAMEL_HASHICORP_VAULT_KEY_STORE` and `CAMEL_HASHICORP_VAULT_KEY_STORE_PASSWORD`. When any of the `CAMEL_HASHICORP_VAULT_*` environment variables is set, the properties function takes all its settings from the environment variables, and none from the `camel.vault.hashicorp` configuration. The secret refresh task logs in the same way as the properties function.

> **Note**
> if you’re running the application on a Kubernetes based cloud platform, you can initialize the environment variables from a Secret or Configmap to enhance security. You can also enhance security by [setting a Secret property placeholder](../../manual/using-propertyplaceholder.html#_resolving_property_placeholders_on_cloud) which will be initialized at application runtime only.

> **Note**
> `camel.vault.hashicorp` configuration only applies to the HashiCorp Vault properties function (E.g when resolving properties). When using the `operation` option to create, get, list secrets etc., you should provide the `host`, `port`, `scheme` (if required) and the options of the login, such as `token`.

At this point, you’ll be able to reference a property in the following way:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{hashicorp:secret:route}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:secret:route}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{hashicorp:secret:route}}"
```

Where route will be the name of the secret stored in the HashiCorp Vault instance, in the 'secret' engine.

> **Note**
> The engine is the part before the first `:`; for a property with a field, only the part before the `#` counts. When the property has no engine, such as `{{hashicorp:route}}` or `{{hashicorp:database#username}}`, the secret is read from the 'secret' engine. Without a field, a default value needs the engine, as in `{{hashicorp:secret:route:default}}`: in `{{hashicorp:route:default}}` the engine would be `route`. With a field it does not, as in `{{hashicorp:database#username:admin}}`.

You could specify a default value in case the secret is not present on HashiCorp Vault instance:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{hashicorp:secret:route:default}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:secret:route:default}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{hashicorp:secret:route:default}}"
```

In this case, if the secret doesn’t exist in the 'secret' engine, the property will fall back to "default" as value.

Also, you are able to get a particular field of the secret, if you have, for example, a secret named database of this form:

```bash
{
  "username": "admin",
  "password": "password123",
  "engine": "postgres",
  "host": "127.0.0.1",
  "port": "3128",
  "dbname": "db"
}
```

You’re able to do get single secret value in your route, in the 'secret' engine, like for example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{hashicorp:secret:database#username}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{hashicorp:secret:database#username}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{hashicorp:secret:database#username}}"
```

Or re-use the property as part of an endpoint.

You could specify a default value in case the particular field of secret is not present on HashiCorp Vault instance, in the 'secret' engine:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{hashicorp:secret:database#username:admin}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{hashicorp:secret:database#username:admin}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{hashicorp:secret:database#username:admin}}"
```

In this case, if the secret doesn’t exist or the secret exists (in the 'secret' engine) but the username field is not part of the secret, the property will fall back to "admin" as value.

There is also the syntax to get a particular version of the secret for both the approach, with field/default value specified or only with secret:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{hashicorp:secret:route@2}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:secret:route@2}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{hashicorp:secret:route@2}}"
```

This approach will return the RAW route secret with version '2', in the 'secret' engine.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{hashicorp:secret:route:default@2}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:secret:route:default@2}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{hashicorp:secret:route:default@2}}"
```

This approach will return the route secret value with version '2' or default value in case the secret doesn’t exist or the version doesn’t exist (in the 'secret' engine).

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{hashicorp:secret:database#username:admin@2}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{hashicorp:secret:database#username:admin@2}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{hashicorp:secret:database#username:admin@2}}"
```

This approach will return the username field of the database secret with version '2' or admin in case the secret doesn’t exist or the version doesn’t exist (in the 'secret' engine).

The only requirement is adding the camel-hashicorp-vault jar to your Camel application.

### Automatic Camel context reloading on Secret Refresh

Being able to reload Camel context on a Secret Refresh could be done by specifying the usual credentials (the same used for HashiCorp Vault Property Function).

With Environment variables:

```bash
export CAMEL_HASHICORP_VAULT_TOKEN=token
export CAMEL_HASHICORP_VAULT_HOST=host
export CAMEL_HASHICORP_VAULT_PORT=port
export CAMEL_HASHICORP_VAULT_SCHEME=http/https
```

or as plain Camel main properties:

```properties
camel.vault.hashicorp.token = token
camel.vault.hashicorp.host = host
camel.vault.hashicorp.port = port
camel.vault.hashicorp.scheme = scheme
```

To enable the automatic refresh, you’ll need additional properties to set:

```properties
camel.vault.hashicorp.refreshEnabled=true
camel.vault.hashicorp.refreshPeriod=60000
camel.vault.hashicorp.secrets=database,api-keys
camel.main.context-reload-enabled = true
```

where `camel.vault.hashicorp.refreshEnabled` will enable the automatic context reload, `camel.vault.hashicorp.refreshPeriod` is the interval of time between two different checks for update events (default 60000ms), and `camel.vault.hashicorp.secrets` is a comma-separated list of secret names (or patterns) to check for updates.

The secret names should use the following format: - `mysecret` or `path/to/secret` - tracks a secret in the default `secret` engine - `myengine:mysecret` or `myengine:path/to/secret` - tracks a secret in the `myengine` engine (use `:` to separate engine from path) - You can use patterns like `database*` to match multiple secrets

Note that `camel.vault.hashicorp.secrets` is not mandatory: if not specified the task responsible for checking updates events will take into account all the properties with a `hashicorp:` prefix. Such a secret is tracked in the engine of the property, in the format above (`hashicorp:myengine:mysecret` is tracked as `myengine:mysecret`, `hashicorp:secret:mysecret` as `mysecret`), and its first check compares the version in Vault with the version that was resolved, so an update made before the first check also triggers a reload.

#### How the Refresh Mechanism Works

Unlike cloud-based secret managers (AWS, GCP, Azure) that provide event-driven notifications, HashiCorp Vault does not have a native event notification system for secret changes. Therefore, this implementation uses a **polling-based approach**:

1.  **Metadata Polling**: The refresh task periodically queries the HashiCorp Vault metadata endpoint (`/v1/<engine>/metadata/<secret>`) for each tracked secret.
    
2.  **Version Tracking**: It compares the `current_version` field to detect changes.
    
3.  **Change Detection**: When a version change is detected, it triggers a Camel context reload.
    
4.  **Efficiency**: Only metadata is queried (not the full secret content), making this approach lightweight.
    

For example, if a secret named `database` is updated in Vault: - The metadata endpoint returns `"current_version": 5` - On the next check, if `current_version` changes to `6`, a reload is triggered - The refresh period (default 60 seconds) determines how quickly changes are detected

This polling approach works with all HashiCorp Vault deployments (on-premise, cloud, enterprise, and open-source) without requiring additional infrastructure.

### Using HashiCorp Vault Property Function in Spring Boot for Early resolving properties

HashiCorp Vault Spring Boot component starter offers the ability to early resolve properties, so the end user could resolve properties directly in the application.properties before both Spring Boot runtime and Camel context will start.

This could be accomplished in the following way. You should specified this property in your application.properties file:

```bash
camel.component.hashicorp-vault.early-resolve-properties=true
```

This will enable the feature so you’ll be able to resolved properties, in your application.properties file, like:

```bash
foo = hashicorp:secret:database/password#string
```
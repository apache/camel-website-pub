# Hashicorp Vault

**Since Camel 3.18**

**Only producer is supported**

The hashicorp-vault component that integrates [Hashicorp Vault](https://www.vaultproject.io/).

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

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Hashicorp Vault component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Hashicorp Vault endpoint is configured using URI syntax:

hashicorp-vault:secretsEngine

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **secretsEngine** (producer) | Vault Name to be used. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (producer) | Hashicorp Vault instance host to be used. |  | String |
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
| **token** (security) | Token to be used. |  | String |

### Using Hashicorp Vault Property Function

To use this function you’ll need to provide credentials for Hashicorp vault as environment variables:

```bash
export $CAMEL_VAULT_HASHICORP_TOKEN=token
export $CAMEL_VAULT_HASHICORP_ENGINE=secretKey
export $CAMEL_VAULT_HASHICORP_HOST=host
export $CAMEL_VAULT_HASHICORP_PORT=port
export $CAMEL_VAULT_HASHICORP_SCHEME=http/https
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.hashicorp.token = token
camel.vault.hashicorp.engine = engine
camel.vault.hashicorp.host = host
camel.vault.hashicorp.port = port
camel.vault.hashicorp.scheme = scheme
```

At this point you’ll be able to reference a property in the following way:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:route}}"/>
    </route>
</camelContext>
```

Where route will be the name of the secret stored in the Hashicorp Vault instance.

You could specify a default value in case the secret is not present on Hashicorp Vault instance:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:route:default}}"/>
    </route>
</camelContext>
```

In this case if the secret doesn’t exist, the property will fallback to "default" as value.

Also you are able to get particular field of the secret, if you have for example a secret named database of this form:

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

You’re able to do get single secret value in your route, like for example:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{hashicorp:database/username}}"/>
    </route>
</camelContext>
```

Or re-use the property as part of an endpoint.

You could specify a default value in case the particular field of secret is not present on Hashicorp Vault instance:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{hashicorp:database/username:admin}}"/>
    </route>
</camelContext>
```

In this case if the secret doesn’t exist or the secret exists, but the username field is not part of the secret, the property will fallback to "admin" as value.

There is also the syntax to get a particular version of the secret for both the approach, with field/default value specified or only with secret:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:route@2}}"/>
    </route>
</camelContext>
```

This approach will return the RAW route secret with version '2'.

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:route:default@2}}"/>
    </route>
</camelContext>
```

This approach will return the route secret value with version '2' or default value in case the secret doesn’t exist or the version doesn’t exist.

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{hashicorp:database/username:admin@2}}"/>
    </route>
</camelContext>
```

This approach will return the username field of the database secret with version '2' or admin in case the secret doesn’t exist or the version doesn’t exist.

For the moment we are not considering the rotation function, if any will be applied, but it is in the work to be done.

The only requirement is adding the camel-hashicorp-vault jar to your Camel application.
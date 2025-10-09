# CyberArk Vault

**Since Camel 4.17**

**Only producer is supported**

The CyberArk Vault component supports [CyberArk Conjur](https://www.cyberark.com/products/conjur/) Vault service.

Prerequisites

You must have access to a CyberArk Conjur instance and have the necessary credentials (username/password, API key, or auth token) to access it.

## URI Format

cyberark-vault:label\[?options\]

Where `label` is a logical name for the endpoint.

You can specify the secret ID either as a URI parameter or via message header:

```java
// Using URI parameter
.to("cyberark-vault:secret?secretId=db/password&...")

// Using message header
.setHeader(CyberArkVaultConstants.SECRET_ID, constant("db/password"))
.to("cyberark-vault:secret?...")
```

You can append query options to the URI in the following format:

`?options=value&option2=value&…​`

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

The CyberArk Vault component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **account** (producer) | **Required** The CyberArk Conjur account name. |  | String |
| **certificatePath** (producer) | Path to the SSL certificate for verification. |  | String |
| **configuration** (producer) | Component configuration. |  | CyberArkVaultConfiguration |
| **conjurClient** (producer) | Reference to a ConjurClient instance in the registry. |  | ConjurClient |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform. It can be getSecret or createSecret.

Enum values:

-   getSecret
    
-   createSecret
    





 | getSecret | CyberArkVaultOperations |
| **secretId** (producer) | The secret ID to retrieve from CyberArk Conjur. |  | String |
| **url** (producer) | **Required** The CyberArk Conjur instance URL. |  | String |
| **verifySsl** (producer) | Whether to verify SSL certificates when connecting to CyberArk Conjur. | true | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **apiKey** (security) | The API key for authentication with CyberArk Conjur. |  | String |
| **authToken** (security) | Pre-authenticated token to use for CyberArk Conjur. |  | String |
| **password** (security) | The password for authentication with CyberArk Conjur. |  | String |
| **username** (security) | The username for authentication with CyberArk Conjur. |  | String |

## Endpoint Options

The CyberArk Vault endpoint is configured using URI syntax:

cyberark-vault:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **account** (producer) | **Required** The CyberArk Conjur account name. |  | String |
| **certificatePath** (producer) | Path to the SSL certificate for verification. |  | String |
| **conjurClient** (producer) | Reference to a ConjurClient instance in the registry. |  | ConjurClient |
| **operation** (producer) | 
The operation to perform. It can be getSecret or createSecret.

Enum values:

-   getSecret
    
-   createSecret
    





 | getSecret | CyberArkVaultOperations |
| **secretId** (producer) | The secret ID to retrieve from CyberArk Conjur. |  | String |
| **url** (producer) | **Required** The CyberArk Conjur instance URL. |  | String |
| **verifySsl** (producer) | Whether to verify SSL certificates when connecting to CyberArk Conjur. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiKey** (security) | The API key for authentication with CyberArk Conjur. |  | String |
| **authToken** (security) | Pre-authenticated token to use for CyberArk Conjur. |  | String |
| **password** (security) | The password for authentication with CyberArk Conjur. |  | String |
| **username** (security) | The username for authentication with CyberArk Conjur. |  | String |

### Authentication Methods

The component supports multiple authentication methods with CyberArk Conjur:

1.  **Username/Password Authentication**: Use username and password to authenticate
    
2.  **API Key Authentication**: Use username and API key (recommended for programmatic access)
    
3.  **Pre-authenticated Token**: Use a pre-obtained authentication token
    

### Using CyberArk Conjur Vault Property Function

To use this function, you’ll need to provide credentials to CyberArk Conjur Service as environment variables:

```bash
export CAMEL_VAULT_CYBERARK_URL=https://conjur.example.com
export CAMEL_VAULT_CYBERARK_ACCOUNT=myaccount
export CAMEL_VAULT_CYBERARK_USERNAME=admin
export CAMEL_VAULT_CYBERARK_PASSWORD=secretpassword
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.cyberark.url=https://conjur.example.com
camel.vault.cyberark.account=myaccount
camel.vault.cyberark.username=admin
camel.vault.cyberark.password=secretpassword
```

> **Note**
> If you’re running the application on a Kubernetes based cloud platform, you can initialize the environment variables from a Secret or ConfigMap to enhance security.

For API key authentication:

```bash
export CAMEL_VAULT_CYBERARK_URL=https://conjur.example.com
export CAMEL_VAULT_CYBERARK_ACCOUNT=myaccount
export CAMEL_VAULT_CYBERARK_USERNAME=host/myapp
export CAMEL_VAULT_CYBERARK_API_KEY=3ahx8dy3...
```

Or in `application.properties`:

```properties
camel.vault.cyberark.url=https://conjur.example.com
camel.vault.cyberark.account=myaccount
camel.vault.cyberark.username=host/myapp
camel.vault.cyberark.apiKey=3ahx8dy3...
```

### Operations

The component supports the following operations:

-   **getSecret** (default) - Retrieve a secret value from CyberArk Conjur
    
-   **createSecret** - Create or update a secret in CyberArk Conjur
    

You can specify the operation either as a URI parameter or via message header:

```java
// Using URI parameter
.to("cyberark-vault:secret?operation=getSecret&secretId=db/password&...")

// Using message header
.setHeader(CyberArkVaultConstants.OPERATION, constant(CyberArkVaultOperations.createSecret))
.to("cyberark-vault:secret?...")
```

### Examples

#### Property Placeholders

At this point, you can access secrets using property placeholders in your routes:

```java
from("direct:start")
    .setHeader("DatabasePassword", simple("{{cyberark:db/password}}"))
    .to("...");
```

You can also specify a default value in case the secret doesn’t exist:

```java
from("direct:start")
    .setHeader("Password", simple("{{cyberark:db/password:defaultPassword}}"))
    .to("...");
```

#### Retrieve JSON Field from Secret

If your secret contains JSON data, you can extract specific fields:

```java
from("direct:start")
    .setHeader("Username", simple("{{cyberark:database#username}}"))
    .setHeader("Password", simple("{{cyberark:database#password}}"))
    .to("...");
```

#### Retrieve a Secret (getSecret)

You can retrieve a secret using the component endpoint:

Using URI parameter:

```java
from("direct:start")
    .to("cyberark-vault:secret?operation=getSecret&secretId=db/password&url=https://conjur.example.com&account=myaccount&username=admin&password=secretpass")
    .log("Retrieved secret: ${body}");
```

Using message header for dynamic secret retrieval:

```java
from("direct:start")
    .setHeader(CyberArkVaultConstants.SECRET_ID, simple("${header.secretName}"))
    .to("cyberark-vault:secret?operation=getSecret&url=https://conjur.example.com&account=myaccount&username=admin&password=secretpass")
    .log("Retrieved secret: ${body}");
```

Retrieve a specific version of a secret:

```java
from("direct:start")
    .setHeader(CyberArkVaultConstants.SECRET_VERSION, constant("3"))
    .to("cyberark-vault:secret?secretId=db/password&url=https://conjur.example.com&account=myaccount&username=admin&apiKey=3ahx8dy3...")
    .log("Retrieved secret version 3: ${body}");
```

#### Create or Update a Secret (createSecret)

To create or update a secret, use the createSecret operation with the secret value in the message body or header:

Using message body:

```java
from("direct:start")
    .setBody(constant("mySecretValue123"))
    .to("cyberark-vault:secret?operation=createSecret&secretId=app/apikey&url=https://conjur.example.com&account=myaccount&username=admin&apiKey=3ahx8dy3...")
    .log("Secret created/updated");
```

Using message header:

```java
from("direct:start")
    .setHeader(CyberArkVaultConstants.SECRET_VALUE, constant("myNewPassword"))
    .setHeader(CyberArkVaultConstants.SECRET_ID, constant("db/password"))
    .to("cyberark-vault:secret?operation=createSecret&url=https://conjur.example.com&account=myaccount&username=admin&apiKey=3ahx8dy3...")
    .log("Secret created/updated");
```

Dynamic secret creation:

```java
from("direct:start")
    .setBody(simple("${header.newSecretValue}"))
    .setHeader(CyberArkVaultConstants.SECRET_ID, simple("${header.secretPath}"))
    .to("cyberark-vault:secret?operation=createSecret&url=https://conjur.example.com&account=myaccount&username=admin&apiKey=3ahx8dy3...")
    .log("Secret ${header.secretPath} created/updated");
```

### SSL Certificate Verification

By default, SSL certificate verification is enabled. You can disable it for testing purposes (not recommended for production):

```properties
camel.vault.cyberark.verifySsl=false
```

Or provide a custom certificate path:

```properties
camel.vault.cyberark.certificatePath=/path/to/cert.pem
```

### Setting Up CyberArk Conjur for Testing

Before you can use the component or run integration tests, you need to set up a CyberArk Conjur instance and configure policies to define which secrets (variables) are available.

#### Step 1: Start Conjur with Docker

The easiest way to get started is using the official [Conjur Quickstart](https://github.com/cyberark/conjur-quickstart):

```bash
# Clone the quickstart repository
git clone https://github.com/cyberark/conjur-quickstart.git
cd conjur-quickstart

# Start Conjur and database
docker-compose up -d

# Wait for services to be ready
sleep 15

# The admin API key will be displayed in the logs
docker-compose logs conjur_server | grep "admin API key"
```

Default connection details: - **URL**: `[http://localhost:8080](http://localhost:8080)` - **Account**: `myConjurAccount` - **Username**: `admin` - **API Key**: Check the container logs (see command above)

#### Step 2: Load Conjur Policy

CyberArk Conjur requires you to define variables in a **policy file** before you can set their values. Here’s how to create and load a policy:

**Automated Script:**

You can also use this automated script to load the policy:

```bash
#!/bin/bash

# Replace with your actual API key from the Conjur logs
API_KEY="your-api-key-here"

# Create policy file
cat > test-secrets.yaml <<'EOF'
- !variable database
- !variable simple-secret
- !variable app/config
- !variable test/secret
- !variable production/database
- !variable api/credentials
- !variable db/primary
- !variable db/replica
- !variable cache/redis
EOF

# Copy to client container
echo "Copying policy to conjur_client..."
docker cp test-secrets.yaml conjur_client:/tmp/test-secrets.yaml

# Initialize Conjur CLI
echo "Initializing Conjur CLI..."
docker exec conjur_client conjur init -u http://conjur_server -a myConjurAccount --force

# Login
echo "Logging in..."
echo "$API_KEY" | docker exec -i conjur_client conjur login -i admin

# Load policy
echo "Loading policy..."
docker exec conjur_client conjur policy load -b root -f /tmp/test-secrets.yaml

if [ $? -eq 0 ]; then
    echo "✅ Policy loaded successfully!"
else
    echo "❌ Policy load failed"
    exit 1
fi

# Clean up
rm test-secrets.yaml
```

Save as `load-policy.sh`, make it executable (`chmod +x load-policy.sh`), update the API\_KEY, and run it.

### Running Integration Tests

The component includes integration tests that require a running CyberArk Conjur instance. The tests are **disabled by default** and only run when specific system properties are provided.

#### Prerequisites

1.  A running CyberArk Conjur instance (see "Setting Up CyberArk Conjur for Testing" above)
    
2.  Conjur policies loaded with the required variables (see Step 2 above)
    
3.  Valid Conjur credentials (URL, account, username, API key)
    

#### Required System Properties

The integration tests require these system properties:

-   `camel.cyberark.url` - CyberArk Conjur URL (e.g., `[http://localhost:8080](http://localhost:8080)`)
    
-   `camel.cyberark.account` - Conjur account name (e.g., `myConjurAccount`)
    
-   `camel.cyberark.username` - Admin username (e.g., `admin`)
    
-   `camel.cyberark.apiKey` - Admin API key
    

#### Running All Integration Tests

```bash
cd components/camel-cyberark-vault

mvn clean verify \
  -Dcamel.cyberark.url=http://localhost:8080 \
  -Dcamel.cyberark.account=myConjurAccount \
  -Dcamel.cyberark.username=admin \
  -Dcamel.cyberark.apiKey=YOUR_API_KEY_HERE
```

Replace `YOUR_API_KEY_HERE` with the actual API key from your Conjur instance.

#### Running Specific Test Classes

```bash
# Run properties function tests
mvn clean verify -Dit.test=CyberArkVaultPropertiesSourceIT \
  -Dcamel.cyberark.url=http://localhost:8080 \
  -Dcamel.cyberark.account=myConjurAccount \
  -Dcamel.cyberark.username=admin \
  -Dcamel.cyberark.apiKey=YOUR_API_KEY_HERE

# Run producer endpoint tests
mvn clean verify -Dit.test=CyberArkVaultProducerIT \
  -Dcamel.cyberark.url=http://localhost:8080 \
  -Dcamel.cyberark.account=myConjurAccount \
  -Dcamel.cyberark.username=admin \
  -Dcamel.cyberark.apiKey=YOUR_API_KEY_HERE
```
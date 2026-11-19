# ![snowflake sink](_images/kamelets/snowflake-sink.svg) Snowflake Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Runs an SQL statement, such as an INSERT, in a Snowflake database for each message, with values taken from the fields of the JSON object in the body.

Use it to store records from another system as rows of a table, such as each order that arrives on a Kafka topic, or to update or delete rows. To read rows, use `snowflake-source`.

Input: the body is one JSON object, as text, such as `{"username":"oscerd","city":"Rome"}`. In `query`, write `:#username` where the value of the field `username` goes. When the object has no field of that name, the header of that name is used instead. Fields that `query` does not name are ignored.

Output: the body afterwards is the JSON object as a Map, and the `CamelSqlUpdateCount` header holds the number of rows the statement changed. When `query` is a SELECT, the body is instead a List of the rows found, each a Map, and the `CamelSqlRowCount` header holds their number.

Good to know: a message fails when its body is not a JSON object (a JSON array or plain text, for example), or when it has no value for a parameter of `query`. The values are sent to the database apart from the SQL text, so the content of a message cannot change the statement. Do not write `?` in `query`, not even in a quoted string: the Kamelet then fails to start. Log in with `password`, or with a key pair in `privateKey` or `privateKeyFile`: a Snowflake user of type SERVICE, meant for applications, cannot log in with a password. When a key is set, the password is not used. `warehouse`, `schema` and `role` choose what the session uses; when they are not set, the defaults of the user apply, and a user with no default warehouse cannot run a query that needs one. Each message logs in to Snowflake anew, as the Kamelet keeps no connection open between messages.

## Configuration Options

The following table summarizes the configuration options available for the `snowflake-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **instanceUrl** | Account Host Name | **Required** The host name of your Snowflake account, without `https://`: your account identifier followed by `.snowflakecomputing.com`, as in the address you open Snowflake at. | string |  | myorg-myaccount.snowflakecomputing.com |
| **query** | Query | **Required** The SQL statement to run for each message, such as an INSERT, UPDATE or DELETE. Write `:#name` where the value of the field `name` of the JSON body goes. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **username** | Username | **Required** The Snowflake user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **databaseName** | Database Name | The Snowflake database that holds the tables `query` names. | string |  | SHOP |
| **password** | Password | The password of the Snowflake user `username`. Leave it empty to log in with a key pair instead, set in `privateKey` or `privateKeyFile`; when a key is set, the password is not used. A Snowflake user of type SERVICE cannot log in with a password, and Snowflake is phasing out sign-in with a password alone for the other users too. With neither a password nor a key, every connection fails with `Missing password`. | string |  |  |
| **privateKey** | Private Key | The private key to log in with instead of a password: the key file in PEM format, encoded in base64 on a single line, such as the output of `base64 -w0 rsa_key.p8`. The PEM text itself, which starts with `-----BEGIN`, is not accepted. The matching public key must be set on the user with `ALTER USER …​ SET RSA_PUBLIC_KEY`. Set this or `privateKeyFile`, not both: with both, every connection fails. | string |  |  |
| **privateKeyFile** | Private Key File | The path of the private key file to log in with instead of a password, in PEM format, such as `rsa_key.p8` made as the Snowflake guide to key-pair authentication shows. In Kubernetes, mount the Secret that holds the key as a file. The matching public key must be set on the user with `ALTER USER …​ SET RSA_PUBLIC_KEY`. A path that does not exist makes every connection fail with `Invalid parameter value null`. | string |  | /etc/snowflake/rsa\_key.p8 |
| **privateKeyPassphrase** | Private Key Passphrase | The passphrase of the key in `privateKey` or `privateKeyFile`, when the key is encrypted: its PEM text then starts with `-----BEGIN ENCRYPTED PRIVATE KEY-----`. Without it, or with a wrong one, every connection fails. | string |  |  |
| **role** | Role | The Snowflake role to run the statements as, which must be granted to the user `username`. When it is not set, the default role of the user is used, as set with `ALTER USER …​ SET DEFAULT_ROLE`. | string |  | LOADER |
| **schema** | Schema | The schema of `databaseName` that holds the tables `query` names, such as `PUBLIC`. When it is not set, the default of the user applies. A table of another schema can still be named in full in `query`, as `SCHEMA.TABLE`. | string |  | SALES |
| **warehouse** | Warehouse | The Snowflake virtual warehouse that runs the statements. When it is not set, the default warehouse of the user `username` is used, as set with `ALTER USER …​ SET DEFAULT_WAREHOUSE`. With neither, a statement that needs a warehouse, such as an INSERT, fails. | string |  | COMPUTE\_WH |

## Dependencies

At runtime, the `snowflake-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:net.snowflake:snowflake-jdbc:4.3.4
    
-   mvn:org.apache.commons:commons-dbcp2:2.14.0
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:snowflake-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Snowflake Sink Kamelet Description

### Cloud Data Warehouse

This Kamelet integrates with Snowflake, a cloud-based data warehouse platform that provides scalable data storage and analytics capabilities. Snowflake is designed for modern data architecture and cloud-native applications.

### JDBC Connectivity

Uses the Snowflake JDBC driver for native connectivity to Snowflake instances. The driver provides optimized performance and supports Snowflake-specific features and data types.

### Instance Configuration

Requires configuration of the Snowflake instance URL (e.g., `instance.snowflakecomputing.com`) which uniquely identifies your Snowflake account and region.

### Authentication Methods

The Kamelet logs in to Snowflake as the Snowflake user `username`, either with `password` or with a key pair. A Snowflake user of type SERVICE, meant for applications, cannot log in with a password, and Snowflake is phasing out sign-in with a password alone for the other users too, so use a key pair for an integration. When a key is set, the password is not used.

-   `privateKey` is the private key file in PEM format, encoded in base64 on a single line, such as the output of `base64 -w0 rsa_key.p8`.
    
-   `privateKeyFile` is instead the path of that file, such as a Kubernetes Secret mounted as a file. Set one of `privateKey` and `privateKeyFile`, not both.
    
-   `privateKeyPassphrase` is the passphrase of the key, when it is encrypted.
    

Snowflake’s guide to [key-pair authentication](https://docs.snowflake.com/en/user-guide/key-pair-auth) shows how to make the key pair, such as with `openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt`, and how to set the public key on the user with `ALTER USER …​ SET RSA_PUBLIC_KEY`.

### Warehouse, Schema and Role

The Kamelet sends these with each login, so the session starts with them:

-   `warehouse`: the virtual warehouse that runs the statements, such as `COMPUTE_WH`.
    
-   `schema`: the schema of `databaseName` that holds the tables, such as `SALES`.
    
-   `role`: the role to run the statements as. It must be granted to the user.
    

When one is not set, the default of the user applies, as set with `ALTER USER …​ SET DEFAULT_WAREHOUSE`, `DEFAULT_NAMESPACE` or `DEFAULT_ROLE`. A user with no default warehouse needs `warehouse`, since an INSERT, an UPDATE or a DELETE needs a running warehouse.

```yaml
- to:
    uri: "kamelet:snowflake-sink"
    parameters:
      instanceUrl: "myorg-myaccount.snowflakecomputing.com"
      username: "ORDERS_SERVICE"
      privateKey: "{{snowflake.private.key}}"
      databaseName: "SHOP"
      schema: "SALES"
      warehouse: "LOAD_WH"
      role: "ORDERS_LOADER"
      query: "INSERT INTO orders (id,customer) VALUES (:#id,:#customer)"
```

### Connections

The Kamelet keeps no connection to Snowflake open between messages: each message logs in again, and starts a new session.

### Data Processing

Processes JSON input data through unmarshalling before executing SQL queries. This enables seamless integration with JSON-based data pipelines and streaming applications.

### Query Execution

Supports parameterized SQL queries using named parameters that map to JSON data fields. This ensures secure and efficient data insertion into Snowflake tables.

### Cloud-Native Features

Snowflake’s cloud-native architecture provides automatic scaling, performance optimization, and enterprise-grade security, making this Kamelet suitable for large-scale data operations.

### Example with a Key Pair

The route below stores each order posted to a webhook as a row, logged in with a key pair. The key, encoded in base64, comes from a property, such as one set from a Kubernetes Secret.

```yaml
- route:
    from:
      uri: "kamelet:webhook-source"
      parameters:
        subpath: "orders"
      steps:
        - to:
            uri: "kamelet:snowflake-sink"
            parameters:
              instanceUrl: "myorg-myaccount.snowflakecomputing.com"
              username: "ORDERS_SERVICE"
              privateKey: "{{snowflake.private.key}}"
              databaseName: "SHOP"
              query: "INSERT INTO orders (id,customer) VALUES (:#id,:#customer)"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/snowflake-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/snowflake-sink.kamelet.yaml)
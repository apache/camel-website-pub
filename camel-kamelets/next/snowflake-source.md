# ![snowflake source](_images/kamelets/snowflake-source.svg) Snowflake Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Runs an SQL query in a Snowflake database again and again, and sends each row it returns as a message, as a JSON object.

Use it to pick up the rows that another application adds to a table, such as new orders or events, and pass them on to another system. To write rows, use `snowflake-sink`.

Output: the body is one row as JSON text in bytes, an object with the column names as keys, such as `{"id":1,"username":"oscerd","city":"Rome"}`. The `Content-Type` header is `application/json`.

Good to know: the query runs again `delay` milliseconds after the previous run, so the same rows are sent again and again, unless `consumedQuery` marks or deletes each row once it is sent and `query` leaves such rows out: for example `SELECT * FROM accounts WHERE processed = false` with `UPDATE accounts SET processed = true WHERE id = :#id`. When the next step fails for a row, `consumedQuery` is not run for it, and the row is read again. A query that finds no rows sends nothing. `query` cannot contain `?`. The format of date and time columns in the JSON depends on the Camel version. Log in with `password`, or with a key pair in `privateKey` or `privateKeyFile`: a Snowflake user of type SERVICE, meant for applications, cannot log in with a password. When a key is set, the password is not used. `warehouse`, `schema` and `role` choose what the session uses; when they are not set, the defaults of the user apply, and a user with no default warehouse cannot run a query that needs one. Each poll logs in to Snowflake anew, as the Kamelet keeps no connection open between polls.

## Configuration Options

The following table summarizes the configuration options available for the `snowflake-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **instanceUrl** | Account Host Name | **Required** The host name of your Snowflake account, without `https://`: your account identifier followed by `.snowflakecomputing.com`, as in the address you open Snowflake at. | string |  | myorg-myaccount.snowflakecomputing.com |
| **query** | Query | **Required** The SQL query to run on each poll, usually a SELECT. Each row it returns becomes a message. | string |  | SELECT \* FROM accounts WHERE processed = false |
| **username** | Username | **Required** The Snowflake user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **consumedQuery** | Consumed Query | An SQL statement to run after each row has been sent on, to mark the row as read or to delete it, so that `query` does not return it again. Write `:#column` where the value of a column of that row goes, such as `:#id`. When it is not set, nothing is changed, and the same rows are read on every poll. | string |  | UPDATE accounts SET processed = true WHERE id = :#id |
| **databaseName** | Database Name | The Snowflake database that holds the tables `query` names. | string |  | SHOP |
| **delay** | Delay | How long to wait after one run of `query` before the next, in milliseconds. | integer | 500 |  |
| **password** | Password | The password of the Snowflake user `username`. Leave it empty to log in with a key pair instead, set in `privateKey` or `privateKeyFile`; when a key is set, the password is not used. A Snowflake user of type SERVICE cannot log in with a password, and Snowflake is phasing out sign-in with a password alone for the other users too. With neither a password nor a key, every connection fails with `Missing password`. | string |  |  |
| **privateKey** | Private Key | The private key to log in with instead of a password: the key file in PEM format, encoded in base64 on a single line, such as the output of `base64 -w0 rsa_key.p8`. The PEM text itself, which starts with `-----BEGIN`, is not accepted. The matching public key must be set on the user with `ALTER USER …​ SET RSA_PUBLIC_KEY`. Set this or `privateKeyFile`, not both: with both, every connection fails. | string |  |  |
| **privateKeyFile** | Private Key File | The path of the private key file to log in with instead of a password, in PEM format, such as `rsa_key.p8` made as the Snowflake guide to key-pair authentication shows. In Kubernetes, mount the Secret that holds the key as a file. The matching public key must be set on the user with `ALTER USER …​ SET RSA_PUBLIC_KEY`. A path that does not exist makes every connection fail with `Invalid parameter value null`. | string |  | /etc/snowflake/rsa\_key.p8 |
| **privateKeyPassphrase** | Private Key Passphrase | The passphrase of the key in `privateKey` or `privateKeyFile`, when the key is encrypted: its PEM text then starts with `-----BEGIN ENCRYPTED PRIVATE KEY-----`. Without it, or with a wrong one, every connection fails. | string |  |  |
| **role** | Role | The Snowflake role to run the queries as, which must be granted to the user `username`. When it is not set, the default role of the user is used, as set with `ALTER USER …​ SET DEFAULT_ROLE`. | string |  | READER |
| **schema** | Schema | The schema of `databaseName` that holds the tables `query` names, such as `PUBLIC`. When it is not set, the default of the user applies. A table of another schema can still be named in full in `query`, as `SCHEMA.TABLE`. | string |  | SALES |
| **warehouse** | Warehouse | The Snowflake virtual warehouse that runs the queries. When it is not set, the default warehouse of the user `username` is used, as set with `ALTER USER …​ SET DEFAULT_WAREHOUSE`. With neither, a query that needs a warehouse fails. | string |  | COMPUTE\_WH |

## Dependencies

At runtime, the `snowflake-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:snowflake-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Snowflake Source Kamelet Description

### Authentication methods

This Kamelet logs in to Snowflake as the Snowflake user `username`, either with `password` or with a key pair. A Snowflake user of type SERVICE, meant for applications, cannot log in with a password, and Snowflake is phasing out sign-in with a password alone for the other users too, so use a key pair for an integration. When a key is set, the password is not used.

-   `privateKey` is the private key file in PEM format, encoded in base64 on a single line, such as the output of `base64 -w0 rsa_key.p8`.
    
-   `privateKeyFile` is instead the path of that file, such as a Kubernetes Secret mounted as a file. Set one of `privateKey` and `privateKeyFile`, not both.
    
-   `privateKeyPassphrase` is the passphrase of the key, when it is encrypted.
    

Snowflake’s guide to [key-pair authentication](https://docs.snowflake.com/en/user-guide/key-pair-auth) shows how to make the key pair, such as with `openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt`, and how to set the public key on the user with `ALTER USER …​ SET RSA_PUBLIC_KEY`.

### Output format

The Kamelet runs `query` again every `delay` milliseconds, and sends each row it returns as a message: a JSON object with the column names as keys. Without `consumedQuery`, the same rows are read again on every run.

### Configuration

The Kamelet requires database connection parameters:

-   `instanceUrl`: the host name of your Snowflake account, such as `myorg-myaccount.snowflakecomputing.com`
    
-   `databaseName` (optional): the Snowflake database that holds the tables
    
-   `schema`, `warehouse` and `role` (optional): the schema of `databaseName` that holds the tables, the virtual warehouse that runs the queries, and the role to run them as. See below.
    
-   `username`: the Snowflake user to log in as, with `password`, or with a key pair in `privateKey` or `privateKeyFile`
    
-   `query`: the SQL query to run, such as `SELECT * FROM accounts WHERE processed = false`
    
-   `consumedQuery` (optional): an SQL statement run for each row once it is sent, to mark the row as read or delete it, such as `UPDATE accounts SET processed = true WHERE id = :#id`
    

### Usage example

The route below logs each account that is not processed yet, and marks it as processed.

```yaml
- route:
    from:
      uri: "kamelet:snowflake-source"
      parameters:
        instanceUrl: "myorg-myaccount.snowflakecomputing.com"
        username: "dbuser"
        password: "dbpass"
        databaseName: "SHOP"
        query: "SELECT * FROM accounts WHERE processed = false"
        consumedQuery: "UPDATE accounts SET processed = true WHERE id = :#id"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Warehouse, Schema and Role

The Kamelet sends these with each login, so the session starts with them:

-   `warehouse`: the virtual warehouse that runs the queries, such as `COMPUTE_WH`.
    
-   `schema`: the schema of `databaseName` that holds the tables, such as `SALES`.
    
-   `role`: the role to run the queries as. It must be granted to the user.
    

When one is not set, the default of the user applies, as set with `ALTER USER …​ SET DEFAULT_WAREHOUSE`, `DEFAULT_NAMESPACE` or `DEFAULT_ROLE`. A user with no default warehouse needs `warehouse` for a query that reads a table.

```yaml
- route:
    from:
      uri: "kamelet:snowflake-source"
      parameters:
        instanceUrl: "myorg-myaccount.snowflakecomputing.com"
        username: "ORDERS_SERVICE"
        privateKeyFile: "/etc/snowflake/rsa_key.p8"
        databaseName: "SHOP"
        schema: "SALES"
        warehouse: "REPORTING_WH"
        role: "ORDERS_READER"
        query: "SELECT * FROM accounts WHERE processed = false"
        consumedQuery: "UPDATE accounts SET processed = true WHERE id = :#id"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Connections

The Kamelet keeps no connection to Snowflake open between polls: each poll logs in again, and starts a new session.

### Example with a Key Pair

The same route, logged in with a key pair. The key file comes from a Kubernetes Secret mounted at `/etc/snowflake`, and the passphrase of the key from a property.

```yaml
- route:
    from:
      uri: "kamelet:snowflake-source"
      parameters:
        instanceUrl: "myorg-myaccount.snowflakecomputing.com"
        username: "ORDERS_SERVICE"
        privateKeyFile: "/etc/snowflake/rsa_key.p8"
        privateKeyPassphrase: "{{snowflake.key.passphrase}}"
        databaseName: "SHOP"
        query: "SELECT * FROM accounts WHERE processed = false"
        consumedQuery: "UPDATE accounts SET processed = true WHERE id = :#id"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/snowflake-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/snowflake-source.kamelet.yaml)
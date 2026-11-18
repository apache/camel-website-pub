# ![postgresql sink](_images/kamelets/postgresql-sink.svg) PostgreSQL Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL statement, such as an INSERT, in a PostgreSQL database for each message, with values taken from the fields of the JSON object in the body.

Use it to store records from another system as rows of a table, such as each order that arrives on a Kafka topic, or to update or delete rows. To read rows, use `postgresql-source`.

Input: the body is one JSON object, as text, such as `{"username":"oscerd","city":"Rome"}`. In `query`, write `:#username` where the value of the field `username` goes. When the object has no field of that name, the header of that name is used instead. Fields that `query` does not name are ignored.

Output: the body afterwards is the JSON object as a Map, and the `CamelSqlUpdateCount` header holds the number of rows the statement changed. When `query` is a SELECT, the body is instead a List of the rows found, each a Map, and the `CamelSqlRowCount` header holds their number.

Good to know: a message fails when its body is not a JSON object (a JSON array or plain text, for example), or when it has no value for a parameter of `query`. The values are sent to the database apart from the SQL text, so the content of a message cannot change the statement. Do not write `?` in `query`, not even in a quoted string: the Kamelet then fails to start. Without `connectionProperties`, the connection uses TLS only when the server offers it, and the certificate of the server is not checked: set `sslmode=require` or `sslmode=verify-full` in `connectionProperties` to insist on TLS.

## Configuration Options

The following table summarizes the configuration options available for the `postgresql-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database to connect to on the PostgreSQL server. | string |  | shop |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **query** | Query | **Required** The SQL statement to run for each message, such as an INSERT, UPDATE or DELETE. Write `:#name` where the value of the field `name` of the JSON body goes. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The host name or IP address of the PostgreSQL server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The database user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **connectionProperties** | Connection Properties | Extra settings for the PostgreSQL JDBC driver, as `name=value` pairs separated by `;`, such as `sslmode=require;connectTimeout=10`. Use it for TLS: `sslmode=require` refuses a server that does not offer TLS, and `sslmode=verify-full` also checks the certificate of the server against the CA certificate in the file named by `sslrootcert`. When it is not set, the driver uses TLS when the server offers it, without checking the certificate. The value is not hidden like a password, and it can show in the log when the integration starts, so do not put a password in it. | string |  | sslmode=require |
| **serverPort** | Server Port | The port the PostgreSQL server listens on. PostgreSQL uses 5432 unless it was set up otherwise. | string | 5432 |  |

## Dependencies

At runtime, the `postgresql-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:org.postgresql:postgresql:42.7.14
    
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
            uri: "kamelet:postgresql-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## PostgreSQL Sink Kamelet Description

### Input Format

This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

### Query Example

Here is an example query:

```sql
INSERT INTO accounts (username,city) VALUES (:#username,:#city)
```

Here is example input for the example query:

```json
{ "username":"oscerd", "city":"Rome"}
```

### Authentication

The Kamelet requires username and password authentication to connect to the PostgreSQL database.

### Connecting with TLS

Set `connectionProperties` to pass settings to the PostgreSQL JDBC driver, as `name=value` pairs separated by `;`. Without it, the driver uses TLS only when the server offers it, and does not check the certificate of the server.

-   `sslmode=require`: always use TLS, and fail when the server does not offer it.
    
-   `sslmode=verify-full;sslrootcert=/etc/certs/root.crt`: also check the certificate of the server against the CA certificate in that file.
    

```yaml
connectionProperties: "sslmode=require"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/postgresql-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/postgresql-sink.kamelet.yaml)
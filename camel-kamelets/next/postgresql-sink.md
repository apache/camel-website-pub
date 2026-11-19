# ![postgresql sink](_images/kamelets/postgresql-sink.svg) PostgreSQL Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL statement, such as an INSERT, in a PostgreSQL database for each message, with values taken from the fields of the JSON object in the body.

Use it to store records from another system as rows of a table, such as each order that arrives on a Kafka topic, or to update or delete rows. To read rows, use `postgresql-source`.

Input: the body is one JSON object, as text, such as `{"username":"oscerd","city":"Rome"}`. In `query`, write `:#username` where the value of the field `username` goes. When the object has no field of that name, the header of that name is used instead. Fields that `query` does not name are ignored. When `batch` is true, the body can also be a JSON array of such objects, and `query` runs once for each of them.

Output: the body afterwards is the JSON object as a Map, and the `CamelSqlUpdateCount` header holds the number of rows the statement changed. For a JSON array with `batch`, the body is a List of Maps, and the header holds the total for all of them. When `query` is a SELECT, the body is instead a List of the rows found, each a Map, and the `CamelSqlRowCount` header holds their number.

Good to know: a message fails when its body is not a JSON object (plain text, for example, or a JSON array when `batch` is not true), or when it has no value for a parameter of `query`. With `batch`, all the rows of one message are written in one transaction: when one of them fails, none is written. The values are sent to the database apart from the SQL text, so the content of a message cannot change the statement. Do not write `?` in `query`, not even in a quoted string: the Kamelet then fails to start. Without `connectionProperties`, the connection uses TLS only when the server offers it, and the certificate of the server is not checked: set `sslmode=require` or `sslmode=verify-full` in `connectionProperties` to insist on TLS.

## Configuration Options

The following table summarizes the configuration options available for the `postgresql-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database to connect to on the PostgreSQL server. | string |  | shop |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **query** | Query | **Required** The SQL statement to run for each message, such as an INSERT, UPDATE or DELETE. Write `:#name` where the value of the field `name` of the JSON body goes. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The host name or IP address of the PostgreSQL server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The database user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **batch** | Batch | Whether the body can be a JSON array of objects, such as `[\{"username":"oscerd","city":"Rome"},\{"username":"ann","city":"Oslo"}]`, to write several rows from one message. `query` runs once for each object, and all of them are written in one database transaction: when one of them fails, none is written. A single JSON object still works. When it is not set, the body must be one JSON object. | boolean |  |  |
| **connectionProperties** | Connection Properties | Extra settings for the PostgreSQL JDBC driver, as `name=value` pairs separated by `;`, such as `sslmode=require;connectTimeout=10`. Use it for TLS: `sslmode=require` refuses a server that does not offer TLS, and `sslmode=verify-full` also checks the certificate of the server against the CA certificate in the file named by `sslrootcert`. When it is not set, the driver uses TLS when the server offers it, without checking the certificate. The value is not hidden like a password, and it can show in the log when the integration starts, so do not put a password in it. | string |  | sslmode=require |
| **maxIdle** | Max Idle Connections | The most unused connections to keep open for later. A connection that is given back when this many are unused already is closed. When it is not set, up to 8 are kept open. | integer |  | 2 |
| **maxTotal** | Max Connections | The most connections to the database that the Kamelet opens at the same time. When all of them are in use, the next message waits for one to be free, as long as `maxWaitMillis` allows. When it is not set, the limit is 8. | integer |  | 20 |
| **maxWaitMillis** | Max Wait | How long to wait for a free connection when `maxTotal` connections are in use, in milliseconds. After that, the message fails. When it is not set, it waits as long as it takes. | integer |  | 5000 |
| **serverPort** | Server Port | The port the PostgreSQL server listens on. PostgreSQL uses 5432 unless it was set up otherwise. | string | 5432 |  |

## Dependencies

At runtime, the `postgresql-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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

### Writing Several Rows from One Message

With `batch` set to true, the body can be a JSON array of objects. `query` runs once for each object, and all of them are written in one database transaction: when one of them fails, none is written. The `CamelSqlUpdateCount` header then holds the number of rows written for the whole message. A single JSON object still works.

```yaml
- route:
    from:
      uri: "timer:accounts?repeatCount=1"
      steps:
        - setBody:
            constant: '[{"username":"oscerd","city":"Rome"},{"username":"ann","city":"Oslo"}]'
        - to:
            uri: "kamelet:postgresql-sink"
            parameters:
              serverName: "db.example.com"
              username: "dbuser"
              password: "dbpass"
              databaseName: "shop"
              query: "INSERT INTO accounts (username,city) VALUES (:#username,:#city)"
              batch: true
```

### Connection Pool

The Kamelet keeps a pool of connections to the database:

-   `maxTotal`: the most connections it opens at the same time, 8 when not set.
    
-   `maxIdle`: the most unused connections it keeps open, 8 when not set.
    
-   `maxWaitMillis`: how long a message waits for a free connection when `maxTotal` are in use, in milliseconds, before it fails. When not set, it waits as long as it takes.
    

```yaml
maxTotal: 4
maxIdle: 2
maxWaitMillis: 5000
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/postgresql-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/postgresql-sink.kamelet.yaml)
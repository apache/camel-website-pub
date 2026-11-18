# ![aws redshift sink](_images/kamelets/aws-redshift-sink.svg) AWS Redshift Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL statement, such as an INSERT, on an Amazon Redshift database for each message, with the values taken from the JSON body.

Use it to load events or records, such as orders or page views, into a table of a Redshift data warehouse, or to update rows when something changes. To read rows from Redshift, use `aws-redshift-source`.

Input: the body is a JSON object, as JSON text, such as `{"username":"alice","city":"Rome"}`. Each `:#name` in `query` takes the value of the field with that name, else of the header with that name. The statement runs once per message.

Output: when it is used inside a route, the body afterwards is the JSON object parsed as a Map, and the `CamelSqlUpdateCount` header holds the number of rows changed.

Good to know: a body that is not a JSON object fails, and so does a body that lacks a field named in `query` when no header has that name either. It logs in with a database user and password, not with AWS keys, and connects with the Amazon Redshift JDBC driver, which uses TLS by default. Other settings of the driver go in `connectionProperties`.

## Configuration Options

The following table summarizes the configuration options available for the `aws-redshift-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database in the cluster, such as `dev`, the database a new cluster has. | string |  | dev |
| **password** | Password | **Required** The password of `username`, set when the cluster or the user was created. | string |  |  |
| **query** | Query | **Required** The SQL statement to run for each message. Write `:#name` where the value of the field `name` of the body goes; the values are passed as parameters, never pasted into the SQL text. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The host name of the Redshift cluster: its endpoint, as shown in the Redshift console, without the port and the database name. | string |  | my-cluster.abc123xyz789.eu-west-1.redshift.amazonaws.com |
| **username** | Username | **Required** The database user to log in as, such as the admin user of the cluster. This is a user of the database, not an AWS access key. | string |  |  |
| **connectionProperties** | Connection Properties | Extra settings for the Amazon Redshift JDBC driver, as `name=value` pairs separated by `;`, such as `loginTimeout=30`. When it is not set, the driver connects with TLS, as it does by default. The value is not hidden like a password, and it can show in the log when the integration starts, so do not put a password in it. | string |  | loginTimeout=30 |
| **serverPort** | Server Port | The port of the cluster. Redshift uses 5439 unless it was changed when the cluster was created. | string | 5439 |  |

## Dependencies

At runtime, the `aws-redshift-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:com.amazon.redshift:redshift-jdbc42:2.3.0
    
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
            uri: "kamelet:aws-redshift-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Redshift Sink Kamelet Description

### Authentication

This Kamelet logs in to the Redshift database with a database user and password (`username` and `password`), not with AWS access keys. It connects with the Amazon Redshift JDBC driver, which uses TLS by default.

### Expected Data format for sink

The Kamelet expects a JSON object, as JSON text. Each `:#name` in the query takes the value of the JSON field with that name, or else of the header with that name. For example, here is a query:

```sql
INSERT INTO accounts (username,city) VALUES (:#username,:#city)
```

Here is example input for the example query:

```json
{ "username":"oscerd", "city":"Rome"}
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-redshift-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-redshift-sink.kamelet.yaml)
# ![aws redshift source](_images/kamelets/aws-redshift-source.svg) AWS Redshift Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL query on an Amazon Redshift database at regular intervals, and sends each row of the result as a message.

Use it to pick up records from a Redshift data warehouse, such as new orders or daily figures, and pass them on to another system. To write to Redshift, use `aws-redshift-sink`.

Output: one message per row. The body is the row as a JSON object, in JSON text, with the column names as field names, such as `{"id":1,"username":"alice","city":"Rome"}`. The `Content-Type` header is `application/json`.

Good to know: the query runs again every `delay` milliseconds, and returns the same rows each time unless they change; set `consumedQuery` to mark or delete each row once it has been sent. It logs in with a database user and password, not with AWS keys, and connects with the Amazon Redshift JDBC driver, which uses TLS by default. Other settings of the driver go in `connectionProperties`.

## Configuration Options

The following table summarizes the configuration options available for the `aws-redshift-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database in the cluster, such as `dev`, the database a new cluster has. | string |  | dev |
| **password** | Password | **Required** The password of `username`, set when the cluster or the user was created. | string |  |  |
| **query** | Query | **Required** The SQL query to run at each poll. Each row of the result becomes a message. | string |  | SELECT \* FROM orders WHERE exported = false |
| **serverName** | Server Name | **Required** The host name of the Redshift cluster: its endpoint, as shown in the Redshift console, without the port and the database name. | string |  | my-cluster.abc123xyz789.eu-west-1.redshift.amazonaws.com |
| **username** | Username | **Required** The database user to log in as, such as the admin user of the cluster. This is a user of the database, not an AWS access key. | string |  |  |
| **connectionProperties** | Connection Properties | Extra settings for the Amazon Redshift JDBC driver, as `name=value` pairs separated by `;`, such as `loginTimeout=30`. When it is not set, the driver connects with TLS, as it does by default. The value is not hidden like a password, and it can show in the log when the integration starts, so do not put a password in it. | string |  | loginTimeout=30 |
| **consumedQuery** | Consumed Query | An SQL statement to run after each row has been sent, to mark it as done or delete it, so that it is not read again. Write `:#name` where the value of the column `name` of the row goes. | string |  | UPDATE orders SET exported = true WHERE id = :#id |
| **delay** | Delay | How long to wait between two runs of the query, in milliseconds. | integer | 500 |  |
| **serverPort** | Server Port | The port of the cluster. Redshift uses 5439 unless it was changed when the cluster was created. | string | 5439 |  |

## Dependencies

At runtime, the `aws-redshift-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:aws-redshift-source"
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

## AWS Redshift Source Kamelet Description

### Authentication

This Kamelet logs in to the Redshift database with a database user and password (`username` and `password`), not with AWS access keys. It connects with the Amazon Redshift JDBC driver, which uses TLS by default.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-redshift-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-redshift-source.kamelet.yaml)
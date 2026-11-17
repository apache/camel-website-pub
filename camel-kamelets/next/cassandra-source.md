# ![cassandra source](_images/kamelets/cassandra-source.svg) Cassandra Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs a CQL query in an Apache Cassandra keyspace every half second, and sends all the rows it returns as one message, a JSON array.

Use it to watch a small Cassandra table, such as a table of settings or of current states, and pass its content on to another system. To write rows, use `cassandra-sink`.

Output: the body is JSON text, an array with one object per row, or one object with `resultStrategy` set to `ONE`. The values of a row are not separate fields of its object: they are in the text of its `formattedContents` field, such as `[id:1, username:'oscerd', city:'Rome']`. The `Content-Type` header is `application/json`.

Good to know: every run sends all the rows the query finds, again and again, and nothing marks a row as read. When the query finds no rows, an empty array `[]` is sent.

## Configuration Options

The following table summarizes the configuration options available for the `cassandra-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Hosts | **Required** The host name or IP address of one or more Cassandra nodes, separated by commas. The other nodes of the cluster are found from them. | string |  | cassandra1.example.com,cassandra2.example.com |
| **connectionPort** | Port | **Required** The port the Cassandra nodes listen on for CQL clients, the same for all hosts. Cassandra uses 9042 unless it was set up otherwise. | string |  | 9042 |
| **keyspace** | Keyspace | **Required** The keyspace (the Cassandra name for a database) that holds the tables of `query`. | string |  | customers |
| **query** | Query | **Required** The CQL query to run, a SELECT. | string |  | SELECT id, username, city FROM accounts |
| **consistencyLevel** | Consistency Level | How many replicas must answer a read before its result counts. `QUORUM`, the default, waits for a majority of the replicas; `ONE` is faster but can return older data. Enum values: \* ONE \* TWO \* THREE \* QUORUM \* ALL \* LOCAL\_QUORUM \* EACH\_QUORUM \* SERIAL \* LOCAL\_SERIAL \* LOCAL\_ONE | string | QUORUM |  |
| **extraTypeCodecs** | Extra Type Codecs | An extra conversion between Cassandra and Java types to turn on, such as `TIMESTAMP_UTC` or `BLOB_TO_ARRAY`. Needed only when a column type does not map to a Java value by default. Enum values: \* BLOB\_TO\_ARRAY \* BOOLEAN\_LIST\_TO\_ARRAY \* BYTE\_LIST\_TO\_ARRAY \* SHORT\_LIST\_TO\_ARRAY \* INT\_LIST\_TO\_ARRAY \* LONG\_LIST\_TO\_ARRAY \* FLOAT\_LIST\_TO\_ARRAY \* DOUBLE\_LIST\_TO\_ARRAY \* TIMESTAMP\_UTC \* TIMESTAMP\_MILLIS\_SYSTEM \* TIMESTAMP\_MILLIS\_UTC \* ZONED\_TIMESTAMP\_SYSTEM \* ZONED\_TIMESTAMP\_UTC \* ZONED\_TIMESTAMP\_PERSISTED \* LOCAL\_TIMESTAMP\_SYSTEM \* LOCAL\_TIMESTAMP\_UTC | string |  |  |
| **password** | Password | The password of the Cassandra user `username`. | string |  |  |
| **resultStrategy** | Result Strategy | Which rows of the result to send. `ALL` sends all rows, `LIMIT_10` and `LIMIT_100` the first 10 or 100, all as one array; `ONE` sends only the first row, as one object. Enum values: \* ALL \* ONE \* LIMIT\_10 \* LIMIT\_100 | string | ALL |  |
| **username** | Username | The Cassandra user to log in as. Leave it empty for a cluster that does not ask for a login. | string |  |  |

## Dependencies

At runtime, the `cassandra-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:cassandraql
    

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
      uri: "kamelet:cassandra-source"
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

## Cassandra Source Kamelet Description

### Authentication methods

The Kamelet supports username/password authentication.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/cassandra-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/cassandra-source.kamelet.yaml)
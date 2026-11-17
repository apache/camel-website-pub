# ![cassandra sink](_images/kamelets/cassandra-sink.svg) Cassandra Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs a CQL statement, such as an INSERT, in an Apache Cassandra keyspace for each message, with the values of its `?` markers taken from the JSON array in the body.

Use it to store events or records as rows of a Cassandra table, for example each reading of a sensor or each order that arrives on a Kafka topic. To read rows, use `cassandra-source`.

Input: the body is a JSON array, as text, with one value for each `?` in `query`, in the same order: for `INSERT INTO accounts (id, username, city) VALUES (?, ?, ?)` the body `[1,"oscerd","Rome"]`. With `jsonPayload` set to false, the body is used as it is, as the one value of a statement with a single `?`.

Output: the body afterwards is an empty List for an INSERT, UPDATE or DELETE.

Good to know: with `jsonPayload` true, the default, a message fails when its body is not a JSON array, such as a JSON object. The values are sent apart from the statement, so the content of a message cannot change it. `ANY`, the default `consistencyLevel`, is the weakest level: a write counts as done even before a replica has stored it.

## Configuration Options

The following table summarizes the configuration options available for the `cassandra-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Hosts | **Required** The host name or IP address of one or more Cassandra nodes, separated by commas. The other nodes of the cluster are found from them. | string |  | cassandra1.example.com,cassandra2.example.com |
| **connectionPort** | Port | **Required** The port the Cassandra nodes listen on for CQL clients, the same for all hosts. Cassandra uses 9042 unless it was set up otherwise. | string |  | 9042 |
| **keyspace** | Keyspace | **Required** The keyspace (the Cassandra name for a database) that holds the tables of `query`. | string |  | customers |
| **query** | Query | **Required** The CQL statement to run for each message, such as an INSERT, UPDATE or DELETE. Write `?` for each value that comes from the body. | string |  | INSERT INTO accounts (id, username, city) VALUES (?, ?, ?) |
| **consistencyLevel** | Consistency Level | How many replicas must store a write before it counts as done. `ANY` is the fastest and the least safe; `QUORUM` or `LOCAL_QUORUM` waits for a majority of the replicas. Enum values: \* ANY \* ONE \* TWO \* THREE \* QUORUM \* ALL \* LOCAL\_QUORUM \* EACH\_QUORUM \* LOCAL\_ONE | string | ANY |  |
| **extraTypeCodecs** | Extra Type Codecs | An extra conversion between Cassandra and Java types to turn on, such as `TIMESTAMP_UTC` or `BLOB_TO_ARRAY`. Needed only when a column type does not map to a value of the body by default. Enum values: \* BLOB\_TO\_ARRAY \* BOOLEAN\_LIST\_TO\_ARRAY \* BYTE\_LIST\_TO\_ARRAY \* SHORT\_LIST\_TO\_ARRAY \* INT\_LIST\_TO\_ARRAY \* LONG\_LIST\_TO\_ARRAY \* FLOAT\_LIST\_TO\_ARRAY \* DOUBLE\_LIST\_TO\_ARRAY \* TIMESTAMP\_UTC \* TIMESTAMP\_MILLIS\_SYSTEM \* TIMESTAMP\_MILLIS\_UTC \* ZONED\_TIMESTAMP\_SYSTEM \* ZONED\_TIMESTAMP\_UTC \* ZONED\_TIMESTAMP\_PERSISTED \* LOCAL\_TIMESTAMP\_SYSTEM \* LOCAL\_TIMESTAMP\_UTC | string |  |  |
| **jsonPayload** | JSON Array Body | If true, the body is read as a JSON array that holds the values of the `?` markers. If false, the body is passed as it is, as the one value of `query`. | boolean | true |  |
| **password** | Password | The password of the Cassandra user `username`. | string |  |  |
| **prepareStatements** | Prepare Statements | Whether `query` is prepared once by Cassandra and then run with the values of each message, which is faster. Set it to false to send the statement as a new one each time. | boolean | true |  |
| **username** | Username | The Cassandra user to log in as. Leave it empty for a cluster that does not ask for a login. | string |  |  |

## Dependencies

At runtime, the `cassandra-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:cassandra-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Cassandra Sink Kamelet Description

### Authentication methods

The Kamelet supports username/password authentication.

### Payload

With `jsonPayload` set to true, the default, the body must be a JSON array that holds the values of the `?` markers of `query`, in their order. A JSON object fails. With `jsonPayload` set to false, the body is passed as it is, as the one value of a statement with a single `?`.

For example, with the query `INSERT INTO accounts (id, username, city) VALUES (?, ?, ?)`, the body is:

```json
[1, "oscerd", "Rome"]
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/cassandra-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/cassandra-sink.kamelet.yaml)
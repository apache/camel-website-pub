# ![cassandra sink](_images/kamelets/cassandra-sink.svg) Cassandra Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to an Apache Cassandra cluster.

## Configuration Options

The following table summarizes the configuration options available for the `cassandra-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The hostname(s) for the Cassandra server(s). Use a comma to separate multiple hostnames. | string |  | localhost |
| **connectionPort** | Connection Port | **Required** The port number(s) of the cassandra server(s). Use a comma to separate multiple port numbers. | string |  | 9042 |
| **keyspace** | Keyspace | **Required** The keyspace to use. | string |  | customers |
| **query** | Query | **Required** The query to execute against the Cassandra cluster table. | string |  |  |
| **consistencyLevel** | Consistency Level | The consistency level to use. Enum values: \* ANY \* ONE \* TWO \* THREE \* QUORUM \* ALL \* LOCAL\_QUORUM \* EACH\_QUORUM \* LOCAL\_ONE | string | ANY |  |
| **extraTypeCodecs** | Extra Type Codecs | To use a specific comma separated list of Extra Type codecs. Enum values: \* BLOB\_TO\_ARRAY \* BOOLEAN\_LIST\_TO\_ARRAY \* BYTE\_LIST\_TO\_ARRAY \* SHORT\_LIST\_TO\_ARRAY \* INT\_LIST\_TO\_ARRAY \* LONG\_LIST\_TO\_ARRAY \* FLOAT\_LIST\_TO\_ARRAY \* DOUBLE\_LIST\_TO\_ARRAY \* TIMESTAMP\_UTC \* TIMESTAMP\_MILLIS\_SYSTEM \* TIMESTAMP\_MILLIS\_UTC \* ZONED\_TIMESTAMP\_SYSTEM \* ZONED\_TIMESTAMP\_UTC \* ZONED\_TIMESTAMP\_PERSISTED \* LOCAL\_TIMESTAMP\_SYSTEM \* LOCAL\_TIMESTAMP\_UTC | string |  |  |
| **jsonPayload** | JSON Payload | If we want to transform the payload in json or not. | boolean | true |  |
| **password** | Password | The password for accessing a secured Cassandra cluster. | string |  |  |
| **prepareStatements** | Prepare Statements | If true, specifies to use PreparedStatements as the query. If false, specifies to use regular Statements as the query. | boolean | true |  |
| **username** | Username | The username for accessing a secured Cassandra cluster. | string |  |  |

## Dependencies

At runtime, the `cassandra-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:cassandraql
    
-   camel:core
    

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

This Kamelet works with JSON Array formatted data, but it’s possible to pass even Object and enable the `jsonPayload` option, transforming the payload directly in Json.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/cassandra-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/cassandra-sink.kamelet.yaml)
# camel-jdbc-kafka-connector sink configuration

Connector Description: Access databases through SQL and JDBC.

When using camel-jdbc-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-jdbc-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.jdbc.CamelJdbcSinkConnector
```

The camel-jdbc sink connector supports 19 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.sink.path.dataSourceName** | **Required** Name of DataSource to lookup in the Registry. If the name is dataSource or default, then Camel will attempt to lookup a default DataSource from the registry, meaning if there is a only one instance of DataSource found, then this DataSource will be used. |  | HIGH |
| **camel.sink.endpoint.allowNamedParameters** | Whether to allow using named parameters in the queries. | true | MEDIUM |
| **camel.sink.endpoint.outputClass** | Specify the full package and class name to use as conversion when outputType=SelectOne or SelectList. |  | MEDIUM |
| **camel.sink.endpoint.outputType** | 
Determines the output the producer should use. One of: \[SelectOne\] \[SelectList\] \[StreamList\].

Enum values:

-   SelectOne
    
-   SelectList
    
-   StreamList
    





 | "SelectList" | MEDIUM |
| **camel.sink.endpoint.parameters** | Optional parameters to the java.sql.Statement. For example to set maxRows, fetchSize etc. This is a multi-value option with prefix: statement. |  | MEDIUM |
| **camel.sink.endpoint.readSize** | The default maximum number of rows that can be read by a polling query. The default value is 0. |  | MEDIUM |
| **camel.sink.endpoint.resetAutoCommit** | Camel will set the autoCommit on the JDBC connection to be false, commit the change after executed the statement and reset the autoCommit flag of the connection at the end, if the resetAutoCommit is true. If the JDBC connection doesn’t support to reset the autoCommit flag, you can set the resetAutoCommit flag to be false, and Camel will not try to reset the autoCommit flag. When used with XA transactions you most likely need to set it to false so that the transaction manager is in charge of committing this tx. | true | MEDIUM |
| **camel.sink.endpoint.transacted** | Whether transactions are in use. | false | MEDIUM |
| **camel.sink.endpoint.useGetBytesForBlob** | To read BLOB columns as bytes instead of string data. This may be needed for certain databases such as Oracle where you must read BLOB columns as bytes. | false | MEDIUM |
| **camel.sink.endpoint.useHeadersAsParameters** | Set this option to true to use the prepareStatementStrategy with named parameters. This allows to define queries with named placeholders, and use headers with the dynamic values for the query placeholders. | false | MEDIUM |
| **camel.sink.endpoint.useJDBC4ColumnNameAndLabelSemantics** | Sets whether to use JDBC 4 or JDBC 3.0 or older semantic when retrieving column name. JDBC 4.0 uses columnLabel to get the column name where as JDBC 3.0 uses both columnName or columnLabel. Unfortunately JDBC drivers behave differently so you can use this option to work out issues around your JDBC driver if you get problem using this component This option is default true. | true | MEDIUM |
| **camel.sink.endpoint.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.sink.endpoint.beanRowMapper** | To use a custom org.apache.camel.component.jdbc.BeanRowMapper when using outputClass. The default implementation will lower case the row names and skip underscores, and dashes. For example CUST\_ID is mapped as custId. |  | MEDIUM |
| **camel.sink.endpoint.connectionStrategy** | To use a custom strategy for working with connections. Do not use a custom strategy when using the spring-jdbc component because a special Spring ConnectionStrategy is used by default to support Spring Transactions. |  | MEDIUM |
| **camel.sink.endpoint.prepareStatementStrategy** | Allows the plugin to use a custom org.apache.camel.component.jdbc.JdbcPrepareStatementStrategy to control preparation of the query and prepared statement. |  | MEDIUM |
| **camel.component.jdbc.dataSource** | To use the DataSource instance instead of looking up the data source by name from the registry. |  | MEDIUM |
| **camel.component.jdbc.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.component.jdbc.autowiredEnabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | MEDIUM |
| **camel.component.jdbc.connectionStrategy** | To use a custom strategy for working with connections. Do not use a custom strategy when using the spring-jdbc component because a special Spring ConnectionStrategy is used by default to support Spring Transactions. |  | MEDIUM |

The camel-jdbc sink connector has no converters out of the box.

The camel-jdbc sink connector has no transforms out of the box.

The camel-jdbc sink connector has no aggregation strategies out of the box.
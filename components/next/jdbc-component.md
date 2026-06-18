# JDBC

**Since Camel 1.2**

**Only producer is supported**

The JDBC component enables you to access databases through JDBC, where SQL queries (SELECT) and operations (INSERT, UPDATE, etc.) are sent in the message body. This component uses the standard JDBC API, unlike the [SQL Component](sql-component.md), which uses spring-jdbc.

> **Note**
> When you use Spring and need to support Spring Transactions, use the [Spring JDBC Component](spring-jdbc-component.md) instead of this one.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jdbc</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

This component can only be used to define producer endpoints, which means that you cannot use the JDBC component in a `from()` statement.

## URI format

jdbc:dataSourceName\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The JDBC component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataSource** (producer) | To use the DataSource instance instead of looking up the data source by name from the registry. |  | DataSource |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **connectionStrategy** (advanced) | To use a custom strategy for working with connections. Do not use a custom strategy when using the spring-jdbc component because a special Spring ConnectionStrategy is used by default to support Spring Transactions. |  | ConnectionStrategy |

## Endpoint Options

The JDBC endpoint is configured using URI syntax:

jdbc:dataSourceName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataSourceName** (producer) | **Required** Name of DataSource to lookup in the Registry. If the name is dataSource or default, then Camel will attempt to lookup a default DataSource from the registry, meaning if there is a only one instance of DataSource found, then this DataSource will be used. |  | String |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowNamedParameters** (producer) | Whether to allow using named parameters in the queries. | true | boolean |
| **outputClass** (producer) | Specify the full package and class name to use as conversion when outputType=SelectOne or SelectList. |  | String |
| **outputType** (producer) | 
Determines the output the producer should use.

Enum values:

-   SelectOne
    
-   SelectList
    
-   StreamList
    





 | SelectList | JdbcOutputType |
| **parameters** (producer) | Optional parameters to the java.sql.Statement. For example to set maxRows, fetchSize etc. This is a multi-value option with prefix: statement. |  | Map |
| **readSize** (producer) | The default maximum number of rows that can be read by a polling query. The default value is 0. |  | int |
| **resetAutoCommit** (producer) | Camel will set the autoCommit on the JDBC connection to be false, commit the change after executed the statement and reset the autoCommit flag of the connection at the end, if the resetAutoCommit is true. If the JDBC connection doesn’t support to reset the autoCommit flag, you can set the resetAutoCommit flag to be false, and Camel will not try to reset the autoCommit flag. When used with XA transactions you most likely need to set it to false so that the transaction manager is in charge of committing this tx. | true | boolean |
| **transacted** (producer) | Whether transactions are in use. | false | boolean |
| **useGetBytesForBlob** (producer) | To read BLOB columns as bytes instead of string data. This may be needed for certain databases such as Oracle where you must read BLOB columns as bytes. | false | boolean |
| **useHeadersAsParameters** (producer) | Set this option to true to use the prepareStatementStrategy with named parameters. This allows to define queries with named placeholders, and use headers with the dynamic values for the query placeholders. | false | boolean |
| **useJDBC4ColumnNameAndLabelSemantics** (producer) | Sets whether to use JDBC 4 or JDBC 3.0 or older semantic when retrieving column name. JDBC 4.0 uses columnLabel to get the column name where as JDBC 3.0 uses both columnName or columnLabel. Unfortunately JDBC drivers behave differently so you can use this option to work out issues around your JDBC driver if you get problem using this component This option is default true. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **beanRowMapper** (advanced) | To use a custom org.apache.camel.component.jdbc.BeanRowMapper when using outputClass. The default implementation will lower case the row names and skip underscores, and dashes. For example CUST\_ID is mapped as custId. |  | BeanRowMapper |
| **connectionStrategy** (advanced) | To use a custom strategy for working with connections. Do not use a custom strategy when using the spring-jdbc component because a special Spring ConnectionStrategy is used by default to support Spring Transactions. |  | ConnectionStrategy |
| **prepareStatementStrategy** (advanced) | Allows the plugin to use a custom org.apache.camel.component.jdbc.JdbcPrepareStatementStrategy to control preparation of the query and prepared statement. |  | JdbcPrepareStatementStrategy |

## Message Headers

The JDBC component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelJdbcUpdateCount** (producer) Constant: [`JDBC_UPDATE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-jdbc/latest/org/apache/camel/component/jdbc/JdbcConstants.html#JDBC_UPDATE_COUNT) | If the query is an UPDATE, query the update count is returned in this OUT header. |  | int |
| **CamelJdbcRowCount** (producer) Constant: [`JDBC_ROW_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-jdbc/latest/org/apache/camel/component/jdbc/JdbcConstants.html#JDBC_ROW_COUNT) | If the query is a SELECT, query the row count is returned in this OUT header. |  | int |
| **CamelJdbcColumnNames** (producer) Constant: [`JDBC_COLUMN_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-jdbc/latest/org/apache/camel/component/jdbc/JdbcConstants.html#JDBC_COLUMN_NAMES) | The column names from the ResultSet as a java.util.Set type. |  | Set |
| **CamelJdbcParameters** (producer) Constant: [`JDBC_PARAMETERS`](https://javadoc.io/doc/org.apache.camel/camel-jdbc/latest/org/apache/camel/component/jdbc/JdbcConstants.html#JDBC_PARAMETERS) | A java.util.Map which has the headers to be used if useHeadersAsParameters has been enabled. |  | Map |
| **CamelRetrieveGeneratedKeys** (producer) Constant: [`JDBC_RETRIEVE_GENERATED_KEYS`](https://javadoc.io/doc/org.apache.camel/camel-jdbc/latest/org/apache/camel/component/jdbc/JdbcConstants.html#JDBC_RETRIEVE_GENERATED_KEYS) | Set its value to true to retrieve generated keys. | false | Boolean |
| **CamelGeneratedColumns** (producer) Constant: [`JDBC_GENERATED_COLUMNS`](https://javadoc.io/doc/org.apache.camel/camel-jdbc/latest/org/apache/camel/component/jdbc/JdbcConstants.html#JDBC_GENERATED_COLUMNS) | Set it to specify the expected generated columns. |  | String\[\] or int\[\] |
| **CamelGeneratedKeysRowCount** (producer) Constant: [`JDBC_GENERATED_KEYS_ROW_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-jdbc/latest/org/apache/camel/component/jdbc/JdbcConstants.html#JDBC_GENERATED_KEYS_ROW_COUNT) | The number of rows in the header that contains generated keys. |  | int |
| **CamelGeneratedKeysRows** (producer) Constant: [`JDBC_GENERATED_KEYS_DATA`](https://javadoc.io/doc/org.apache.camel/camel-jdbc/latest/org/apache/camel/component/jdbc/JdbcConstants.html#JDBC_GENERATED_KEYS_DATA) | Rows that contains the generated keys. |  | List |

## Usage

### Result

By default, the result is returned in the OUT body as an `ArrayList<HashMap<String, Object>>`. The `List` object contains the list of rows and the `Map` objects contain each row with the `String` key as the column name. You can use the option `outputType` to control the result.

**Note:** This component fetches `ResultSetMetaData` to be able to return the column name as the key in the `Map`.

### Generated keys

If you insert data using SQL INSERT, then the RDBMS may support auto generated keys. You can instruct the [JDBC](#) producer to return the generated keys in headers.  
To do that set the header `CamelRetrieveGeneratedKeys=true`. Then the generated keys will be provided as headers with the keys listed in the table above.

Using generated keys does not work together with named parameters.

### Using named parameters

In the given route below, we want to get all the projects from the `projects` table. Notice the SQL query has two named parameters, `:?lic` and `:?min`. Camel will then look up these parameters from the message headers. Notice in the example above we set two headers with constant value for the named parameters:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:projects")
    .setHeader("lic", constant("ASF"))
    .setHeader("min", constant(123))
    .setBody("select * from projects where license = :?lic and id > :?min order by id")
    .to("jdbc:myDataSource?useHeadersAsParameters=true");
```

```xml
<route>
    <from uri="direct:projects"/>
    <setHeader name="lic">
        <constant>ASF</constant>
    </setHeader>
    <setHeader name="min">
        <constant>123</constant>
    </setHeader>
    <setBody>
        <constant>select * from projects where license = :?lic and id &gt; :?min order by id</constant>
    </setBody>
    <to uri="jdbc:myDataSource?useHeadersAsParameters=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:projects
    steps:
      - setHeader:
          name: lic
          constant: ASF
      - setHeader:
          name: min
          constant: "123"
      - setBody:
          constant: "select * from projects where license = :?lic and id > :?min order by id"
      - to:
          uri: jdbc:myDataSource
          parameters:
            useHeadersAsParameters: true
```

You can also store the header values in a `java.util.Map` and store the map on the headers with the key `CamelJdbcParameters`.

## Examples

In the following example, we set up the DataSource that camel-jdbc requires. First we register our datasource in the Camel registry as `testdb`:

_Java-only: programmatic DataSource registration using EmbeddedDatabaseBuilder_

```java
EmbeddedDatabase db = new EmbeddedDatabaseBuilder()
      .setType(EmbeddedDatabaseType.H2).addScript("sql/init.sql").build();

CamelContext context = ...
context.getRegistry().bind("testdb", db);
```

Then we configure a route that routes to the JDBC component, so the SQL will be executed. Note how we refer to the `testdb` datasource that was bound in the previous step:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:hello")
    .to("jdbc:testdb");
```

```xml
<route>
  <from uri="direct:hello"/>
  <to uri="jdbc:testdb"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:hello
      steps:
        - to:
            uri: jdbc:testdb
```

We create an endpoint, add the SQL query to the body of the IN message, and then send the exchange. The result of the query is returned in the _OUT_ body:

_Java-only: using ProducerTemplate to send an exchange to the endpoint_

```java
Endpoint endpoint = context.getEndpoint("direct:hello");
Exchange exchange = endpoint.createExchange();
// then we set the SQL on the in body
exchange.getMessage().setBody("select * from customer order by ID");
// now we send the exchange to the endpoint, and receive the response from Camel
Exchange out = template.send(endpoint, exchange);
```

If you want to work on the rows one by one instead of the entire ResultSet at once, you need to use the Splitter EIP such as:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:hello")
// here we split the data from the testdb into new messages one by one,
// so the mock endpoint will receive a message per row in the table
// the StreamList option allows streaming the result of the query without creating a List of rows
// and notice we also enable streaming mode on the splitter
.to("jdbc:testdb?outputType=StreamList")
  .split(body()).streaming()
  .to("mock:result");
```

```xml
<route>
  <from uri="direct:hello"/>
  <to uri="jdbc:testdb?outputType=StreamList"/>
  <split streaming="true">
    <body/>
    <to uri="mock:result"/>
  </split>
</route>
```

```yaml
- route:
    from:
      uri: direct:hello
    steps:
      - to:
          uri: jdbc:testdb
          parameters:
            outputType: StreamList
      - split:
          expression:
            body: {}
          streaming: true
          steps:
            - to:
                uri: mock:result
```

### Polling the database every minute

If we want to poll a database using the JDBC component, we need to combine it with a polling scheduler such as the [Timer](timer-component.md) or [Quartz](quartz-component.md) etc. In the following example, we retrieve data from the database every 60 seconds:

-   Java
    
-   XML
    
-   YAML
    

```java
from("timer://foo?period=60000")
    .setBody(constant("select * from customer"))
    .to("jdbc:testdb")
    .to("activemq:queue:customers");
```

```xml
<route>
    <from uri="timer://foo?period=60000"/>
    <setBody>
        <constant>select * from customer</constant>
    </setBody>
    <to uri="jdbc:testdb"/>
    <to uri="activemq:queue:customers"/>
</route>
```

```yaml
- route:
    from:
      uri: timer://foo
      parameters:
        period: "60000"
    steps:
      - setBody:
          constant: "select * from customer"
      - to:
          uri: jdbc:testdb
      - to:
          uri: activemq:queue:customers
```

### Move Data Between Data Sources

A common use case is to query for data, process it and move it to another data source (ETL operations). In the following example, we retrieve new customer records from the source table every hour, filter/transform them and move them to a destination table:

_Java-only: ETL route using inline Processor to filter and transform results_

```java
from("timer://MoveNewCustomersEveryHour?period=3600000")
    .setBody(constant("select * from customer where create_time > (sysdate-1/24)"))
    .to("jdbc:testdb")
    .split(body())
        .process(new MyCustomerProcessor()) //filter/transform results as needed
        .setBody(simple("insert into processed_customer values('${body[ID]}','${body[NAME]}')"))
        .to("jdbc:testdb");
```

## Spring Boot Auto-Configuration

When using jdbc with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jdbc-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jdbc.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.jdbc.connection-strategy** | To use a custom strategy for working with connections. Do not use a custom strategy when using the spring-jdbc component because a special Spring ConnectionStrategy is used by default to support Spring Transactions. The option is a org.apache.camel.component.jdbc.ConnectionStrategy type. |  | ConnectionStrategy |
| **camel.component.jdbc.enabled** | Whether to enable auto configuration of the jdbc component. This is enabled by default. |  | Boolean |
| **camel.component.jdbc.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
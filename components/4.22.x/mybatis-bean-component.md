# MyBatis Bean

**Since Camel 2.22**

**Only producer is supported**

The MyBatis Bean component allows you to query, insert, update and delete data in a relational database using [MyBatis](http://mybatis.org/) bean annotations.

This component can **only** be used as a producer. If you want to consume from MyBatis, then use the regular **mybatis** component.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-mybatis</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

This component will by default load the MyBatis SqlMapConfig file from the root of the classpath with the expected name of `SqlMapConfig.xml`. If the file is located in another location, you will need to configure the `configurationUri` option on the `MyBatisComponent` component.

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

The MyBatis Bean component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configurationUri** (producer) | Location of MyBatis xml configuration file. The default value is: SqlMapConfig.xml loaded from the classpath. | SqlMapConfig.xml | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **sqlSessionFactory** (advanced) | **Autowired** To use the SqlSessionFactory. |  | SqlSessionFactory |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The MyBatis Bean endpoint is configured using URI syntax:

mybatis-bean:beanName:methodName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **beanName** (producer) | **Required** Name of the bean with the MyBatis annotations. This can either by a type alias or a FQN class name. |  | String |
| **methodName** (producer) | **Required** Name of the method on the bean that has the SQL query to be executed. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **executorType** (producer) | 
The executor type to be used while executing statements. simple - executor does nothing special. reuse - executor reuses prepared statements. batch - executor reuses statements and batches updates.

Enum values:

-   SIMPLE
    
-   REUSE
    
-   BATCH
    





 | SIMPLE | ExecutorType |
| **inputHeader** (producer) | User the header value for input parameters instead of the message body. By default, inputHeader == null and the input parameters are taken from the message body. If outputHeader is set, the value is used and query parameters will be taken from the header instead of the body. |  | String |
| **outputHeader** (producer) | Store the query result in a header instead of the message body. By default, outputHeader == null and the query result is stored in the message body, any existing content in the message body is discarded. If outputHeader is set, the value is used as the name of the header to store the query result and the original message body is preserved. Setting outputHeader will also omit populating the default CamelMyBatisResult header since it would be the same as outputHeader all the time. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The MyBatis Bean component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMyBatisResult** (producer) Constant: [`MYBATIS_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-mybatis/latest/org/apache/camel/component/mybatis/MyBatisConstants.html#MYBATIS_RESULT) | The response returned from MyBatis in any of the operations. Such as INSERT could return the auto-generated key, or number of rows etc. |  | Object |

## Usage

### Message Body

The response from MyBatis will only be set as the body if it’s a `SELECT` statement. That means, for example, for `INSERT` statements Camel will not replace the body. This allows you to continue routing and keep the original body. The response from MyBatis is always stored in the header with the key `CamelMyBatisResult`.

## Examples

For example, if you wish to consume beans from a JMS queue and insert them into a database, you could do the following:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:queue:newAccount")
    .to("mybatis-bean:AccountService:insertBeanAccount");
```

```xml
<route>
  <from uri="activemq:queue:newAccount"/>
  <to uri="mybatis-bean:AccountService:insertBeanAccount"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:queue:newAccount
      steps:
        - to:
            uri: mybatis-bean:AccountService:insertBeanAccount
```

Notice we have to specify the bean name and method name, as we need to instruct Camel which kind of operation to invoke.

Where `AccountService` is the type alias for the bean that has the MyBatis bean annotations. You can configure type alias in the SqlMapConfig file:

```xml
    <typeAliases>
        <typeAlias alias="Account" type="org.apache.camel.component.mybatis.Account"/>
        <typeAlias alias="AccountService" type="org.apache.camel.component.mybatis.bean.AccountService"/>
    </typeAliases>
```

On the `AccountService` bean you can declare the MyBatis mappins using annotations as shown:

_Java-only: MyBatis bean annotation mappings_

```java
public interface AccountService {

    @Select("select ACC_ID as id, ACC_FIRST_NAME as firstName, ACC_LAST_NAME as lastName"
        + ", ACC_EMAIL as emailAddress from ACCOUNT where ACC_ID = #{id}")
    Account selectBeanAccountById(@Param("id") int no);

    @Select("select * from ACCOUNT order by ACC_ID")
    @ResultMap("Account.AccountResult")
    List<Account> selectBeanAllAccounts();

    @Insert("insert into ACCOUNT (ACC_ID,ACC_FIRST_NAME,ACC_LAST_NAME,ACC_EMAIL)"
        + " values (#{id}, #{firstName}, #{lastName}, #{emailAddress})")
    void insertBeanAccount(Account account);

}
```
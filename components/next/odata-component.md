# OData

**Since Camel 4.23**

**Only producer is supported**

The OData component allows you to interact with OData V4 services using standard OData CRUD operations.

The component provides OData-specific request and response handling while using Camel HTTP as the underlying HTTP transport.

The OData component is the successor to the deprecated `camel-olingo4` component.

The component supports OData V4 services using JSON representations.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-odata</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

### odata:httpUri

Where `httpUri` is the base URL of the OData entity set or resource.

For example:

```text
odata:http://localhost:8080/odata/Products
odata:https://services.odata.org/V4/Northwind/Northwind.svc/Categories
```

The URI can also contain endpoint options as query parameters.

The OData query options can alternatively be configured on the endpoint or supplied dynamically using message headers.

The component uses Camel HTTP for the underlying HTTP transport.

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

The OData component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OData endpoint is configured using URI syntax:

odata:httpUri

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **httpUri** (producer) | **Required** The base OData service URI. |  | URI |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **count** (producer) | The OData $count query parameter. | false | Boolean |
| **expand** (producer) | The OData $expand query parameter. |  | String |
| **filter** (producer) | The OData $filter query parameter. |  | String |
| **operation** (producer) | 
The OData operation to perform.

Enum values:

-   READ\_SET
    
-   READ\_ENTRY
    
-   CREATE
    
-   UPDATE
    
-   DELETE
    





 |  | ODataOperation |
| **orderBy** (producer) | The OData $orderby query parameter. |  | String |
| **select** (producer) | The OData $select query parameter. |  | String |
| **skip** (producer) | The OData $skip query parameter. |  | Integer |
| **top** (producer) | The OData $top query parameter. |  | Integer |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **authBearerToken** (security) | Bearer token for Bearer authentication. |  | String |
| **authMethod** (security) | Authentication method to use (e.g., Basic, Bearer). |  | String |
| **authPassword** (security) | Password for Basic authentication. |  | String |
| **authUsername** (security) | Username for Basic authentication. |  | String |
| **sslContextParameters** (security) | To use a custom SSLContextParameters. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Message Headers

The OData component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelODataOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#OPERATION) | 
The OData operation to perform.

Enum values:

-   READ\_SET
    
-   READ\_ENTRY
    
-   CREATE
    
-   UPDATE
    
-   DELETE
    





 |  | ODataOperation |
| **CamelODataKey** (producer) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#KEY) | The OData entity key. |  | String |
| **CamelODataETag** (producer) Constant: [`ETAG`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#ETAG) | The OData ETag. |  | String |
| **CamelODataNextLink** (producer) Constant: [`NEXT_LINK`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#NEXT_LINK) | The OData next link for pagination. |  | String |
| **CamelODataIncludeCount** (producer) Constant: [`INCLUDE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#INCLUDE_COUNT) | Whether to include the OData count in the response. |  | Boolean |
| **CamelODataCount** (producer) Constant: [`COUNT`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#COUNT) | The OData count returned by the server. |  | Long |
| **CamelODataFilter** (producer) Constant: [`FILTER`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#FILTER) | The OData filter expression. |  | String |
| **CamelODataSelect** (producer) Constant: [`SELECT`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#SELECT) | The OData select expression. |  | String |
| **CamelODataExpand** (producer) Constant: [`EXPAND`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#EXPAND) | The OData expand expression. |  | String |
| **CamelODataOrderBy** (producer) Constant: [`ORDER_BY`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#ORDER_BY) | The OData orderby expression. |  | String |
| **CamelODataTop** (producer) Constant: [`TOP`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#TOP) | The OData top query option. |  | Integer |
| **CamelODataSkip** (producer) Constant: [`SKIP`](https://javadoc.io/doc/org.apache.camel/camel-odata/latest/org/apache/camel/component/odata/ODataConstants.html#SKIP) | The OData skip query option. |  | Integer |
> **Note**
> This is a producer-only component. Per-message options can be supplied through `CamelOData` headers in addition to endpoint options.

> **Note**
> If the route receives messages from an untrusted producer, take care when forwarding internal Camel headers to this component. In particular, an inbound `Authorization` header can be used for the OData request and takes precedence over endpoint authentication.

## Operations

The operation is selected using the `CamelODataOperation` message header or the `operation` endpoint option.

The following operations are supported:

  
| Operation | HTTP Method | Description |
| --- | --- | --- |
| `READ_SET` | `GET` | Reads a collection of entities. This is the default operation. |
| `READ_ENTRY` | `GET` | Reads a single entity. Use `CamelODataKey` to specify the entity key. |
| `CREATE` | `POST` | Creates a new entity using the message body as the request payload. |
| `UPDATE` | `PATCH` | Updates an existing entity using `CamelODataKey` to identify the entity. |
| `DELETE` | `DELETE` | Deletes an existing entity using `CamelODataKey` to identify the entity. |

For `READ_ENTRY`, `UPDATE`, and `DELETE`, the key is appended to the configured resource URI.

For example:

```text
CamelODataKey = 101
odata:http://localhost:8080/odata/Products
```

results in:

```text
http://localhost:8080/odata/Products(101)
```

The key is treated as an OData key expression. The component does not automatically add quotes or otherwise change the supplied key value.

For example, a string key can be supplied as `'ABC-123'`, while a composite key can be supplied as `ProductID=101,CategoryID=5`.

The key value should be a valid and trusted OData key expression.

## Message Headers

The following message headers can be used to control OData processing dynamically.

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelODataOperation` | `ODataOperation` / `String` | Specifies the operation to execute. |
| `CamelODataKey` | `String` | Specifies the key for `READ_ENTRY`, `UPDATE`, and `DELETE` operations. |
| `CamelODataFilter` | `String` | Overrides the `$filter` query option. |
| `CamelODataSelect` | `String` | Overrides the `$select` query option. |
| `CamelODataExpand` | `String` | Overrides the `$expand` query option. |
| `CamelODataOrderBy` | `String` | Overrides the `$orderby` query option. |
| `CamelODataTop` | `Integer` | Overrides the `$top` query option. |
| `CamelODataSkip` | `Integer` | Overrides the `$skip` query option. |
| `CamelODataIncludeCount` | `Boolean` | Controls whether the `$count` query option is included in the request. |
| `CamelODataETag` | `String` | Supplies an ETag for the `If-Match` HTTP request header. The component also populates this header from an ETag returned by the OData service. |
| `CamelODataCount` | `Long` | Contains the count returned by the OData service when an `@odata.count` value is present. |
| `CamelODataNextLink` | `String` | Contains the `@odata.nextLink` value returned by the OData service when present. |
| `CamelHttpResponseCode` | `Integer` | Contains the HTTP response status code returned by the OData service. |

A message-level `Authorization` header can also be supplied.

When an `Authorization` header is present, it takes precedence over authentication configured on the OData endpoint.

If the OData route is exposed to an upstream HTTP consumer, such as `platform-http`, take care that an inbound `Authorization` header may be forwarded to the OData service.

If the upstream authorization credentials must not be forwarded, remove the header before sending the exchange to the OData component.

For example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("platform-http:/products")
    .removeHeader("Authorization")
    .to("odata:http://my-odata-service/odata/Products");
```

```xml
<route>
  <from uri="platform-http:/products"/>
  <removeHeader name="Authorization"/>
  <to uri="odata:http://my-odata-service/odata/Products"/>
</route>
```

```yaml
- route:
    from:
      uri: platform-http:/products
      steps:
        - removeHeader:
            name: Authorization
        - to:
            uri: odata:http://my-odata-service/odata/Products
```

## Query Options

The component supports the following OData query options:

  
| Option | Type | Description |
| --- | --- | --- |
| `filter` | `String` | OData `$filter` expression. |
| `select` | `String` | OData `$select` expression. |
| `expand` | `String` | OData `$expand` expression. |
| `orderBy` | `String` | OData `$orderby` expression. |
| `top` | `Integer` | OData `$top` value. |
| `skip` | `Integer` | OData `$skip` value. |
| `count` | `Boolean` | Controls the OData `$count` query option. |

Additional OData query options can be supplied as endpoint URI parameters. Because the component uses lenient endpoint properties, options that are not defined as explicit component options are passed through as OData query parameters. Ensure that endpoint option names are spelled correctly and that any additional options are valid OData query options.

For example:

```text
odata:http://localhost:8080/odata/Products?filter=Name%20eq%20%27Laptop%27&select=Name,Price&top=10
```

Query options configured through message headers take precedence over the corresponding endpoint configuration.

## Authentication

The component supports Basic authentication and Bearer token authentication through endpoint options.

For example, Basic authentication can be configured using:

```text
odata:http://localhost:8080/odata/Products?authMethod=Basic&authUsername=user&authPassword=password
```

Bearer token authentication can be configured using the `authBearerToken` option.

Authentication can also be supplied dynamically using the message-level `Authorization` header:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getProducts")
    .setHeader("Authorization", constant("Bearer my-token"))
    .to("odata:http://my-odata-service/odata/Products");
```

```xml
<route>
  <from uri="direct:getProducts"/>
  <setHeader name="Authorization">
    <constant>Bearer my-token</constant>
  </setHeader>
  <to uri="odata:http://my-odata-service/odata/Products"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getProducts
      steps:
        - setHeader:
            name: Authorization
            expression:
              constant:
                expression: "Bearer my-token"
        - to:
            uri: odata:http://my-odata-service/odata/Products
```

When an `Authorization` header is present on the message, it takes precedence over endpoint authentication.

Take care when forwarding exchanges from an upstream HTTP consumer because the incoming `Authorization` header may be forwarded to the OData service.

## ETags

The component supports optimistic concurrency using OData/HTTP ETags.

An ETag supplied in `CamelODataETag` is sent to the service using the HTTP `If-Match` header.

For example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:updateProduct")
    .setHeader("CamelODataOperation", constant("UPDATE"))
    .setHeader("CamelODataKey", constant("101"))
    .setHeader("CamelODataETag", constant("W/\"etag-value\""))
    .setBody(constant("{\"Price\": 249.99}"))
    .to("odata:http://my-odata-service/odata/Products");
```

```xml
<route>
  <from uri="direct:updateProduct"/>
  <setHeader name="CamelODataOperation">
    <constant>UPDATE</constant>
  </setHeader>
  <setHeader name="CamelODataKey">
    <constant>101</constant>
  </setHeader>
  <setHeader name="CamelODataETag">
    <constant>W/"etag-value"</constant>
  </setHeader>
  <setBody>
    <constant>{"Price": 249.99}</constant>
  </setBody>
  <to uri="odata:http://my-odata-service/odata/Products"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:updateProduct
      steps:
        - setHeader:
            name: CamelODataOperation
            expression:
              constant:
                expression: UPDATE
        - setHeader:
            name: CamelODataKey
            expression:
              constant:
                expression: "101"
        - setHeader:
            name: CamelODataETag
            expression:
              constant:
                expression: 'W/"etag-value"'
        - setBody:
            expression:
              constant:
                expression: '{"Price": 249.99}'
        - to:
            uri: odata:http://my-odata-service/odata/Products
```

When the service returns an HTTP `ETag` header, the value is exposed as `CamelODataETag`.

The component also recognizes the OData `@odata.etag` property in a JSON response.

## OData Response Metadata

For responses containing OData metadata, the component exposes commonly used values as Camel message headers.

For example, a response containing:

```json
{
  "@odata.count": 42,
  "@odata.nextLink": "https://my-odata-service/odata/Products?$skip=10",
  "value": [
    {
      "ID": 1,
      "Name": "Laptop"
    }
  ]
}
```

makes the count and next-link available through:

```java
exchange.getMessage().getHeader("CamelODataCount");
exchange.getMessage().getHeader("CamelODataNextLink");
```

The response body contains the parsed JSON response.

## SSL Configuration

The component uses Camel HTTP for the underlying HTTP transport.

The `sslContextParameters` endpoint option can be used to configure SSL/TLS parameters for HTTPS connections.

Refer to the generated endpoint options section for details about configuring SSL context parameters.

## Examples

### Fetching a Collection

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getProducts")
    .to("odata:http://my-odata-service/odata/Products")
    .split(simple("${body[value]}"))
        .to("log:product")
    .end();
```

```xml
<route>
  <from uri="direct:getProducts"/>
  <to uri="odata:http://my-odata-service/odata/Products"/>
  <split>
    <simple>${body[value]}</simple>
    <to uri="log:product"/>
  </split>
</route>
```

```yaml
- route:
    from:
      uri: direct:getProducts
      steps:
        - to:
            uri: odata:http://my-odata-service/odata/Products
        - split:
            expression:
              simple:
                expression: "${body[value]}"
            steps:
              - to:
                  uri: log:product
```

The default operation is `READ_SET`, so no operation header is required. The response body is the parsed JSON object as a `Map`, and the entities are in its `value` entry.

### Reading a Single Entity

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getProductById")
    .setHeader("CamelODataOperation", constant("READ_ENTRY"))
    .setHeader("CamelODataKey", constant("101"))
    .to("odata:http://my-odata-service/odata/Products");
```

```xml
<route>
  <from uri="direct:getProductById"/>
  <setHeader name="CamelODataOperation">
    <constant>READ_ENTRY</constant>
  </setHeader>
  <setHeader name="CamelODataKey">
    <constant>101</constant>
  </setHeader>
  <to uri="odata:http://my-odata-service/odata/Products"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getProductById
      steps:
        - setHeader:
            name: CamelODataOperation
            expression:
              constant:
                expression: READ_ENTRY
        - setHeader:
            name: CamelODataKey
            expression:
              constant:
                expression: "101"
        - to:
            uri: odata:http://my-odata-service/odata/Products
```

This results in a request to:

```text
http://my-odata-service/odata/Products(101)
```

### Creating an Entity

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createProduct")
    .setHeader("CamelODataOperation", constant("CREATE"))
    .setBody(constant("{\"Name\": \"Tablet\", \"Price\": 299.99}"))
    .to("odata:http://my-odata-service/odata/Products");
```

```xml
<route>
  <from uri="direct:createProduct"/>
  <setHeader name="CamelODataOperation">
    <constant>CREATE</constant>
  </setHeader>
  <setBody>
    <constant>{"Name": "Tablet", "Price": 299.99}</constant>
  </setBody>
  <to uri="odata:http://my-odata-service/odata/Products"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createProduct
      steps:
        - setHeader:
            name: CamelODataOperation
            expression:
              constant:
                expression: CREATE
        - setBody:
            expression:
              constant:
                expression: '{"Name": "Tablet", "Price": 299.99}'
        - to:
            uri: odata:http://my-odata-service/odata/Products
```

The component sends the message body using HTTP `POST`. A `String` body is sent as is, so it must be JSON; any other body, such as a `Map`, is serialized to JSON.

### Updating an Entity

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:updateProduct")
    .setHeader("CamelODataOperation", constant("UPDATE"))
    .setHeader("CamelODataKey", constant("101"))
    .setHeader("CamelODataETag", constant("W/\"etag-value\""))
    .setBody(constant("{\"Price\": 249.99}"))
    .to("odata:http://my-odata-service/odata/Products");
```

```xml
<route>
  <from uri="direct:updateProduct"/>
  <setHeader name="CamelODataOperation">
    <constant>UPDATE</constant>
  </setHeader>
  <setHeader name="CamelODataKey">
    <constant>101</constant>
  </setHeader>
  <setHeader name="CamelODataETag">
    <constant>W/"etag-value"</constant>
  </setHeader>
  <setBody>
    <constant>{"Price": 249.99}</constant>
  </setBody>
  <to uri="odata:http://my-odata-service/odata/Products"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:updateProduct
      steps:
        - setHeader:
            name: CamelODataOperation
            expression:
              constant:
                expression: UPDATE
        - setHeader:
            name: CamelODataKey
            expression:
              constant:
                expression: "101"
        - setHeader:
            name: CamelODataETag
            expression:
              constant:
                expression: 'W/"etag-value"'
        - setBody:
            expression:
              constant:
                expression: '{"Price": 249.99}'
        - to:
            uri: odata:http://my-odata-service/odata/Products
```

The component sends the update using HTTP `PATCH`.

When an ETag is supplied, it is sent using the HTTP `If-Match` header.

### Deleting an Entity

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deleteProduct")
    .setHeader("CamelODataOperation", constant("DELETE"))
    .setHeader("CamelODataKey", constant("101"))
    .to("odata:http://my-odata-service/odata/Products");
```

```xml
<route>
  <from uri="direct:deleteProduct"/>
  <setHeader name="CamelODataOperation">
    <constant>DELETE</constant>
  </setHeader>
  <setHeader name="CamelODataKey">
    <constant>101</constant>
  </setHeader>
  <to uri="odata:http://my-odata-service/odata/Products"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:deleteProduct
      steps:
        - setHeader:
            name: CamelODataOperation
            expression:
              constant:
                expression: DELETE
        - setHeader:
            name: CamelODataKey
            expression:
              constant:
                expression: "101"
        - to:
            uri: odata:http://my-odata-service/odata/Products
```

The component sends an HTTP `DELETE` request for the specified entity.

## Limitations

The component currently supports producer operations only.

The `$batch` operation is not currently supported.

The component supports OData V4 JSON representations only.
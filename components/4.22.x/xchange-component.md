# XChange

**Since Camel 2.21**

**Only producer is supported**

The XChange component uses the [XChange](https://knowm.org/open-source/xchange/) Java library to provide access to 60+ Bitcoin and Altcoin exchanges. It comes with a consistent interface for trading and accessing market data.

Camel can get crypto currency market data, query historical data, place market orders and much more.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-xchange</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

xchange://exchange?options

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

The XChange component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The XChange endpoint is configured using URI syntax:

xchange:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (producer) | **Required** The exchange to connect to. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **currency** (producer) | The currency. |  | Currency |
| **currencyPair** (producer) | The currency pair. |  | String |
| **method** (producer) | 
**Required** The method to execute.

Enum values:

-   balances
    
-   fundingHistory
    
-   wallets
    
-   currencies
    
-   currencyMetaData
    
-   currencyPairs
    
-   currencyPairMetaData
    
-   ticker
    





 |  | XChangeMethod |
| **service** (producer) | 

**Required** The service to call.

Enum values:

-   marketdata
    
-   metadata
    
-   account
    





 |  | XChangeService |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The XChange component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **Currency** (producer) Constant: [`HEADER_CURRENCY`](https://javadoc.io/doc/org.apache.camel/camel-xchange/latest/org/apache/camel/component/xchange/XChangeConfiguration.html#HEADER_CURRENCY) | The target currency. |  | Currency |
| **CurrencyPair** (producer) Constant: [`HEADER_CURRENCY_PAIR`](https://javadoc.io/doc/org.apache.camel/camel-xchange/latest/org/apache/camel/component/xchange/XChangeConfiguration.html#HEADER_CURRENCY_PAIR) | The target currency pair. |  | CurrencyPair |

## Usage

### Authentication

This component communicates with supported cryptocurrency exchanges via REST API. Some API requests use simple unauthenticated GET request. For most of the interesting stuff, however, you’d need an account with the exchange and have API access keys enabled.

These API access keys need to be guarded tightly, especially so when they also allow for the withdraw functionality. In which case, anyone who can get hold of your API keys can easily transfer funds from your account to some other address i.e. steal your money.

Your API access keys can be stored in an exchange specific properties file in your SSH directory. For Binance, for example, this would be: `~/.ssh/binance-secret.keys`

##
# This file MUST NEVER be commited to source control.
# It is therefore added to .gitignore.
#
apiKey = GuRW0\*\*\*\*\*\*\*\*\*
secretKey = nKLki\*\*\*\*\*\*\*\*\*\*\*\*

## Examples

In this sample we find the current Bitcoin market price in USDT:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:ticker").to("xchange:binance?service=marketdata&method=ticker&currencyPair=BTC/USDT");
```

```xml
<route>
  <from uri="direct:ticker"/>
  <to uri="xchange:binance?service=marketdata&amp;method=ticker&amp;currencyPair=BTC/USDT"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:ticker
      steps:
        - to:
            uri: xchange:binance
            parameters:
              service: marketdata
              method: ticker
              currencyPair: BTC/USDT
```
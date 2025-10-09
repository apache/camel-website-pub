# Geocoder

**Since Camel 2.12**

**Only producer is supported**

The Geocoder component is used for looking up geocodes (latitude and longitude) for a given address, or reverse lookup.

The component uses either a hosted [Nominatim server](https://github.com/openstreetmap/Nominatim) or the [Java API for Google Geocoder](https://code.google.com/p/geocoder-java/) library.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-geocoder</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

geocoder:address:name\[?options\]
geocoder:latlng:latitude,longitude\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Geocoder component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **geoApiContext** (advanced) | Configuration for Google maps API. |  | GeoApiContext |

## Endpoint Options

The Geocoder endpoint is configured using URI syntax:

geocoder:address:latlng

with the following path and query parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **address** (producer) | The geo address which should be prefixed with address:. |  | String |
| **latlng** (producer) | The geo latitude and longitude which should be prefixed with latlng:. |  | String |

### Query Parameters (15 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **headersOnly** (producer) | Whether to only enrich the Exchange with headers, and leave the body as-is. | false | boolean |
| **language** (producer) | The language to use. | en | String |
| **serverUrl** (producer) | URL to the geocoder server. Mandatory for Nominatim server. |  | String |
| **type** (producer) | 
Type of GeoCoding server. Supported Nominatim and Google.

Enum values:

-   NOMINATIM
    
-   GOOGLE
    





 |  | GeoCoderType |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **proxyAuthDomain** (proxy) | Proxy Authentication Domain to access Google GeoCoding server. |  | String |
| **proxyAuthHost** (proxy) | Proxy Authentication Host to access Google GeoCoding server. |  | String |
| **proxyAuthMethod** (proxy) | Authentication Method to Google GeoCoding server. |  | String |
| **proxyAuthPassword** (proxy) | Proxy Password to access GeoCoding server. |  | String |
| **proxyAuthUsername** (proxy) | Proxy Username to access GeoCoding server. |  | String |
| **proxyHost** (proxy) | Proxy Host to access GeoCoding server. |  | String |
| **proxyPort** (proxy) | Proxy Port to access GeoCoding server. |  | Integer |
| **apiKey** (security) | API Key to access Google. Mandatory for Google GeoCoding server. |  | String |
| **clientId** (security) | Client ID to access Google GeoCoding server. |  | String |
| **clientKey** (security) | Client Key to access Google GeoCoding server. |  | String |

## Exchange data format

## Message Headers

The Geocoder component supports 11 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGeoCoderAddress** (producer) Constant: [`ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#ADDRESS) | The formatted address. |  | String |
| **CamelGeoCoderLatlng** (producer) Constant: [`LATLNG`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#LATLNG) | The latitude and longitude of the location. Separated by comma. |  | String |
| **CamelGeoCoderLat** (producer) Constant: [`LAT`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#LAT) | The latitude of the location. |  | String |
| **CamelGeoCoderLng** (producer) Constant: [`LNG`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#LNG) | The longitude of the location. |  | String |
| **CamelGeoCoderStatus** (producer) Constant: [`STATUS`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#STATUS) | 
**Required** Status code from the geocoder library. If status is GeocoderStatus.OK then additional headers is enriched.

Enum values:

-   ERROR
    
-   INVALID\_REQUEST
    
-   ACCESS\_NOT\_CONFIGURED
    
-   OK
    
-   OVER\_QUERY\_LIMIT
    
-   OVER\_DAILY\_LIMIT
    
-   REQUEST\_DENIED
    
-   UNKNOWN\_ERROR
    
-   ZERO\_RESULTS
    





 |  | GeocoderStatus |
| **CamelGeoCoderRegionCode** (producer) Constant: [`REGION_CODE`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#REGION_CODE) | The region code. |  | String |
| **CamelGeoCoderRegionName** (producer) Constant: [`REGION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#REGION_NAME) | The region name. |  | String |
| **CamelGeoCoderCity** (producer) Constant: [`CITY`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#CITY) | The city long name. |  | String |
| **CamelGeoCoderCountryLong** (producer) Constant: [`COUNTRY_LONG`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#COUNTRY_LONG) | The country long name. |  | String |
| **CamelGeoCoderCountryShort** (producer) Constant: [`COUNTRY_SHORT`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#COUNTRY_SHORT) | The country short name. |  | String |
| **CamelGeoCoderPostalCode** (producer) Constant: [`POSTAL_CODE`](https://javadoc.io/doc/org.apache.camel/camel-geocoder/latest/org/apache/camel/component/geocoder/GeoCoderConstants.html#POSTAL_CODE) | The postal code. |  | String |

Notice not all headers may be provided depending on available data and mode in use (address vs latlng).

### Body using a Nominatim Server

Camel will deliver the body as a JSONv2 type.

### Body using a Google Server

Camel will deliver the body as a `com.google.code.geocoder.model.GeocodeResponse` type.  
And if the address is `"current"` then the response is a String type with a JSON representation of the current location.

If the option `headersOnly` is set to `true` then the message body is left as-is, and only headers will be added to the Exchange.

## Samples

In the example below we get the latitude and longitude for Paris, France

```java
from("direct:start")
    .to("geocoder:address:Paris, France?type=NOMINATIM&serverUrl=https://nominatim.openstreetmap.org")
```

If you provide a header with the `CamelGeoCoderAddress` then that overrides the endpoint configuration, so to get the location of Copenhagen, Denmark we can send a message with a headers as shown:

```java
template.sendBodyAndHeader("direct:start", "Hello", GeoCoderConstants.ADDRESS, "Copenhagen, Denmark");
```

To get the address for a latitude and longitude we can do:

```java
from("direct:start")
    .to("geocoder:latlng:40.714224,-73.961452")
    .log("Location ${header.CamelGeocoderAddress} is at lat/lng: ${header.CamelGeocoderLatlng} and in country ${header.CamelGeoCoderCountryShort}")
```

Which will log

Location 285 Bedford Avenue, Brooklyn, NY 11211, USA is at lat/lng: 40.71412890,-73.96140740 and in country US

To get the current location using the Google GeoCoder, you can use "current" as the address as shown:

```java
from("direct:start")
    .to("geocoder:address:current")
```

## Spring Boot Auto-Configuration

When using geocoder with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-geocoder-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.geocoder.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.geocoder.enabled** | Whether to enable auto configuration of the geocoder component. This is enabled by default. |  | Boolean |
| **camel.component.geocoder.geo-api-context** | Configuration for Google maps API. The option is a com.google.maps.GeoApiContext type. |  | GeoApiContext |
| **camel.component.geocoder.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
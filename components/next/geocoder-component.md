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

The Geocoder component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **geoApiContext** (advanced) | Configuration for Google maps API. |  | GeoApiContext |

## Endpoint Options

The Geocoder endpoint is configured using URI syntax:

geocoder:address:latlng

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **address** (producer) | The geo address which should be prefixed with address:. |  | String |
| **latlng** (producer) | The geo latitude and longitude which should be prefixed with latlng:. |  | String |

### Query Parameters

   
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

## Message Headers

The Geocoder component supports the following message header(s), which is/are listed below:

   
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

## Message Body

The message body at each side of the Geocoder component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | The body is not read: the address or the latitude and longitude come from the CamelGeoCoderAddress or CamelGeoCoderLatlng header, or else from the endpoint. |
| **Producer output** | `list` or `unchanged` | 
With Google, the array of com.google.maps.model.GeocodingResult, empty for no results; unchanged when Google denies the request, with the status in the CamelGeoCoderStatus header. With Nominatim, its jsonv2 response as text: an array of one place for an address, an object for a latitude and longitude. The first result is also in the headers.

-   With `type=NOMINATIM`: `text` (`java.lang.String`)
    
-   With `headersOnly=true`: `unchanged`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

## Exchange data format

Notice not all headers may be provided depending on available data and mode in use (`address` vs. `latlng`).

### Body using a Nominatim Server

Camel will deliver the body as a String with the JSON response of Nominatim (the `jsonv2` format): an array with one place for an address, and an object for a latitude and longitude.

### Body using a Google Server

Camel will deliver the body as an array of `com.google.maps.model.GeocodingResult` (empty when there are no results).  
If the address is `"current"` then the current location is found by geolocation, and the body is the array of `GeocodingResult` of that location as well. When Google denies the request, the body is left as-is and the `CamelGeoCoderStatus` header has the status.

If the option `headersOnly` is set to `true` then the message body is left as-is, and only headers will be added to the Exchange.

## Examples

In the example below, we get the latitude and longitude for Paris, France

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("geocoder:address:Paris, France?type=NOMINATIM&serverUrl=https://nominatim.openstreetmap.org");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="geocoder:address:Paris, France?type=NOMINATIM&amp;serverUrl=https://nominatim.openstreetmap.org"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "geocoder:address:Paris, France"
            parameters:
              type: NOMINATIM
              serverUrl: "https://nominatim.openstreetmap.org"
```

If you provide a header with the `CamelGeoCoderAddress` then that overrides the endpoint configuration, so to get the location of Copenhagen, Denmark we can send a message with a headers as shown:

_Java-only: overriding the address via a message header_

```java
template.sendBodyAndHeader("direct:start", "Hello", "CamelGeoCoderAddress", "Copenhagen, Denmark");
```

To get the address for a latitude and longitude we can do:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("geocoder:latlng:40.714224,-73.961452")
    .log("Location ${header.CamelGeoCoderAddress} is at lat/lng: ${header.CamelGeoCoderLatlng} and in country ${header.CamelGeoCoderCountryShort}");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="geocoder:latlng:40.714224,-73.961452"/>
  <log message="Location ${header.CamelGeoCoderAddress} is at lat/lng: ${header.CamelGeoCoderLatlng} and in country ${header.CamelGeoCoderCountryShort}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "geocoder:latlng:40.714224,-73.961452"
        - log:
            message: "Location ${header.CamelGeoCoderAddress} is at lat/lng: ${header.CamelGeoCoderLatlng} and in country ${header.CamelGeoCoderCountryShort}"
```

Which will log

Location 285 Bedford Avenue, Brooklyn, NY 11211, USA is at lat/lng: 40.71412890,-73.96140740 and in country US

To get the current location using the Google GeoCoder, you can use "current" as the address as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("geocoder:address:current");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="geocoder:address:current"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: geocoder:address:current
```
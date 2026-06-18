# SAP NetWeaver

**Since Camel 2.12**

**Only producer is supported**

The SAP Netweaver integrates with the [SAP NetWeaver Gateway](http://scn.sap.com/community/developer-center/netweaver-gateway) using HTTP transports.

This camel component supports only producer endpoints.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-sap-netweaver</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

The URI scheme for a sap netweaver gateway component is as follows

sap-netweaver:https://host:8080/path?username=foo&password=secret

## Prerequisites

You would need to have an account on the SAP NetWeaver system to be able to leverage this component. SAP provides a [demo setup](http://scn.sap.com/docs/DOC-31221#section6) where you can request an account.

This component uses the basic authentication scheme for logging into SAP NetWeaver.

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

The SAP NetWeaver component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The SAP NetWeaver endpoint is configured using URI syntax:

sap-netweaver:url

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **url** (producer) | **Required** Url to the SAP net-weaver gateway server. |  | String |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **flatternMap** (producer) | If the JSON Map contains only a single entry, then flattern by storing that single entry value as the message body. | true | boolean |
| **json** (producer) | Whether to return data in JSON format. If this option is false, then XML is returned in Atom format. | true | boolean |
| **jsonAsMap** (producer) | To transform the JSON from a String to a Map in the message body. | true | boolean |
| **password** (producer) | **Required** Password for account. |  | String |
| **username** (producer) | **Required** Username for account. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The SAP NetWeaver component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelNetWeaverCommand** (producer) Constant: [`COMMAND`](https://javadoc.io/doc/org.apache.camel/camel-sap-netweaver/latest/org/apache/camel/component/sap/netweaver/NetWeaverConstants.html#COMMAND) | **Required** The command to execute in [http://msdn.microsoft.com/en-us/library/cc956153.aspxMS](http://msdn.microsoft.com/en-us/library/cc956153.aspxMS) ADO.Net Data Service format. |  | String |
| **CamelHttpPath** (producer) Constant: [`HTTP_PATH`](https://javadoc.io/doc/org.apache.camel/camel-sap-netweaver/latest/org/apache/camel/component/sap/netweaver/NetWeaverConstants.html#HTTP_PATH) | The http path. |  | String |
| **Accept** (producer) Constant: [`ACCEPT`](https://javadoc.io/doc/org.apache.camel/camel-sap-netweaver/latest/org/apache/camel/component/sap/netweaver/NetWeaverConstants.html#ACCEPT) | The media type. |  | String |

## Examples

This example is using the flight demo example from SAP, which is available online over the internet [here](http://scn.sap.com/docs/DOC-31221).

In the route below we request the SAP NetWeaver demo server using the following url

https://sapes4.sapdevcenter.com/sap/opu/odata/IWFND/RMTSAMPLEFLIGHT

And we want to execute the following command

```text
FlightCollection(carrid='AA',connid='0017',fldate=datetime'2016-04-20T00%3A00%3A00')
```

To get flight details for the given flight. The command syntax is in [MS ADO.Net Data Service](http://msdn.microsoft.com/en-us/library/cc956153.aspx) format.

We have the following Camel route

_Java-only: route using Java constants and toF() string formatting_

```java
from("direct:start")
    .setHeader(NetWeaverConstants.COMMAND, constant(command))
    .toF("sap-netweaver:%s?username=%s&password=%s", url, username, password)
    .to("log:response")
    .to("velocity:flight-info.vm")
```

Where `url`, `username`, `password` and `command` are defined as:

_Java-only: Java field definitions_

```java
private String username = "P1909969254";
private String password = "TODO";
private String url = "https://sapes4.sapdevcenter.com/sap/opu/odata/IWFND/RMTSAMPLEFLIGHT";
private String command = "FlightCollection(carrid='AA',connid='0017',fldate=datetime'2016-04-20T00%3A00%3A00')";
```

The password is invalid. You would need to create an account at SAP first to run the demo.

The velocity template is used for formatting the response to a basic HTML page

```xml
<html>
  <body>
  Flight information:

  <p/>
  <br/>Airline ID: $body["AirLineID"]
  <br/>Aircraft Type: $body["AirCraftType"]
  <br/>Departure city: $body["FlightDetails"]["DepartureCity"]
  <br/>Departure airport: $body["FlightDetails"]["DepartureAirPort"]
  <br/>Destination city: $body["FlightDetails"]["DestinationCity"]
  <br/>Destination airport: $body["FlightDetails"]["DestinationAirPort"]

  </body>
</html>
```

When running the application, you get sample output:

Flight information:
Airline ID: AA
Aircraft Type: 747-400
Departure city: new york
Departure airport: JFK
Destination city: SAN FRANCISCO
Destination airport: SFO

## Spring Boot Auto-Configuration

When using sap-netweaver with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-sap-netweaver-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.sap-netweaver.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.sap-netweaver.enabled** | Whether to enable auto configuration of the sap-netweaver component. This is enabled by default. |  | Boolean |
| **camel.component.sap-netweaver.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
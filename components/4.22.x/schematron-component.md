# Schematron

**Since Camel 2.15**

**Only producer is supported**

[Schematron](http://www.schematron.com/index.md) is an XML-based language for validating XML instance documents. It is used to make assertions about data in an XML document, and it is also used to express operational and business rules. Schematron is an [ISO Standard](http://standards.iso.org/ittf/PubliclyAvailableStandards/index.md). The schematron component uses the leading [implementation](http://www.schematron.com/implementation.md) of ISO schematron. It is an XSLT based implementation. The schematron rules are run through [four XSLT pipelines](http://www.schematron.com/implementation.md), which generates a final XSLT which will be used as the basis for running the assertion against the XML document. The component is written in a way that Schematron rules are loaded at the start of the endpoint (only once) this is to minimize the overhead of instantiating a Java Templates object representing the rules.

## URI format

schematron://path?\[options\]

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

The Schematron component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Schematron endpoint is configured using URI syntax:

schematron:path

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **path** (producer) | **Required** The path to the schematron rules file. Can either be in class path or location in the file system. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **abort** (producer) | Flag to abort the route and throw a schematron validation exception. | false | boolean |
| **rules** (producer) | To use the given schematron rules instead of loading from the path. |  | Templates |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **uriResolver** (advanced) | Set the URIResolver to be used for resolving schematron includes in the rules file. |  | URIResolver |

## Headers

   
| Name | Description | Type | In/Out |
| --- | --- | --- | --- |
| CamelSchematronValidationStatus | The schematron validation status: SUCCESS / FAILED | String | IN |
| CamelSchematronValidationReport | The schematron report body in XML format. See an example below | String | IN |

## Examples

### URI and path syntax

The following example shows how to invoke the schematron processor. The schematron rules file is sourced from the class path:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start").to("schematron://sch/schematron.sch").to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="schematron://sch/schematron.sch"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: schematron://sch/schematron.sch
        - to:
            uri: mock:result
```

The following example shows a more advanced route with validation and error handling. The schematron rules file is sourced from the file system:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("schematron:///usr/local/sch/schematron.sch")
    .log("Schematron validation status: ${in.header.CamelSchematronValidationStatus}")
    .choice()
        .when(simple("${in.header.CamelSchematronValidationStatus} == 'SUCCESS'"))
            .to("mock:success")
        .otherwise()
            .log("Failed schematron validation")
            .setBody(header("CamelSchematronValidationReport"))
            .to("mock:failure");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="schematron:///usr/local/sch/schematron.sch"/>
  <log message="Schematron validation status: ${in.header.CamelSchematronValidationStatus}"/>
  <choice>
    <when>
      <simple>${in.header.CamelSchematronValidationStatus} == 'SUCCESS'</simple>
      <to uri="mock:success"/>
    </when>
    <otherwise>
      <log message="Failed schematron validation"/>
      <setBody>
        <header>CamelSchematronValidationReport</header>
      </setBody>
      <to uri="mock:failure"/>
    </otherwise>
  </choice>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: schematron:///usr/local/sch/schematron.sch
        - log:
            message: "Schematron validation status: ${in.header.CamelSchematronValidationStatus}"
        - choice:
            when:
              - simple: "${in.header.CamelSchematronValidationStatus} == 'SUCCESS'"
                steps:
                  - to:
                      uri: mock:success
            otherwise:
              steps:
                - log:
                    message: Failed schematron validation
                - setBody:
                    expression:
                      header:
                        expression: CamelSchematronValidationReport
                - to:
                    uri: mock:failure
```

> **Tip**
> **Where to store schematron rules?**
>
> Schematron rules can change with business requirement, as such it is recommended to store these rules somewhere in a file system. When the schematron component endpoint is started, the rules are compiled into XSLT as a Java Templates Object. This is done only once to minimize the overhead of instantiating Java Templates object, which can be an expensive operation for a large set of rules and given that the process goes through four pipelines of [XSLT transformations](http://www.schematron.com/implementation.md). So if you happen to store the rules in the file system, in the event of an update, all you need is to restart the route or the component. No harm in storing these rules in the class path though, but you will have to build and deploy the component to pick up the changes.

### Schematron rules and report examples

Here is an example of schematron rules

```xml
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://purl.oclc.org/dsdl/schematron">
   <title>Check Sections 12/07</title>
   <pattern id="section-check">
      <rule context="section">
         <assert test="title">This section has no title</assert>
         <assert test="para">This section has no paragraphs</assert>
      </rule>
   </pattern>
</schema>
```

Here is an example of schematron report:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svrl:schematron-output xmlns:svrl="http://purl.oclc.org/dsdl/svrl"
 xmlns:iso="http://purl.oclc.org/dsdl/schematron"
 xmlns:saxon="http://saxon.sf.net/"
 xmlns:schold="http://www.ascc.net/xml/schematron"
 xmlns:xhtml="http://www.w3.org/1999/xhtml"
 xmlns:xs="http://www.w3.org/2001/XMLSchema"
 xmlns:xsd="http://www.w3.org/2001/XMLSchema" schemaVersion="" title="">

   <svrl:active-pattern document="" />
   <svrl:fired-rule context="chapter" />
   <svrl:failed-assert test="title" location="/doc[1]/chapter[1]">
      <svrl:text>A chapter should have a title</svrl:text>
   </svrl:failed-assert>
   <svrl:fired-rule context="chapter" />
   <svrl:failed-assert test="title" location="/doc[1]/chapter[2]">
      <svrl:text>A chapter should have a title</svrl:text>
   </svrl:failed-assert>
   <svrl:fired-rule context="chapter" />
</svrl:schematron-output>
```

> **Tip**
> **Useful Links and resources**
>
> -   [Introduction to Schematron](http://www.mulberrytech.com/papers/schematron-Philly.pdf) by Mulleberry technologies. An excellent document in PDF to get you started on Schematron.
>     
> -   [Schematron official site](http://www.schematron.com). This contains links to other resources
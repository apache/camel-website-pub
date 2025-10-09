# RSS

**Since Camel 2.1**

The RSS component ships with an RSS dataformat that can be used to convert between String (as XML) and ROME RSS model objects.

-   marshal = from ROME `SyndFeed` to XML `String`
    
-   unmarshal = from XML `String` to ROME `SyndFeed`
    

A route using this would look something like this:

The purpose of this feature is to make it possible to use Camel’s lovely built-in expressions for manipulating RSS messages. As shown below, an XPath expression can be used to filter the RSS message:

> **Tip**
> **Query parameters**
>
> If the URL for the RSS feed uses query parameters, this component will understand them as well, for example if the feed uses `alt=rss`, then you can for example do `from("rss:http://someserver.com/feeds/posts/default?alt=rss&splitEntries=false&delay=1000").to("bean:rss");`

## Options

The RSS dataformat has no options.

## Example

The RSS component ships with an RSS dataformat that can be used to convert between String (as XML) and ROME RSS model objects.

-   marshal = from ROME `SyndFeed` to XML `String`
    
-   unmarshal = from XML `String` to ROME `SyndFeed`
    

A route using the RSS dataformat will look like this:

```java
from("rss:file:src/test/data/rss20.xml?splitEntries=false&delay=1000")
  .marshal().rss()
  .to("mock:marshal");
```

The purpose of this feature is to make it possible to use Camel’s built-in expressions for manipulating RSS messages. As shown below, an XPath expression can be used to filter the RSS message. In the following example, on ly entries with Camel in the title will get through the filter.

```java
from("rss:file:src/test/data/rss20.xml?splitEntries=true&delay=100")
  .marshal().rss()
  .filter().xpath("//item/title[contains(.,'Camel')]")
    .to("mock:result");
```

## Spring Boot Auto-Configuration

When using rss with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-rss-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.rss.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.rss.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.rss.enabled** | Whether to enable auto configuration of the rss component. This is enabled by default. |  | Boolean |
| **camel.dataformat.rss.enabled** | Whether to enable auto configuration of the rss data format. This is enabled by default. |  | Boolean |
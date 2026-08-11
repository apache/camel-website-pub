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

The RSS dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |

## Example

The RSS component ships with an RSS dataformat that can be used to convert between String (as XML) and ROME RSS model objects.

-   marshal = from ROME `SyndFeed` to XML `String`
    
-   unmarshal = from XML `String` to ROME `SyndFeed`
    

A route using the RSS dataformat will look like this:

-   Java
    
-   XML
    
-   YAML
    

```java
from("rss:file:src/test/data/rss20.xml?splitEntries=false&delay=1000")
    .marshal().rss()
    .to("mock:marshal");
```

```xml
<route>
  <from uri="rss:file:src/test/data/rss20.xml?splitEntries=false&amp;delay=1000"/>
  <marshal><rss/></marshal>
  <to uri="mock:marshal"/>
</route>
```

```yaml
- route:
    from:
      uri: rss:file:src/test/data/rss20.xml
      parameters:
        splitEntries: false
        delay: 1000
      steps:
        - marshal:
            rss: {}
        - to:
            uri: mock:marshal
```

The purpose of this feature is to make it possible to use Camel’s built-in expressions for manipulating RSS messages. As shown below, an XPath expression can be used to filter the RSS message. In the following example, only entries with Camel in the title will get through the filter.

-   Java
    
-   XML
    
-   YAML
    

```java
from("rss:file:src/test/data/rss20.xml?splitEntries=true&delay=100")
    .marshal().rss()
    .filter().xpath("//item/title[contains(.,'Camel')]")
        .to("mock:result");
```

```xml
<route>
  <from uri="rss:file:src/test/data/rss20.xml?splitEntries=true&amp;delay=100"/>
  <marshal><rss/></marshal>
  <filter>
    <xpath>//item/title[contains(.,'Camel')]</xpath>
    <to uri="mock:result"/>
  </filter>
</route>
```

```yaml
- route:
    from:
      uri: rss:file:src/test/data/rss20.xml
      parameters:
        splitEntries: true
        delay: 100
      steps:
        - marshal:
            rss: {}
        - filter:
            xpath: "//item/title[contains(.,'Camel')]"
            steps:
              - to:
                  uri: mock:result
```
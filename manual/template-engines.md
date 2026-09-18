# Template engines

A template engine is a tool that generates text output, such as emails, XML, JSon or code, by combining templates with dynamic data. In Camel, templates are primarily used to create layouts while dynamically using data from the current [Message Exchange](exchange.md).

Below is a list of some of the template engines that are provided by Camel:

  
| Template | Artifact | Description |
| --- | --- | --- |
| [Chunk](../components/4.22.x/chunk-component.md) | camel-chunk | Transform messages using Chunk templating engine. |
| [Freemarker](../components/4.22.x/freemarker-component.md) | camel-freemarker | Transform messages using FreeMarker templates. |
| [JTE](../components/4.22.x/jte-component.md) | camel-jte | Transform messages using a Java based template engine (JTE). |
| [Mustache](../components/4.22.x/mustache-component.md) | camel-mustache | Transform messages using a Mustache template. |
| [MVEL](../components/4.22.x/mvel-component.md) | camel-mvel | Transform messages using an MVEL template. |
| [String Template](../components/4.22.x/string-template-component.md) | camel-stringtemplate | Transform messages using StringTemplate engine. |
| [Thymeleaf](../components/4.22.x/thymeleaf-component.md) | camel-thymeleaf | Transform messages using a Thymeleaf template. |
| [Velocity](../components/4.22.x/velocity-component.md) | camel-velocity | Transform messages using a Velocity template. |
| [XSLT](../components/4.22.x/xslt-component.md) | camel-xslt | Transforms XML payload using an XSLT template. |
| [XSLT Saxon](../components/4.22.x/xslt-saxon-component.md) | camel-xslt-saxon | Transform XML payloads using an XSLT template using Saxon. |
> **Tip**
> To see a wider list try Camel CLI to execute: `camel catalog component --filter=transform` from the CLI.

## Which template engine to choose

Velocity is a mature template engine with long-term support from Camel. It can be used for text generation, such as emails. Mustache can be used for similar purposes and is cross-platform.

For templates that require more conditional logic and XML or HTML output, Freemarker, MVEL, and Thymeleaf are good choices. JTE is known to be fast due to its compile-time template processing.

> **Note**
> These template engines perform directly on the Exchange, if you want to template routes, look at [Route Templates](route-template.md).
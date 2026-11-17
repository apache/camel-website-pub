# Remove Headers

The Remove Headers EIP allows you to remove one or more headers from the [Message](message.md), based on pattern syntax.

## Options

The Remove Headers eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **pattern** | **Required** Name or pattern of headers to remove. The pattern supports exact match, wildcard (pattern ends with \*), and regular expression (all case-insensitive). |  | String |
| **excludePattern** | Name or pattern of headers to not remove. The pattern supports exact match, wildcard (pattern ends with \*), and regular expression (all case-insensitive). To keep several headers, use a regular expression such as header1|header3. |  | String |

## Message Body

The message body at each side of the Remove Headers EIP: _EIP input_ is the body it needs, _EIP output_ the body after it, and _Steps_ the body its own steps start with.

  
| Side | Body | Description |
| --- | --- | --- |
| **EIP output** | `unchanged` | Removes headers: the body stays as it was. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../../manual/body-types.md).

## Exchange properties

The Remove Headers eip has no exchange properties.

## Remove Headers by pattern

The Remove Headers EIP supports pattern matching by the following rules in the given order:

-   match by exact name
    
-   match by wildcard
    
-   match by regular expression
    

## Remove all headers

To remove all headers you can use `*` as the pattern:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:b")
  .removeHeaders("*")
  .to("mock:result");
```

```xml
<route>
  <from uri="seda:b"/>
  <removeHeaders pattern="*"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:b
      steps:
        - removeHeaders:
            pattern: "*"
        - to:
            uri: mock:result
```

## Remove all Camel headers

To remove all headers that start with `Camel` then use `Camel*` as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:b")
  .removeHeaders("Camel*")
  .to("mock:result");
```

```xml
<route>
  <from uri="seda:b"/>
  <removeHeaders pattern="Camel*"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:b
      steps:
        - removeHeaders: "Camel*"
        - to:
            uri: mock:result
```

## Keeping some headers

The `excludePattern` option keeps the headers it matches, with the same rules as `pattern`. It is a single pattern: to keep several headers, use a regular expression with `|` (a comma does not separate patterns). In Java, you can also give several exclude patterns as arguments.

The following removes all headers, except `header1`, `header3` and the headers that start with `Camel`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:b")
  .removeHeaders("*", "header1", "header3", "Camel*")
  .to("mock:result");
```

```xml
<route>
  <from uri="seda:b"/>
  <removeHeaders pattern="*" excludePattern="header1|header3|Camel.*"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:b
      steps:
        - removeHeaders:
            pattern: "*"
            excludePattern: "header1|header3|Camel.*"
        - to:
            uri: mock:result
```

> **Note**
> Inside a regular expression, `Camel*` means `Came` followed by any number of `l`: use `Camel.*` to match the headers that start with `Camel`.

## Leaking Camel headers when sending to an endpoint

When I send a message to a Camel endpoint such as the [Mail](../../4.22.x/mail-component.md) component, then the mail include some message headers I do not want. How can I avoid this?

This is a gotcha more people encounter. However, it’s very easy to solve. To remove all headers (see above) use a `*` expression:

Most components will automatically remove all Camel specific headers (the header key starts with `Camel`) using the `DefaultHeaderFilterStrategy` which automatic removes these headers. However if you use a component that does not do this, such as a custom component, or a Camel component which has not been improved to do that, then you can remove all these Camel specific headers using `Camel*` with the `removeHeaders` EIP as shown previously on this page.

## See Also

Camel provides the following EIPs for removing headers or exchange properties:

-   [Remove Header](removeHeader-eip.md): To remove a single header
    
-   [Remove Headers](#): To remove one or more message headers
    
-   [Remove Property](removeProperty-eip.md): To remove a single exchange property
    
-   [Remove Properties](removeProperties-eip.md): To remove one or more exchange properties
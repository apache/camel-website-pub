# Remove Properties

The Remove Properties EIP allows you to remove one or more `Exchange` properties, based on pattern syntax.

## Options

The Remove Properties eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **pattern** | **Required** Name or pattern of properties to remove. The pattern is matched in the following order: 1 = exact match 2 = wildcard (pattern ends with a and the name starts with the pattern) 3 = regular expression (all of above is case in-sensitive). |  | String |
| **excludePattern** | Name or pattern of properties to not remove. The pattern is matched in the following order: 1 = exact match 2 = wildcard (pattern ends with a and the name starts with the pattern) 3 = regular expression (all of above is case in-sensitive). |  | String |

## Exchange properties

The Remove Properties eip has no exchange properties.

## Remove Exchange Properties by pattern

The Remove Properties EIP supports pattern matching by the following rules in the given order:

-   match by exact name
    
-   match by wildcard
    
-   match by regular expression
    

## Remove all properties

For example to remove all properties use \* as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:b")
  .removeProperties("*")
  .to("mock:result");
```

```xml
<route>
  <from uri="seda:b"/>
  <removeProperties pattern="*"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- from:
    uri: seda:b
    steps:
      - removeProperties:
          pattern: "*"
      - to:
          uri: mock:result
```

> **Important**
> Be careful to remove all exchange properties as Camel uses internally exchange properties to keep state on the `Exchange` during routing. So use this with care. You should generally only remove custom exchange properties that are under your own control.

## Remove properties by pattern

To remove all exchange properties that start with `Foo` then use `Foo*` as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:b")
  .removeProperties("Foo*")
  .to("mock:result");
```

```xml
<route>
  <from uri="seda:b"/>
  <removeProperties pattern="Foo*"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- from:
    uri: seda:b
    steps:
      - removeProperties:
          pattern: "Foo*"
      - to:
          uri: mock:result
```

## See Also

Camel provides the following EIPs for removing headers or exchange properties:

-   [Remove Header](removeHeader-eip.md): To remove a single header
    
-   [Remove Headers](removeHeaders-eip.md): To remove one or more message headers
    
-   [Remove Property](removeProperty-eip.md): To remove a single exchange property
    
-   [Remove Properties](#): To remove one or more exchange properties
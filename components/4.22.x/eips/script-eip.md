# Script

The Script EIP is used for executing a coding script.

![image](_images/eip/MessagingGatewayIcon.gif)

This is useful when you need to invoke some logic not in Java code such as JavaScript, Groovy or any of the other Languages.

> **Note**
> The returned value from the script is discarded and not used. If the returned value should be set as the new message body, then use the [Message Translator](message-translator.md) EIP instead.

## Options

The Script eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **expression** | **Required** The expression to evaluate as a script. The script result does not change the message body (use transform instead if that is desired). |  | ExpressionDefinition |

## Exchange properties

The Script eip has no exchange properties.

## Using Script EIP

The route below will read the file contents and call a groovy script

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
  .script().groovy("some groovy code goes here")
  .to("bean:myServiceBean.processLine");
```

```xml
<route>
  <from uri="file:inbox"/>
  <script>
    <groovy>some groovy code goes here</groovy>
  </script>
  <to uri="bean:myServiceBean.processLine"/>
</route>
```

Mind that you can use _CDATA_ if the script uses `< >` etc:

```xml
<route>
  <from uri="file://inbox"/>
  <script>
    <groovy><![CDATA[ some groovy script here that can be multiple lines and whatnot ]]></groovy>
  </script>
  <to uri="bean:myServiceBean.processLine"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - script:
            expression:
              groovy:
                expression: >
                 some groovy code goes here
                 that can be in multiple
                 lines and have a lot of code
        - to:
            uri: bean:myServiceBean.processLine
```

### Scripting Context

The scripting context has access to the current `Exchange` and can essentially change the message or headers directly.

### Using external script files

You can refer to external script files instead of inlining the script. For example, to load a groovy script from the classpath, you need to prefix the value with `resource:` as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
  .script().groovy("resource:classpath:com/foo/myscript.groovy")
  .to("bean:myServiceBean.processLine");
```

```xml
<route>
  <from uri="file:inbox"/>
  <script>
    <groovy>resource:classpath:com/foo/myscript.groovy</groovy>
  </script>
  <to uri="bean:myServiceBean.processLine"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - script:
            expression:
              groovy:
                expression: resource:classpath:com/foo/myscript.groovy
        - to:
            uri: bean:myServiceBean.processLine
```

You can also refer to the script from the file system with `file:` instead of `classpath:` such as `file:/var/myscript.groovy`
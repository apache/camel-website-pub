# Throw Exception

How can I throw an exception

![image](_images/eip/MessageExpirationIcon.gif)

Use a special processor to throw an exception.

## Options

The Throw Exception eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **message** | The message text for the exception to be thrown. Supports simple language expressions. |  | String |
| **exceptionType** | The fully qualified class name of the exception to throw. Used together with message. |  | String |
| **ref** | Reference to an existing exception instance to lookup from the registry and throw. |  | String |

## Message Body

The message body at each side of the Throw Exception EIP: _EIP input_ is the body it needs, _EIP output_ the body after it, and _Steps_ the body its own steps start with.

  
| Side | Body | Description |
| --- | --- | --- |
| **EIP output** | `unchanged` | Fails the exchange with the exception: the body stays as it was. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Exchange properties

The Throw Exception eip has no exchange properties.

## Using Throw Exception

In a specific situation we want to fail processing the current message by throwing an exception. In the [Content-Based Router](choice-eip.md) below we use `throwException` in such a case.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .choice()
        .when(simple("${body} contains 'Hello'")).to("mock:hello")
        .when(simple("${body} contains 'Bye'")).to("mock:bye").throwException(new IllegalArgumentException("Not allowed"))
        .otherwise().to("mock:other")
    .end()
.to("mock:result");
```

In XML you specify the FQN class name via `exceptionType` and the `message` is the caused text to include in the exception.

```xml
    <route>
        <from uri="direct:start"/>
        <choice>
            <when>
                <simple>${body} contains 'Hello'</simple>
                <to uri="mock:hello"/>
            </when>
            <when>
                <simple>${body} contains 'Bye'</simple>
                <to uri="mock:bye"/>
                <throwException exceptionType="java.lang.IllegalArgumentException" message="Not Allowed"/>
            </when>
            <otherwise>
                <to uri="mock:other"/>
            </otherwise>
        </choice>
        <to uri="mock:result"/>
    </route>
```

In YML you specify the FQN class name via `exceptionType` and the `message` is the caused text to include in the exception.

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - choice:
            when:
              - expression:
                  simple:
                    expression: "${body} contains 'Hello'"
                steps:
                  - to:
                      uri: mock:hello
              - expression:
                  simple:
                    expression: "${body} contains 'Bye'"
                steps:
                  - to:
                      uri: mock:bye
                  - throwException:
                      exceptionType: "java.lang.IllegalArgumentException"
                      message: "Not Allowed"
            otherwise:
              steps:
                - to:
                    uri: mock:other
        - to:
            uri: mock:result
```

## See Also

See also the related [Stop](stop-eip.md) EIP.
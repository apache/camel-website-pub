# Do Try

Camel supports the Java equivalent of try, catch, and finally directly in the DSL. It aims to work like its Java sisters but with more power.

In Camel, we prefix the keywords with `do` to avoid having same keyword as Java. So we have:

-   `doTry`
    
-   `doCatch`
    
-   `doFinally`
    
-   `end` to end the block in Java DSL
    

> **Important**
> When using `doTry …​ doCatch …​ doFinally`, the regular Camel [Error Handler](../../../manual/error-handler.md) is not in use; meaning any `onException` or the likes does not trigger.
>
> The reason is that `doTry …​ doCatch …​ doFinally` is in fact its own error handler and mimics how try/catch/finally works in Java.

## EIP options

The Do Try eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **outputs** | **Required** |  | List |
| **doCatch** | Catches exceptions as part of a try, catch, finally block. |  | List |
| **doFinally** | Path traversed when a try, catch, finally block exits. |  | FinallyDefinition |

## Using doTry …​ doCatch …​ doFinally

In the route below we have all of them in action:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .doTry()
        .process(new ProcessorFail())
        .to("mock:result")
    .doCatch(IOException.class, IllegalStateException.class)
        .to("mock:catch")
    .doFinally()
        .to("mock:finally")
    .end();
```

```xml
<route>
  <from uri="direct:start"/>
  <doTry>
    <process ref="processorFail"/>
    <to uri="mock:result"/>
    <doCatch>
      <exception>java.io.IOException</exception>
      <exception>java.lang.IllegalStateException</exception>
      <to uri="mock:catch"/>
    </doCatch>
    <doFinally>
       <to uri="mock:finally"/>
    </doFinally>
  </doTry>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - doTry:
            steps:
              - process:
                  ref: processorFail
              - to:
                  uri: mock:result
              - doCatch:
                  exception:
                    - java.io.IOException
                    - java.lang.IllegalStateException
                  steps:
                    - to:
                        uri: mock:catch
              - doFinally:
                  steps:
                    - to:
                        uri: mock:finally
```

### Using onWhen with doCatch

You can use [Predicates](../../../manual/predicate.md) with `doCatch` to make it determine at runtime if the block should be triggered or not. In this example, we only want to trigger if the caused exception message contains the word **Damn**.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .doTry()
        .process(new ProcessorFail())
        .to("mock:result")
    .doCatch(IOException.class, IllegalStateException.class)
        .onWhen(exceptionMessage().contains("Damn"))
        .to("mock:catch")
    .doCatch(CamelExchangeException.class)
        .to("mock:catchCamel")
    .doFinally()
        .to("mock:finally")
    .end();
```

```xml
<route>
  <from uri="direct:start"/>
  <doTry>
    <process ref="processorFail"/>
    <to uri="mock:result"/>
    <doCatch>
      <exception>java.io.IOException</exception>
      <exception>java.lang.IllegalStateException</exception>
      <onWhen>
        <simple>${exception.message} contains 'Damn'</simple>
      </onWhen>
      <to uri="mock:catch"/>
    </doCatch>
    <doCatch>
      <exception>org.apache.camel.CamelExchangeException</exception>
      <to uri="mock:catchCamel"/>
    </doCatch>
    <doFinally>
       <to uri="mock:finally"/>
    </doFinally>
  </doTry>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - doTry:
            steps:
              - process:
                  ref: processorFail
              - to:
                  uri: mock:result
              - doCatch:
                  exception:
                    - java.io.IOException
                    - java.lang.IllegalStateException
                  steps:
                    - onWhen:
                        expression:
                          simple:
                            expression: "${exception.message} contains 'Damn'"
                    - to:
                        uri: mock:catch
              - doCatch:
                  exception:
                    - org.apache.camel.CamelExchangeException
                  steps:
                    - to:
                        uri: mock:catchCamel
              - doFinally:
                  steps:
                    - to:
                        uri: mock:finally
```

### Use end() to end the block

When using Java DSL you must use `end()` to indicate where the try …​ catch …​ finally block ends. If the route has a `doFinally`, then the `end()` should be at the end of the finally block. If there is no `doFinally`, then the `end()` should be at the end of the last `doCatch`.

> **Tip**
> Instead of `end()` you can use `endDoTry()` to end and _return back_ to the try …​ catch scope.

### Nested doTry …​ doCatch

When nesting `doTry …​ doCatch` from an outer `doTry …​ doCatch` EIP, pay extra attention when using Java DSL as the Java programming language is not _indent aware_ so you may write code that is indented in a way where you think a catch block is associated with the other doTry, but it is not.

Given the following Java DSL:

```java
from("direct:test")
    .doTry().
        doTry().
            throwException(new IllegalArgumentException("Forced by me"))
        .doCatch(Exception.class)
            .log("docatch 1")
            .throwException(new IllegalArgumentException("Second forced by me"))
    .doCatch(Exception.class)
        .log("docatch 2")
    .end();
```

Both `docatch 1` and `docatch 2` are in the inner `doTry`, and the outer `doTry` has no catch blocks. Use `endDoTry()` to end the blocks correctly:

```java
from("direct:test")
    .doTry().
        doTry().
            throwException(new IllegalArgumentException("Forced by me"))
        .doCatch(Exception.class)
            .log("docatch 1")
            .throwException(new IllegalArgumentException("Second forced by me"))
         .endDoTry() // end this doCatch block
     .endDoTry() // end the inner doTry
    .doCatch(Exception.class)
        .log("docatch 2")
    .end();
```
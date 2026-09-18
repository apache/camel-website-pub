# Writing Integrations in XML

Camel K support the classic XML DSL available in Camel:

example.xml

```xml
<routes xmlns="http://camel.apache.org/schema/spring">
    <route>
        <from uri="timer:tick"/>
        <setBody>
            <constant>Hello Camel K!</constant>
         </setBody>
        <to uri="log:info"/>
    </route>
</routes>
```

You can run it by executing:

```none
kamel run example.xml
```
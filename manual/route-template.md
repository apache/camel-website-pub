# Route Template

A Route template is as its name implies a template for a route, which is used to create routes from a set of input parameters. In other words, route templates are parameterized routes.

_Route template_ + _input parameters_ ⇒ _route_

From a route template, you can create one or more routes.

## Defining route templates in the DSL

Route templates are to be defined in the DSL (just like routes) as shown in the following:

-   Java
    
-   XML
    
-   YAML
    

```java
public class MyRouteTemplates extends RouteBuilder {

    @Override
    public void configure() throws Exception {
        // create a route template with the given name
        routeTemplate("myTemplate")
            // here we define the required input parameters (can have default values)
            .templateParameter("name")
            .templateParameter("greeting")
            .templateParameter("myPeriod", "3s")
            // here comes the route in the template
            // notice how we use {{name}} to refer to the template parameters
            // we can also use {{propertyName}} to refer to property placeholders
            .from("timer:{{name}}?period={{myPeriod}}")
                .setBody(simple("{{greeting}} ${body}"))
                .log("${body}");
    }
}
```

```xml
  <routeTemplate id="myTemplate">
    <templateParameter name="name"/>
    <templateParameter name="greeting"/>
    <templateParameter name="myPeriod" defaultValue="3s"/>
    <route>
      <from uri="timer:{{name}}?period={{myPeriod}}"/>
      <setBody><simple>{{greeting}} ${body}</simple></setBody>
      <log message="${body}"/>
    </route>
  </routeTemplate>
```

```yaml
- routeTemplate:
    id: "myTemplate"
    parameters:
      - name: "name"
      - name: "greeting"
      - name: "myPeriod"
        defaultValue: "3s"
    from:
      uri: "timer:{{name}}"
      parameters:
        period: "{{myPeriod}}"
      steps:
        - setBody:
            expression:
              simple:
                expression: "{{greeting}} ${body}"
        - log:
            message: "${body}"
```

In the examples above, there was one route template, but you can define as many as you want. Each template must have a unique id.

### Template parameters

The template parameters are used for defining the parameters the template accepts. In the example, there are three parameters: `_name_`, `_greeting_`, and `_myPeriod_`. The first two parameters are mandatory, whereas `_myPeriod_` is optional as it has a default value of 3s.

The template parameters are then used in the route as regular property placeholders with the `{{ }}` syntax. Notice how we use `{{name}}` and `{{greeting}}` in the timer endpoint and the simple language.

The route can use regular property placeholders from a properties file as well:

Application Properties

```properties
greeting = Davs
```

Then Camel would normally have used this value `Davs` when creating the route. However, as the route template has defined a template parameter with the same name `greeting` then a value must be provided when creating routes from the template.

Template parameters take precedence over regular property placeholders.

### Special Property Placeholders

Template property placeholders are placed between two curly braces:

```text
{{myProperty}}
```

To indicate that a template parameter is optional, and can have a `null` value, a question mark (`?`) must be used, as shown:

```text
{{?myProperty}}
```

For example in the following route the `replyTo` queue for the JMS endpoint is optional. So if the value is `null` then Camel will not assign `null` as `replyTo` in the JMS endpoint, and instead leave it as if was never configured; for example this allows the option to use its default setting.

-   Java
    
-   XML
    
-   YAML
    

Notice how we use `?` in the replyTo option below:

```java
from("timer:{{name}}?period={{myPeriod}}")
    .setBody(simple("{{greeting}} ${body}"))
    .to("jms:myqueue?replyTo={{?replyToQueue}}");
```

Notice how we use `?` in the replyTo option below:

```xml
<route>
    <from uri="timer:{{name}}?period={{myPeriod}}"/>
    <setBody>
        <simple>{{greeting}} ${body}</simple>
    </setBody>
    <to uri="jms:myqueue?replyTo={{?replyToQueue}}"/>
</route>
```

Notice how we use `?` in the replyTo option below:

```yaml
- route:
    from:
      uri: "timer:{{name}}"
      parameters:
        period: "{{myPeriod}}"
      steps:
        - setBody:
            expression:
              simple:
                expression: "{{greeting}} ${body}"
        - to:
            uri: "jms:myqueue"
            parameters:
              replyTo: "{{?replyToQueue}}"
```

> **Important**
> In case no replyToQueue property is provided when creating the template the option replyTo is just ignored.

#### Optional endpoint URIs

The `{{?}}` syntax can also be used for the entire endpoint URI. When the template parameter is not provided, the step is silently skipped (removed from the route).

-   Java
    
-   XML
    
-   YAML
    

```java
routeTemplate("myTemplate")
    .templateParameter("name")
    .templateOptionalParameter("optionalUri")
    .from("direct:{{name}}")
    .to("{{?optionalUri}}")
    .to("mock:end");
```

```xml
<routeTemplate id="myTemplate">
    <templateParameter name="name"/>
    <templateParameter name="optionalUri" required="false"/>
    <route>
        <from uri="direct:{{name}}"/>
        <to uri="{{?optionalUri}}"/>
        <to uri="mock:end"/>
    </route>
</routeTemplate>
```

```yaml
- routeTemplate:
    id: "myTemplate"
    parameters:
      - name: "name"
      - name: "optionalUri"
        required: false
    from:
      uri: "direct:{{name}}"
      steps:
        - to:
            uri: "{{?optionalUri}}"
        - to:
            uri: "mock:end"
```

When creating a route from this template without providing the `optionalUri` parameter, the `to("{\{?optionalUri}}")` step is omitted and messages flow directly to `mock:end`. When the parameter is provided, the step is included as usual.

This works with `to`, `toD`, `wireTap`, `enrich`, `pollEnrich`, and `poll` EIPs.

A property can also have a logical negation using the exclamation mark (`!`):

```text
{{!myProperty}}
```

In the following example we have the parameter named `disableTest` which we then need to negate when configuring this on the JMS endpoint for its `testConnectionOnStartup` option. This means that `disableTest=true` resolves as `testConnectionOnStartup=false`, and visa-versa. To support this then we must use the negation using the `!` mark:

-   Java
    
-   XML
    
-   YAML
    

```java
from("timer:{{name}}?period={{myPeriod}}")
    .setBody(simple("{{greeting}} ${body}"))
    .to("jms:myqueue?replyTo={{?replyToQueue}}&testConnectionOnStartup={{!disableTest}}");
```

```xml
<route>
    <from uri="timer:{{name}}?period={{myPeriod}}"/>
    <setBody>
        <simple>{{greeting}} ${body}</simple>
    </setBody>
    <to uri="jms:myqueue?replyTo={{?replyToQueue}}&amp;testConnectionOnStartup={{!disableTest}}"/>
</route>
```

```yaml
- route:
    from:
      uri: timer
      parameters:
        timerName: "{{name}}"
        period: "{{myPeriod}}"
      steps:
        - setBody:
            expression:
              simple:
                expression: "{{greeting}} ${body}"
        - to:
            uri: jms
            parameters:
              destinationName: myqueue
              replyTo: "{{?replyToQueue}}"
              testConnectionOnStartup: "{{!disableTest}}"
```

## Creating a route from a route template

To create routes from route templates, then this is possible from standard Java code, and all the Camel DSLs.

In the following code snippet, we create 2 routes from the same template, but with different parameters.

-   Java
    
-   Java DSL
    
-   XML
    
-   YAML
    

Here we create routes from standard Java using the Camel Java API using `org.apache.camel.builder.TemplatedRouteBuilder` that uses a fluent builder style.

```java
// create two routes from the template
TemplatedRouteBuilder.builder(context, "myTemplate")
    .parameter("name", "one")
    .parameter("greeting", "Hello")
    .add(); // adds a new route from the given input parameters

TemplatedRouteBuilder.builder(context, "myTemplate")
    .parameter("name", "two")
    .parameter("greeting", "Bonjour")
    .parameter("myPeriod", "5s")
    .add(); // adds a new route from the given input parameters
```

Here we create routes from inside a regular `RouteBuilder` using Java DSL where each `templatedRoute` will create and add a new route from the given input parameters.

```java
templatedRoute("myTemplate")
        .parameter("name", "one")
        .parameter("greeting", "Hello");

templatedRoute("myTemplate")
        .parameter("name", "two")
        .parameter("greeting", "Bonjour")
        .parameter("myPeriod", "5s");
```

```xml
  <templatedRoute routeTemplateRef="myTemplate">
    <parameter name="name" value="one"/>
    <parameter name="greeting" value="Hello"/>
  </templatedRoute>

  <templatedRoute routeTemplateRef="myTemplate">
    <parameter name="name" value="two"/>
    <parameter name="greeting" value="Bonjour"/>
    <parameter name="myPeriod" value="5s"/>
  </templatedRoute>
```

```yaml
- templatedRoute:
    routeTemplateRef: "myTemplate"
    parameters:
      - name: "name"
        value: "one"
      - name: "greeting"
        value: "Hello"

- templatedRoute:
    routeTemplateRef: "myTemplate"
    parameters:
      - name: "name"
        value: "two"
      - name: "greeting"
        value: "Bonjour"
      - name: "myPeriod"
        value: "5s"
```

> **Tip**
> In Java code then the returned value from `add` method is the route id of the new route that was added. However `null` is returned if the route is not yet created and added, which can happen if `CamelContext` is not started yet.

If no route id is provided, then Camel will auto assign a route id. In the example above then Camel would assign route ids such as `route1`, `route2` to these routes.

If you want to specify a route id, then use `routeId` as follows, where the id is set to `myCoolRoute`:

-   Java
    
-   Java DSL
    
-   XML
    
-   YAML
    

```java
TemplatedRouteBuilder.builder(context, "myTemplate")
    .routeId("myCoolRoute")
    .parameter("name", "one")
    .parameter("greeting", "hello")
    .parameter("myPeriod", "5s")
    .add();
```

```java
templatedRoute("myTemplate")
        .routeId("myCoolRoute")
        .parameter("name", "one")
        .parameter("greeting", "hello")
        .parameter("myPeriod", "5s");
```

```xml
  <templatedRoute routeTemplateRef="myTemplate" routeId="myCoolRoute">
    <parameter name="name" value="one"/>
    <parameter name="greeting" value="hello"/>
    <parameter name="myPeriod" value="5s"/>
  </templatedRoute>
```

```yaml
- templatedRoute:
    routeTemplateRef: "myTemplate"
    routeId: "myCoolRoute"
    parameters:
      - name: "name"
        value: "one"
      - name: "greeting"
        value: "hello"
      - name: "myPeriod"
        value: "5s"
```

### Using template parameters with Java DSL Simple builder

When using Java DSL and [Simple](../components/4.22.x/languages/simple-language.md) language, then beware that you should not use the _simple fluent builder_ when defining the simple expressions/predicates.

For example, given the following route template in Java DSL:

_Java-only: route template with Simple fluent builder (unsupported usage)_

```java
public class MyRouteTemplates extends RouteBuilder {

    @Override
    public void configure() throws Exception {
        routeTemplate("myTemplate")
            .templateParameter("name")
            .templateParameter("color")
            .from("direct:{{name}}")
                .choice()
                    .when(simple("{{color}}").isEqualTo("red")) (1)
                        .to("direct:red")
                    .otherwise()
                        .to("color:other")
                .end();
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>This is not supported (see explanation below)</td></tr></tbody></table>

> **Important**
> Then notice how the simple predicate is using _simple fluent builder_ `simple("{{color}}").isEqualTo("red")`. This is **not supported** with route templates and would not work when creating multiple routes from the template.

Instead, the simple expression should be a literal String value _only_ as follows:

_Java-only: correct Simple expression syntax for route templates_

```java
.when(simple("'{{color}}' == 'red'")
```

So the correct solution would be as follows:

_Java-only: correct route template with Simple String literal_

```java
public class MyRouteTemplates extends RouteBuilder {

    @Override
    public void configure() throws Exception {
        routeTemplate("myTemplate")
            .templateParameter("name")
            .templateParameter("color")
            .from("direct:{{name}}")
                .choice()
                    .when(simple("'{{color}}' == 'red'") (1)
                        .to("direct:red")
                    .otherwise()
                        .to("color:other")
                .end();
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>This is supported and the simple expression as a String literal can be used as-is in all the Camel DSL.</td></tr></tbody></table>

### Using hardcoded node IDs in route templates

If route templates contain hardcoded node IDs, then routes created from templates will use the same IDs. Therefore, if two or more routes are created from the same template, you will have _duplicate id detected_ error.

Given the route template below, then it has hardcoded ID (`_new-order_`) in node calling the http services.

-   Java
    
-   XML
    
-   YAML
    

```java
routeTemplate("orderTemplate")
    .templateParameter("queue")
    .from("jms:{{queue}}")
        .to("http:orderserver.acme.com/neworder").id("new-order") (1)
        .log("Processing order");
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Hardcoded ID on the To EIP</td></tr></tbody></table>

```xml
<routeTemplate id="orderTemplate">
    <templateParameter name="queue"/>
    <route>
        <from uri="jms:{{queue}}"/>
        <to id="new-order" uri="http:orderserver.acme.com/neworder"/> (1)
        <log message="Processing order"/>
    </route>
</routeTemplate>
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Hardcoded ID on the To EIP</td></tr></tbody></table>

```yaml
- routeTemplate:
    id: "myTemplate"
    parameters:
      - name: "queue"
    from:
      uri: "jms:{{queue}}"
      steps:
        - to:
            id: new-order (1)
            uri: http:orderserver.acme.com/neworder
        - log:
            message: Processing order
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Hardcoded ID on the To EIP</td></tr></tbody></table>

When creating routes from templates, you can then provide a _prefix_ which is used for all node IDs. This allows to create 2 or more routes without _duplicate id_ errors.

For example in the following, we create a new route `_myCoolRoute_` from the `_myTemplate_` template, and use a prefix of `_web_`.

-   Java
    
-   XML
    
-   YAML
    

```java
templatedRoute("orderTemplate")
        .routeId("webOrder")
        .prefixId("web")
        .parameter("queue", "order.web");
```

Then we can create a 2nd route with a different \_prefixId\`:

```java
templatedRoute("orderTemplate")
        .routeId("ftpOrder")
        .prefixId("ftp")
        .parameter("queue", "order.ftp");
```

```xml
  <templatedRoute routeTemplateRef="orderTemplate" routeId="webOrder" prefixId="web">
    <parameter name="queue" value="web"/>
  </templatedRoute>
```

Then we can create a 2nd route with a different \_prefixId\`:

```xml
  <templatedRoute routeTemplateRef="orderTemplate" routeId="ftpOrder" prefixId="ftp">
    <parameter name="queue" value="order.ftp"/>
  </templatedRoute>
```

```yaml
- templatedRoute:
    routeTemplateRef: "orderTemplate"
    routeId: "webOrder"
    prefixId: "web"
    parameters:
      - name: "queue"
        value: "web"
```

Then we can create a 2nd route with a different \_prefixId\`:

```yaml
- templatedRoute:
    routeTemplateRef: "orderTemplate"
    routeId: "ftpOrder"
    prefixId: "ftp"
    parameters:
      - name: "queue"
        value: "order.ftp"
```

## Binding Beans to Route Templates

Route templates support binding locally-scoped beans that are private to each route created from the template. This is an advanced feature.

See [Route Template Bean Binding](route-template-bean-binding.md) for details.

## Configuring route templates when creating route (advanced)

There may be some special situations where you want to be able to do some custom configuration/code when a route is about to be created from a route template.

> **Note**
> This is only available in Java DSL

To support this you can use the `configure` in the route template DSL where you can specify the code to execute as show:

_Java-only: custom configuration callback when creating route from template_

```java
routeTemplate("myTemplate")
    .templateParameter("myTopic")
    .configure((RouteTemplateContext rtc) ->
        // do some custom code here
    )
    .from("direct:to-topic")
    .to("kafka:{{myTopic}}");
```

## JMX management

The route templates can be dumped as XML from the `ManagedCamelContextMBean` MBean via the `dumpRouteTemplatesAsXml` operation.

## Creating routes from a properties file

When using `camel-main` you can specify the parameters for route templates in `application.properties` file.

For example, given the route template below:

-   Java
    
-   XML
    
-   YAML
    

```java
routeTemplate("mytemplate")
    .templateParameter("input")
    .templateParameter("result")
    .from("direct:{{input}}")
        .to("mock:{{result}}");
```

```xml
<routeTemplate id="mytemplate">
    <templateParameter name="input"/>
    <templateParameter name="result"/>
    <route>
        <from uri="direct:{{input}}"/>
        <to uri="mock:{{result}}"/>
    </route>
</routeTemplate>
```

```yaml
- routeTemplate:
    id: mytemplate
    parameters:
      - name: input
      - name: result
    from:
      uri: "direct:{{input}}"
      steps:
        - to:
            uri: "mock:{{result}}"
```

Then we can create two routes from this template by configuring the values in the `application.properties` file:

```properties
camel.route-template[0].template-id=mytemplate
camel.route-template[0].input=foo
camel.route-template[0].result=cheese

camel.route-template[1].template-id=mytemplate
camel.route-template[1].input=bar
camel.route-template[1].result=cheese
```

## Creating routes from custom sources of template parameters

The SPI interface `org.apache.camel.spi.RouteTemplateParameterSource` can be used to implement custom sources that are used during startup of Camel to create routes via the templates with parameters from the custom source(s).

For example, a custom source can be implemented to read parameters from a shared database that Camel uses during startup to create routes. This allows externalizing these parameters and as well to easily add more routes with varying parameters.

To let Camel discover custom sources, then register the source into the Camel registry.

## See Also

See these examples:

-   [Standalone Route Template](https://github.com/apache/camel-examples/tree/main/routetemplate)
    
-   [Spring Boot Route Template](https://github.com/apache/camel-spring-boot-examples/tree/main/routetemplate)
    
-   [Spring Boot Route Template XML DSL](https://github.com/apache/camel-spring-boot-examples/tree/main/routetemplate-xml)
# `CamelTestSupport` style of testing

If you used Camel standalone or on other runtimes before, you may know `CamelTestSupport` already. The original `CamelTestSupport` class is not well suited to Quarkus, so there’s an extended Quarkus friendly version called `CamelQuarkusTestSupport`.

> > **Important**
> > `CamelQuarkusTestSupport` only works in JVM mode. If you need to test in native mode, then use one of the alternate test strategies described in the [Testing](../testing.md) guide.

To use `CamelQuarkusTestSupport`, you must add `camel-quarkus-junit` as a test scoped dependency to your application.

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-junit</artifactId>
    <scope>test</scope>
</dependency>
```

## Customizing the `CamelContext` for testing

You can customize the `CamelContext` for testing with [configuration profiles](https://quarkus.io/guides/config-reference#profiles), CDI beans, observers, [mocks](https://quarkus.io/guides/getting-started-testing#mock-support) etc. You can also override the `createCamelContext` method and interact directly with the `CamelContext`.

> **Important**
> When using `createCamelContext` you **MUST NOT** instantiate and return a new `CamelContext`. Instead, invoke `super.createCamelContext()` and modify the returned `CamelContext` as needed. Failing to follow this rule will result in an exception being thrown.

```java
@QuarkusTest
class SimpleTest extends CamelQuarkusTestSupport {

    @Override
    protected CamelContext createCamelContext() throws Exception {
        // Must call super to get a handle on the application scoped CamelContext
        CamelContext context = super.createCamelContext();
        // Apply customizations
        context.setTracing(true);
        // Return the modified CamelContext
        return context;
    }
}
```

## Configuring routes for testing

Any classes that extend `RouteBuilder` in your application will have their routes automatically added to the `CamelContext`. Similarly, any XML or YAML routes configured from `camel.main.routes-include-pattern` will also be loaded.

This may not always be desirable for your tests. You control which routes get loaded at test time with configuration properties:

-   `quarkus.camel.routes-discovery.include-patterns`
    
-   `quarkus.camel.routes-discovery.exclude-patterns`,
    
-   `camel.main.routes-include-pattern`
    
-   `camel.main.routes-exclude-pattern`.
    

You can also define test specific routes per test class by overriding `createRouteBuilder`:

```java
@QuarkusTest
class SimpleTest extends CamelQuarkusTestSupport {
    @Test
    void testGreeting() {
        MockEndpoint mockEndpoint = getMockEndpoint("mock:result");
        mockEndpoint.expectedBodiesReceived("Hello World");

        template.sendBody("direct:start", "World");

        mockEndpoint.assertIsSatisfied();
    }

    @Override
    protected RoutesBuilder createRouteBuilder() throws Exception {
        return new RouteBuilder() {
            @Override
            public void configure() throws Exception {
                from("direct:start")
                    .transform().simple("Hello ${body}")
                    .to("mock:result");
            }
        };
    }
}
```

## CamelContext test lifecycle

One of the main differences in `CamelQuarkusTestSupport` compared to `CamelTestSupport` is how the `CamelContext` lifecycle is managed.

On Camel Quarkus, a single `CamelContext` is created for you automatically by the runtime. By default, this `CamelContext` is shared among all tests and remains started for the duration of the entire test suite execution.

This can potentially have some unintended side effects for your tests. If you need to have the `CamelContext` restarted between tests, then you can create a custom [test profile](https://quarkus.io/guides/getting-started-testing#testing_different_profiles), which will force the application under test to be restarted.

For example, to define a test profile:

```java
@QuarkusTest
class MyTestProfile implements QuarkusTestProfile {
    ...
}
```

Then reference it on the test class with `@TestProfile`:

```java
// @TestProfile will trigger the application to be restarted
@TestProfile(MyTestProfile.class)
@QuarkusTest
class SimpleTest extends CamelQuarkusTestSupport {
    ...
}
```

> **Note**
> You cannot manually restart the `CamelContext` by invoking its `stop()` and `start()` methods. This will result in an exception.

## Examples

### Simple `RouteBuilder` and test class

Simple `RouteBuilder`:

```java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:start")
            .transform().simple("Hello ${body}")
            .to("mock:result");
    }
}
```

Test sending a message payload to the `direct:start` endpoint:

```java
@QuarkusTest
class SimpleTest extends CamelQuarkusTestSupport {
    @Test
    void testGreeting() {
        MockEndpoint mockEndpoint = getMockEndpoint("mock:result");
        mockEndpoint.expectedBodiesReceived("Hello World");

        template.sendBody("direct:start", "World");

        mockEndpoint.assertIsSatisfied();
    }
}
```

### Using `AdviceWith`

[AdviceWith](../../../../manual/advice-with.md) allows you to modify routes at runtime for testing purposes - replacing endpoints, adding interceptors, or changing route behavior without modifying production code.

#### Advising existing application routes

The recommended pattern is:

1.  Define routes in your **application code** (src/main/java)
    
2.  Use `AdviceWith` to modify these **existing** routes in your tests
    

```java
// Application code: src/main/java/com/example/MyRoutes.java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() {
        from("kafka:input-topic").routeId("my-kafka-route")
            .to("kafka:output-topic")
            .to("mock:result");
    }
}

// Test code: src/test/java/com/example/MyRoutesTest.java
@QuarkusTest
class MyRoutesTest extends CamelQuarkusTestSupport {
    @BeforeEach
    public void beforeEach() throws Exception {
        // Advise the application route
        AdviceWith.adviceWith(this.context, "my-kafka-route", route -> {
            route.weaveByToUri("kafka:output-topic*").replace().to("mock:kafka-stub");
        });
    }

    @Test
    void testRoute() throws Exception {
        MockEndpoint stub = getMockEndpoint("mock:kafka-stub");
        stub.expectedMessageCount(1);

        template.sendBody("kafka:input-topic", "test");

        stub.assertIsSatisfied();
    }
}
```

> **Warning**
> Advising routes created via `createRouteBuilder()` in tests can lead to unpredictable behavior.

#### Apply advice in `@BeforeEach` or `doBeforeEach`

When all tests in a class need the same advice, apply it in `@BeforeEach` or override `doBeforeEach`:

```java
@QuarkusTest
class SimpleTest extends CamelQuarkusTestSupport {
    @BeforeEach
    public void beforeEach() throws Exception {
        // Apply advice to EXISTING application route
        AdviceWith.adviceWith(this.context, "advisedRoute", route -> {
            route.replaceFromWith("direct:replaced");
        });
        // Routes that aren't advised are automatically started after this method completes
    }

    @Test
    void testAdvisedRoute() throws Exception {
        MockEndpoint mockEndpoint = getMockEndpoint("mock:result");
        mockEndpoint.expectedBodiesReceived("Hello World");

        template.sendBody("direct:replaced", "World");

        mockEndpoint.assertIsSatisfied();
    }
}
```

Routes that aren’t advised are automatically started after `@BeforeEach` or `doBeforeEach` completes. Advice modifications are automatically cleaned up between test methods

#### Per-test-method advice using `adviceRoute()`

When you need **different** advice in each test method, use the `adviceRoute()` helper method which handles route lifecycle (stop, advice, start) automatically:

```java
@QuarkusTest
class PerMethodAdviceTest extends CamelQuarkusTestSupport {
    @Test
    void testWithMockOutput() throws Exception {
        // Apply advice specific to this test on EXISTING application route
        adviceRoute("my-route", route -> {
            route.weaveByToUri("kafka:output*").replace().to("mock:kafka-stub");
        });

        MockEndpoint stub = getMockEndpoint("mock:kafka-stub");
        stub.expectedMessageCount(1);

        template.sendBody("kafka:input", "test message");

        stub.assertIsSatisfied();
    }

    @Test
    void testWithDifferentAdvice() throws Exception {
        // Different advice for this test on the same EXISTING route
        adviceRoute("my-route", route -> {
            route.weaveByToUri("kafka:output*").replace()
                .transform(simple("MODIFIED: ${body}"))
                .to("mock:result");
        });

        // ... different test assertions
    }
}
```

#### Advice patterns

> **Important**
> When using `weaveByToUri()`, `weaveByType()`, or similar methods, use specific patterns rather than wildcards to avoid unintentionally matching endpoints from the main application or other routes.

For example, instead of:

```java
// Matches ALL Kafka endpoints in the context
route.weaveByToUri("kafka:*").replace().to("mock:result");
```

Use specific endpoint URIs:

```java
// Only matches the specific endpoint you intend to advise
route.weaveByToUri("kafka:my-output-topic*").replace().to("mock:result");
```

Or use IDs for even more precision:

```java
// Uses ID for exact matching
route.weaveById("kafkaProducer").replace().to("mock:result");
```

Wildcard patterns like `kafka:*`, `http:*`, or `direct:*` will match **all** endpoints of that type throughout the entire `CamelContext`, including routes from your main application that the test may not need to modify. This can cause unexpected test failures and interference between tests.

#### Advice cleanup between tests

Advice modifications are automatically cleaned up between test methods to prevent interference. This ensures that:

-   Each test starts with a clean route state
    
-   Advice from one test doesn’t affect subsequent tests
    
-   Tests remain independent and can run in any order
    

## Limitations

### Test lifecycle methods inherited from `CamelTestSupport`

`CamelQuarkusTestSupport` inherits some test lifecycle methods from `CamelTestSupport`. However, they should not be used and instead are replaced with equivalent methods in `CamelQuarkusTestSupport`.

 
| CamelTestSupport lifecycle methods | CamelQuarkusTestSupport equivalent |
| --- | --- |
| `afterAll` | `doAfterAll` |
| `afterEach`, `afterTestExecution` | `doAfterEach` |
| `beforeAll` | `doAfterConstruct` |
| `beforeEach` | `doBeforeEach` |

### Creating a custom Camel registry is not supported

The `CamelQuarkusTestSupport` implementation of `createCamelRegistry` will throw `UnsupportedOperationException`.

If you need to bind or unbind objects to the Camel registry, then you can do it by one of the following methods.

-   Produce named CDI beans
    
    ```java
    public class MyBeanProducers {
        @Produces
        @Named("myBean")
        public MyBean createMyBean() {
            return new MyBean();
        }
    }
    ```
    
-   Override `createCamelContext` (see example above) and invoke `camelContext.getRegistry().bind("foo", fooBean)`
    
-   Use the `@BindToRegistry` annotation
    
    ```java
    @QuarkusTest
    class SimpleTest extends CamelQuarkusTestSupport {
        @BindToRegistry("myBean")
        MyBean myBean = new MyBean();
    }
    ```
    

> **Note**
> Beans bound to the Camel registry from individual test classes, will persist for the duration of the test suite execution. This could have unintended consequences, depending on your test expectations. You can use test profiles to restart the `CamelContext` to avoid this.
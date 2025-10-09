# Test

> **Warning**
> **Deprecated:** This test is deprecated and may be removed in a future release.

**Since Camel 2.9**

The `camel-test` module is used for unit testing Camel.

> **Warning**
> This module is deprecated. Use [camel-test-junit5](../../4.18.x/others/test-junit5.md) instead.

The class `org.apache.camel.test.junit4.CamelTestSupport` provides a base JUnit class which you would extend and implement your Camel unit test.

## Simple unit test example

As shown below is a basic junit test which uses `camel-test`. The `createRouteBuilder` method is used for build the routes to be tested. Then the methods with `@Test` annotations are JUnit test methods which will be executed. The base class `CamelTestSupport` has a number of helper methods to configure testing, see more at the javadoc of this class.

```java
import org.apache.camel.RoutesBuilder;
import org.apache.camel.builder.RouteBuilder;
import org.apache.camel.test.junit4.CamelTestSupport;
import org.junit.Test;

public class SimpleMockTest extends CamelTestSupport {

    @Test
    public void testMock() throws Exception {
        getMockEndpoint("mock:result").expectedBodiesReceived("Hello World");

        template.sendBody("direct:start", "Hello World");

        assertMockEndpointsSatisfied();
    }

    @Override
    protected RoutesBuilder createRouteBuilder() throws Exception {
        return new RouteBuilder() {
            @Override
            public void configure() throws Exception {
                from("direct:start")
                        .to("mock:result");
            }
        };
    }

}
```
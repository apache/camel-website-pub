# Testing

Testing offers a good way to ensure camel routes behave as expected over time. Before going deeper into the subject, it is strongly advised to read [First Steps](first-steps.md) and [Quarkus testing](https://quarkus.io/guides/getting-started-testing).

When it comes to testing a route in the context of Quarkus, the recommended approach is to write local integration tests. This has the advantage of covering both JVM and native mode.

The following pages cover further testing topics:

-   [Testing with external services](testing/external-services.md)
    
-   [Annotation based testing with `@CamelQuarkusTest`](testing/camel-quarkus-test.md) (JVM mode only)
    
-   [`CamelTestSupport` style of testing](testing/camel-quarkus-test-support.md) (JVM mode only)
    

## A test running in JVM mode

All tests should be annotated with `@QuarkusTest`. This will bootstrap Quarkus and start Camel routes before the `@Test` logic is executed, like in the example below:

```java
import io.quarkus.test.junit.QuarkusTest;
import org.junit.jupiter.api.Test;

@QuarkusTest
class MyTest {
    @Test
    void test() {
        // Use any suitable code that send test data to the route and then assert outcomes
    }
}
```

An example implementation can be found [here](https://github.com/apache/camel-quarkus/blob/main/integration-tests/bindy/src/test/java/org/apache/camel/quarkus/component/bindy/it/MessageTest.java).

## A test running in native mode

Providing all extensions your application depends on are supported in native mode, you should test that your application works correctly native mode. The test logic defined in JVM mode can be reused in native mode, by inheriting from the respective JVM mode class. The `@QuarkusIntegrationTest` annotation instructs the Quarkus JUnit extension to compile the application under test to a native image and will start it before running the tests.

```java
import io.quarkus.test.junit.QuarkusIntegrationTest;

@QuarkusIntegrationTest
class MyIT extends MyTest {
}
```

An example implementation of a native can be found [here](https://github.com/apache/camel-quarkus/blob/main/integration-tests/bindy/src/test/java/org/apache/camel/quarkus/component/bindy/it/MessageRecordIT.java).

## `@QuarkusTest` Vs `@QuarkusIntegrationTest`

JVM mode tests annotated with `@QuarkusTest` are executed in the same JVM as the application under test. This makes it possible to [`@Inject`](https://quarkus.io/guides/getting-started-testing#injection-into-tests) CDI beans from the application into the test code. You can also define new beans or even override beans from the application using [`@jakarta.enterprise.inject.Alternative`](https://quarkus.io/guides/getting-started-testing#cdi-alternative-mechanism) and [`@jakarta.annotation.Priority`](https://quarkus.io/guides/getting-started-testing#cdi-alternative-mechanism).

These options do not work in native mode for tests annotated with `@QuarkusIntegrationTest`, as they are executed in a JVM hosted in a process separate from the running native application.

An important consequence of this, is that all communication between the tests and the native application, must take one or more of the following forms:

-   Network calls. Typically, HTTP or any other network protocol your application supports.
    
-   Watching the filesystem for changes (E.g. via Camel `file` endpoints).
    
-   Any other kind of interprocess communication.
    

`QuarkusIntegrationTest` also provides some additional features that are not available through `@QuarkusTest`.

-   In JVM mode it can launch and test the runnable application JAR produced by the Quarkus build.
    
-   In native mode it can launch and test the native application produced by the Quarkus build.
    
-   If a container image was created during the build, then a container is started so that tests can be executed against it.
    

For more information about `QuarkusIntegrationTest` see the [Quarkus testing guide](https://quarkus.io/guides/getting-started-testing#quarkus-integration-test).
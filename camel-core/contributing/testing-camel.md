# Testing Camel

## Basic testing

After you have [Build](building.md) the code, you should test your changes. Our project follows [Apache Maven](http://maven.apache.org) conventions for building and testing the code.

The code base relies on the [Maven Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/) for running the unit tests and the [Maven Failsafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/) for running the integration tests.

To run the unit tests, use the following command:

```bash
mvn test
```

To run the integration tests, use the following command:

```bash
mvn verify
```

> **Note**
> The command `mvn verify` will also run the unit tests.

The set of tests executed may differ according to the platform, operating system and Java version used.

> **Note**
> Our project has automation that will automatically test contributions made via pull-requests. Nonetheless, it’s always better to ensure your contribution works before sending it.

### Unit Tests versus Integration Tests

Since Camel is an integration framework, which by definition depends on external systems, tools and platforms to produce or consume data, the distinction of unit/integration tests may not be so clear.

Tests must follow the following naming convention:

-   `*Test.java` (i.e.: MyComponentTest.java) for unit tests.
    
-   `*IT.java` (i.e.: MyComponentIT.java) for integration tests.
    
-   `*ManualTest.java` (i.e.: MyComponentManualTest.java) for manual tests.
    

## Implementing new tests

If you need to implement tests for your changes, which is highly recommended, you will probably need to handle three separate things:

1.  writing testable code
    
2.  writing Apache Camel tests
    
3.  simulating the infrastructure
    

### Writing testable code

Camel has multiple features to simplify testing. You can use those features to maximize your ability to test your code contribution. The [Testing](../../manual/testing.md) page in the User Manual provides detailed information and examples for writing Camel tests.

> **Note**
> Although the testing information on the User Manual is aimed at Camel users, the same features are also used to test Camel itself.

### Writing Apache Camel tests

Naturally, there is no rule of thumb for how the code changes, and test logic should be written. There are, however, a few things to avoid and good practices to follow when writing tests for Apache Camel.

**Things to avoid**:

-   Calling `Thread.sleep` in tests
    
-   Disabling tests without providing a reason (when needed, create a Jira ticket and use that as part of the reason string)
    
-   Writing large tests
    
-   Writing assertions without a fail message
    
-   Writing custom profiles for enabling/disabling tests
    

**Good things to do**:

-   Use the [Awaitility](http://www.awaitility.org/) library
    
-   Writing small tests
    
-   Coordinating test execution using [JUnit’s @Order annotation](https://junit.org/junit5/docs/current/user-guide/#writing-tests-test-execution-order)
    
-   Providing fail messages for assertions
    

### Simulating the test infrastructure

In many cases, it may be necessary to access or simulate access to a certain infrastructure to execute the tests.

As an integration framework, by nature, Camel needs to interact with other systems to execute its tests.

> **Note**
> Typical assumptions made when writing tests for user-level applications, don’t necessarily translate well to Camel. In many cases, it is necessary to evaluate the specific needs and requirements of each component. For instance, assumptions about whether it’s OK or not to reuse resources, whether data ordering matters, and a lot more have to be evaluated per-component.

Camel has a growing library of reusable components to help providing the [test infra structure](../../manual/test-infra.md).

These components are located in the test-infra module and provide support for simulating message brokers, cloud environments, databases, and much more.

Using these components is usually as simple as registering them as JUnit 5 extensions:

```java
@RegisterExtension
static NatsService service = NatsServiceFactory.createService();
```

Then you can access the service by using the methods and properties provided by the services. This varies according to each service.

If you need to implement a new test-infra service, check the [test infra structure](../../manual/test-infra.md) documentation for additional details.
# Testing extensions

Testing Camel Quarkus extensions is very similar to [testing Camel Quarkus applications](../user-guide/testing.md). In both cases, the tests interact with a Camel Quarkus application. The main difference is in the purpose of the tested application: when testing extensions, it is there just for the sake of testing. We use it as a means to indirectly verify the functionality of the underlying extension(s).

## Where are the integration tests?

Here are the directories containing integration tests:

-   `[integration-tests](https://github.com/apache/camel-quarkus/tree/main/integration-tests)`
    
-   `[integration-test-groups/*](https://github.com/apache/camel-quarkus/tree/main/integration-test-groups)`
    
-   `[extensions-jvm/*/integration-test](https://github.com/apache/camel-quarkus/tree/main/extensions-jvm)`
    

## Anatomy of an extension integration test

### The application

The application under test lives under `src/main` directory of the test module. It should typically contain one or more Camel routes that utilize the Camel component brought by the extension under test.

`ProducerTemplate` may be favorable over having a full-fledged route, e.g. when it helps to avoid additional dependencies or where it helps to keep the test application simple.

On the other hand, the use of `ConsumerTemplate` should be assessed carefully. In some cases, it may use a different `Consumer` implementation (polling vs. non-polling) than what would be used by the given component in a route. Thus, a test application with `ConsumerTemplate` may miss covering important execution paths. The rule of thumb is to use `ConsumerTemplate` only for components whose default consumer implements `PollingConsumer`.

### Tests

Because [native tests run in a process separate](../user-guide/testing.html#jvm-vs-native-tests) from the JVM running the tests, all communication between the tests and the application under test must go over network or some other kind of interprocess communication. We typically use JAX-RS endpoints (on the application side) and [RestAssured](https://rest-assured.io/) (on the test side) for this purpose.

As suggested in the [Testing user guide](../user-guide/testing.html#native-tests), our native tests typically extend their JVM counterparts using the same test code for both JVM and native mode. For this reason we abstain from using CDI and direct call of application code in our tests.

Except for [RestAssured](https://rest-assured.io/), we also use [Awaitility](http://www.awaitility.org/) for awaiting some state and [AssertJ](https://assertj.github.io/doc/) for more advanced assertions.

> **Tip**
> As mentioned in [Create new extension](create-new-extension.md) section, `mvn cq:create -N -Dcq.artifactIdBase=my-component` generates some testing boilerplate for you. If you want to add just a new test module for an existing extension, `mvn cq:new-test -N -Dcq.artifactIdBase=my-component` is there for you.

## Minimal set of dependencies

Keeping the set of test module dependencies as small as possible has several advantages:

-   Less code is faster to compile to native image
    
-   Additional code may introduce some side effects, mainly in native compilation. For instance, an extension A may configure the native compiler in such a way that it causes also extension B to work properly in native mode. However, if B was tested in isolation, it would not work.
    
-   This rule also applies to `junit`, `testcontainers`, `rest-assured`, `assertj` and similar testing dependencies: Unless there is some really good reason to do the opposite, they should be kept in Maven `test` scope. Having them in the `compile` or `runtime` scope makes them analyzed and possibly compiled by GraalVM when the tests are run in native mode. On one hand, it makes the native compilation slower and on the other hand, those testing artifacts may cause native compilation issues.
    

## Grouping

Some of our test modules have very similar sets of dependencies. While it is important to test them in isolation, running each separately takes quite a lot of time, mainly due to native compilation. In such cases, it may make sense to create a "grouped" module that unifies (using some tooling) several isolated tests. The grouped module may then be preferred in a CI job that validates pull requests, while the isolated tests are run only once a day.

### How grouping works

-   The isolated test modules are located under `[integration-test-groups](https://github.com/apache/camel-quarkus/tree/main/integration-test-groups)` directory of the source tree.
    
-   For each subdirectory of `integration-test-groups` there is a grouped test module under `integration-tests`. E.g. for `[integration-test-groups/azure](https://github.com/apache/camel-quarkus/tree/main/integration-test-groups/azure)` there is `[integration-tests/azure-grouped](https://github.com/apache/camel-quarkus/tree/main/integration-tests/azure-grouped)`.
    
-   Grouped modules dynamically pull all sources from their associated isolated test modules to their `target/[test-]classes` directories respectively.
    
-   `application.properties` files and service descriptors are concatenated using a Groovy script.
    
-   The dependencies in the grouped `pom.xml` need to be updated manually via `mvn process-resources -Pformat -N` run from the root directory of the source tree.
    

## Coverage

When porting a Camel component to Quarkus, we generally do not want to duplicate all the fine grained tests that are often available in Camel already. Our main goal is to make sure that the main use cases work well in native mode. But how can you figure out which are those?

The use cases explained in the given components documentation usually give a good guidance. For example, when writing tests for the SQL extension, you would go to documentation page of the [SQL component](../../../components/4.14.x/sql-component.md) and try to cover the use cases mentioned there: [Treatment of the message body](../../../components/4.14.x/sql-component.html#_treatment_of_the_message_body) [Result of the query](../../../components/4.14.x/sql-component.html#_result_of_the_query), [Using StreamList](../../../components/4.14.x/sql-component.html#_using_streamlist), etc.

In any case, both consumer and producer of the component (if the component supports both) should be covered.

## Lightweight functional tests

Especially when testing various configuration setups, having a separate integration test module for each configuration set would be an overkill. `io.quarkus.test.QuarkusUnitTest` may suit well for such situations.

A big advantage of this kind of tests is that they are very lightweight and fast. But on the other hand, they are executed only in JVM mode.

Please refer to the [Servlet extension](https://github.com/apache/camel-quarkus/tree/main/extensions/servlet/deployment/src/test/java/org/apache/camel/quarkus/component/servlet/test) for an examples.
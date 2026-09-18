# Openapi Validator

**Since Camel 4.7**

Camel comes with a default client request/response validator for the Camel Rest DSL.

The `camel-openapi-validator` uses the third party [Atlassian Swagger Request Validator](https://bitbucket.org/atlassian/swagger-request-validator/src/master/) library instead for client request/response validator. This library is a more extensive validator than the default validator from `camel-core`.

## Auto-detection from classpath

To use this implementation all you need to do is to add the `camel-openapi-validator` dependency to the classpath.

### Configuring levels of errors

The Atlassian Swagger Request Validator supports configuring [fine-grained levels](https://bitbucket.org/atlassian/swagger-request-validator/src/c6200d0d849ae69be679f7fe01042cd9e84637c4/swagger-request-validator-core/README.md) for validating. This allows to turn on ignoring some specific errors.

For example, you can ignore query parameters

```properties
camel.rest.validation-levels[validation.schema.required] = INFO
camel.rest.validation-levels[validation.request.parameter.query.missing] = IGNORE
camel.rest.validation-levels[validation.response.body.missing] = WARN
```
# ![kafka batch manual commit action](_images/kamelets/kafka-batch-manual-commit-action.svg) Kafka Batch Manual Commit Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Manually commit Kafka Batch Offset.

## Configuration Options

The `kafka-batch-manual-commit-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `kafka-batch-manual-commit-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:kafka-batch-manual-commit-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-manual-commit-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-manual-commit-action.kamelet.yaml)
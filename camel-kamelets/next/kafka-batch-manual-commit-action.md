# ![kafka batch manual commit action](_images/kamelets/kafka-batch-manual-commit-action.svg) Kafka Batch Manual Commit Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Saves in Kafka the position (offset) reached by a batch of records from `kafka-batch-source`, so that the batch is not received again after a restart.

Use it to count the records of a batch as read only once the whole batch was handled, for example once it was written to a database: put it at the end of a flow that starts with `kafka-batch-source`. For single records from `kafka-source` use `kafka-manual-commit-action`.

Input: a batch from `kafka-batch-source`, or from one of the `kafka-batch-**-registry-**` sources, with `allowManualCommit` set to true and `autoCommitEnable` set to false. It uses the `CamelKafkaManualCommit` header of the message, or else that of the last entry of the list.

Output: the message is unchanged.

Good to know: without the `CamelKafkaManualCommit` header, for example when `allowManualCommit` is false, it does nothing and does not fail.

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
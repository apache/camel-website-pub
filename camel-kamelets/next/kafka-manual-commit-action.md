# ![kafka manual commit action](_images/kamelets/kafka-manual-commit-action.svg) Kafka Manual Commit Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Saves in Kafka the position (offset) of the record that `kafka-source` received, so that the record is not received again after a restart.

Use it to count a record as read only once it was handled, for example once it was written to a database: put it at the end of a flow that starts with `kafka-source`. The records after the last saved position are read again after a restart. For `kafka-batch-source` use `kafka-batch-manual-commit-action`.

Input: any message from `kafka-source` with `allowManualCommit` set to true and `autoCommitEnable` set to false. It uses the `CamelKafkaManualCommit` header that the source then sets.

Output: the message is unchanged.

Good to know: without the `CamelKafkaManualCommit` header, for example when `allowManualCommit` is false, it does nothing and does not fail. Saving the position of a record also counts the earlier records of its partition as read.

## Configuration Options

The `kafka-manual-commit-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `kafka-manual-commit-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kafka
    
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
            uri: "kamelet:kafka-manual-commit-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-manual-commit-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-manual-commit-action.kamelet.yaml)
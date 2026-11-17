# ![is tombstone filter action](_images/kamelets/is-tombstone-filter-action.svg) Is Tombstone Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Drops the Kafka records that have no value, called tombstones, and passes on all other messages unchanged.

Use it to skip tombstones, which mark a key as deleted in a compacted topic, after `kafka-source` when the next step cannot handle a message without a body.

Input: any message.

Output: the same message, unchanged, when it has a body. A message with no body, or with empty text as its body, is dropped and nothing is sent on.

## Configuration Options

The `is-tombstone-filter-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `is-tombstone-filter-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:is-tombstone-filter-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/is-tombstone-filter-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/is-tombstone-filter-action.kamelet.yaml)
# ![insert header action](_images/kamelets/insert-header-action.svg) Insert Header Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Adds a header to each message, or replaces it, with a fixed text or a value taken from the message.

Use it to give a sink the headers it reads, such as the `ce-projectKey` header of `jira-add-issue-sink`, to tag messages with where they come from, or to copy the body into a header for a later step. To set the key of a Kafka record, `set-kafka-key-action` is simpler.

Input: any message.

Output: the same body. The header named by `name` is set to `value`, and replaces a header of the same name.

Good to know: `value` is written in the Camel Simple language: plain text is used as it is, and the `${…​}` parts are filled in from the message, such as `${body}` for the body, or `${header.source}` for the value of the header `source`.

## Configuration Options

The following table summarizes the configuration options available for the `insert-header-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **name** | Header Name | **Required** The name of the header to set, such as `source`. With Knative, the name must start with `ce-`, the prefix of the CloudEvent attributes. | string |  | source |
| **value** | Header Value | **Required** The value of the header: plain text, such as `orders-app`, or a Simple expression whose `$\{…​}` parts are filled in from the message, such as `$\{body}` or `$\{header.customerId}`. | string |  | ${header.customerId} |

## Dependencies

At runtime, the `insert-header-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:insert-header-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/insert-header-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/insert-header-action.kamelet.yaml)
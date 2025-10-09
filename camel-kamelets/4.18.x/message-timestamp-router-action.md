# ![message timestamp router action](_images/kamelets/message-timestamp-router-action.svg) Message Timestamp Router Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Update the topic field as a function of the original topic name and the record’s timestamp field.

## Configuration Options

The following table summarizes the configuration options available for the `message-timestamp-router-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **timestampKeys** | Timestamp Keys | **Required** Comma separated list of Timestamp keys. The timestamp is taken from the first found field. | string |  |  |
| **timestampFormat** | Timestamp Format | Format string for the timestamp that is compatible with java.text.SimpleDateFormat. | string | yyyyMMdd |  |
| **timestampKeyFormat** | Timestamp Keys Format | Format of the timestamp keys. Possible values are `timestamp`, or any format string for the timestamp that is compatible with `java.text.SimpleDateFormat`. In case of `timestamp` the field is evaluated as milliseconds since 1970 (as a UNIX Timestamp). | string | timestamp |  |
| **topicFormat** | Topic Format | Format string which can contain '$\[topic\]' and '$\[timestamp\]' as placeholders for the topic and timestamp, respectively. | string | topic-$\[timestamp\] |  |

## Dependencies

At runtime, the `message-timestamp-router-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:core
    
-   camel:kafka
    

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
            uri: "kamelet:message-timestamp-router-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/message-timestamp-router-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/message-timestamp-router-action.kamelet.yaml)
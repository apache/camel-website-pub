# ![timestamp router action](_images/kamelets/timestamp-router-action.svg) Timestamp Router Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Update the topic field as a function of the original topic name and the record timestamp.

## Configuration Options

The following table summarizes the configuration options available for the `timestamp-router-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **timestampFormat** | Timestamp Format | Format string for the timestamp that is compatible with java.text.SimpleDateFormat. | string | yyyyMMdd |  |
| **timestampHeaderName** | Timestamp Header Name | The name of the header containing a timestamp. | string | CamelKafkaTimestamp |  |
| **topicFormat** | Topic Format | Format string which can contain '$\[topic\]' and '$\[timestamp\]' as placeholders for the topic and timestamp, respectively. | string | topic-$\[timestamp\] |  |

## Dependencies

At runtime, the `timestamp-router-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:timestamp-router-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/timestamp-router-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/timestamp-router-action.kamelet.yaml)
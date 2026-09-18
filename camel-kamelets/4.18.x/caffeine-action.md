# ![caffeine action](_images/kamelets/caffeine-action.svg) Caffeine Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Perform operations on a caffeine cache

## Configuration Options

The following table summarizes the configuration options available for the `caffeine-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **cacheName** | Cache name | **Required** The name of the cache we want to use. | string | caffeine-cache |  |

## Dependencies

At runtime, the `caffeine-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:caffeine
    
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
            uri: "kamelet:caffeine-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/caffeine-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/caffeine-action.kamelet.yaml)
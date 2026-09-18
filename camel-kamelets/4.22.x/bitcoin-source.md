# ![bitcoin source](_images/kamelets/bitcoin-source.svg) Bitcoin Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Provides a feed of the value of the Bitcoin compared to USDT using the Binance service.

## Configuration Options

The following table summarizes the configuration options available for the `bitcoin-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **period** | Period between Updates | The interval between updates in milliseconds. | integer | 10000 |  |

## Dependencies

At runtime, the `bitcoin-source` Kamelet relies upon the presence of the following dependencies:

-   camel:xchange
    
-   camel:kamelet
    
-   camel:jackson
    
-   camel:timer
    

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
      uri: "kamelet:bitcoin-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Bitcoin Source Kamelet Description

This is a simple Kamelet providing a feed of the value of the Bitcoin compared to USDT using the Binance service.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/bitcoin-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/bitcoin-source.kamelet.yaml)
# ![bitcoin source](_images/kamelets/bitcoin-source.svg) Bitcoin Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the current price of Bitcoin in USDT (Tether) from the public market data of the Binance trading platform at a regular interval, one message per reading.

Use it to follow the Bitcoin price, for example to store it over time, to send an alert when it crosses a threshold, or as a live data feed for a demo. It reads market prices from Binance; it does not connect to a Bitcoin node or wallet.

Output: the body is JSON text with the ticker of the BTC/USDT pair: among others the last price (`last`), the best bid and ask (`bid`, `ask`), the high and low (`high`, `low`) and the volume (`volume`) of the last 24 hours. The `Content-Type` header is `application/json`.

Good to know: it needs access to the internet and no account or key. The first reading comes about one second after start, then one every `period`.

## Configuration Options

The following table summarizes the configuration options available for the `bitcoin-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **period** | Period between Updates | How long to wait between two readings, in milliseconds. For example, 60000 is one minute. | integer | 10000 | 60000 |

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
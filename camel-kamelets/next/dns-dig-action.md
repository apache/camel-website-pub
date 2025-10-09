# ![dns dig action](_images/kamelets/dns-dig-action.svg) DNS DIG Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Query a DNS through Dig.

## Configuration Options

The `dns-dig-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `dns-dig-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:dns
    
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
            uri: "kamelet:dns-dig-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/dns-dig-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/dns-dig-action.kamelet.yaml)
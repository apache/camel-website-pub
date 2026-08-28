# ![dns lookup action](_images/kamelets/dns-lookup-action.svg) DNS Lookup Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Lookup for a domain

## Configuration Options

The `dns-lookup-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `dns-lookup-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:jackson
    
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
            uri: "kamelet:dns-lookup-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/dns-lookup-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/dns-lookup-action.kamelet.yaml)
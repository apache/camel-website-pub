# ![predicate filter action](_images/kamelets/predicate-filter-action.svg) Predicate Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Filter based on a JSONPath Expression. Since this is a filter, the expression is a negation. This means that if the `foo` field of the example is equal to `John`, the message goes ahead. Otherwise it is filtered out.

## Configuration Options

The following table summarizes the configuration options available for the `predicate-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **expression** | Expression | **Required** The JSONPath Expression to evaluate, without the external parenthesis. Since this is a filter, the expression is a negation. This means that if the `foo` field of the example is equal to `John`, the message goes ahead. Otherwise it is filtered out. | string |  | @.foo =~ /.\*John/ |

## Dependencies

At runtime, the `predicate-filter-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kamelet
    
-   camel:jsonpath
    

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
            uri: "kamelet:predicate-filter-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/predicate-filter-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/predicate-filter-action.kamelet.yaml)
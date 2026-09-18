# ![drop headers action](_images/kamelets/drop-headers-action.svg) Drop Headers Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Remove headers from the message in transit based on a pattern.

## Configuration Options

The following table summarizes the configuration options available for the `drop-headers-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **pattern** | Pattern | **Required** Name or pattern of headers to remove. The pattern is matched in the following order, 1 = exact match 2 = wildcard (pattern ends with a and the name starts with the pattern) 3 = regular expression (all of above is case in-sensitive). | string |  | Camel\* |
| **excludePattern** | Exclusion Pattern | Name or pattern of headers to not remove. The pattern is matched in the following order, 1 = exact match 2 = wildcard (pattern ends with a and the name starts with the pattern) 3 = regular expression (all of above is case in-sensitive). | string |  | Camel\* |

## Dependencies

At runtime, the `drop-headers-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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
            uri: "kamelet:drop-headers-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/drop-headers-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/drop-headers-action.kamelet.yaml)
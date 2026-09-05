# ![replace field action](_images/kamelets/replace-field-action.svg) Replace Field Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Replace field with a different key in the message in transit.

Only top level fields are considered. Fields nested inside an object are passed through untouched, so a rename that names a nested field has no effect.

## Configuration Options

The following table summarizes the configuration options available for the `replace-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **renames** | Renames | **Required** Comma separated list of field with new value to be renamed. Only top level fields are renamed; naming a field nested inside an object has no effect. | string |  | foo:bar,c1:c2 |
| **disabled** | Disabled | Comma separated list of top level fields to be disabled. | string | none |  |
| **enabled** | Enabled | Comma separated list of top level fields to be enabled. | string | all |  |

## Dependencies

At runtime, the `replace-field-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:jackson
    
-   camel:kamelet
    
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
            uri: "kamelet:replace-field-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/replace-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/replace-field-action.kamelet.yaml)
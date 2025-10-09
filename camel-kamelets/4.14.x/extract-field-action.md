# ![extract field action](_images/kamelets/extract-field-action.svg) Extract Field Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Extract a field from the message body.

## Configuration Options

The following table summarizes the configuration options available for the `extract-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **field** | Field | **Required** The name of the field to extract. | string |  |  |
| **headerOutput** | Header Output | If enable the action will store the extracted field in an header named CamelKameletsExtractFieldName. | boolean | false |  |
| **headerOutputName** | Header Output Name | A custom name for the header containing the extracted field. | string | none |  |
| **strictHeaderCheck** | Strict Header Check | If enabled the action will check if the header output name (custom or default) has been used already in the exchange. If so, the extracted field is stored in the message body, if not, the extracted field is stored in the selected header (custom or default). | boolean | false |  |
| **trimField** | Trim Field | If enabled we return the Raw extracted field. | boolean | false |  |

## Dependencies

At runtime, the `extract-field-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    
-   camel:jackson
    
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
            uri: "kamelet:extract-field-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/extract-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/extract-field-action.kamelet.yaml)
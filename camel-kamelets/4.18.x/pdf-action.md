# ![pdf action](_images/kamelets/pdf-action.svg) PDF Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Create a PDF.

## Configuration Options

The following table summarizes the configuration options available for the `pdf-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **font** | Font | **Required** The font to use while generating the PDF. One of Courier, Courier-Bold, Courier-Oblique, Courier-BoldOblique, Helvetica, Helvetica-Bold, Helvetica-Oblique, Helvetica-BoldOblique, Times-Roman, Times-Bold, Times-Italic, Times-BoldItalic, Symbol, ZapfDingbats. | string | Helvetica |  |
| **fontSize** | Font Size | **Required** The Font size to use while generating the PDF. | string | 14 |  |
| **pageSize** | Page Size | **Required** The Page size to use while generating the PDF. One of LETTER, LEGAL, A0, A1, A2, A3, A4, A5, A6. | string | A4 |  |

## Dependencies

At runtime, the `pdf-action` Kamelet relies upon the presence of the following dependencies:

-   camel:pdf
    
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
            uri: "kamelet:pdf-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pdf-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pdf-action.kamelet.yaml)
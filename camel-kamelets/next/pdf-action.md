# ![pdf action](_images/kamelets/pdf-action.svg) PDF Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Turns the text of each message into a PDF document, with one font, font size and page size for the whole text.

Use it to produce a simple printable document, such as a receipt, a report or a log, that is then stored as a file or sent by email. To lay out the text first, put a template action before it, such as `mustache-template-action`.

Input: the body is the text to write, as text. Each line of the text starts a new line in the PDF, and a new page starts when a page is full.

Output: the body is the PDF document, as bytes. The headers are kept as they are; a `Content-Type` header set before is not changed to PDF.

Good to know: long lines are not wrapped; they run past the right edge of the page. Set `font` to one of the names its description lists, such as `HELVETICA`, the default. Headers that start with `CamelPdf` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `pdf-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **font** | Font | **Required** The font of the whole text, one of the standard PDF fonts: `COURIER`, `COURIER_BOLD`, `COURIER_OBLIQUE`, `COURIER_BOLD_OBLIQUE`, `HELVETICA`, `HELVETICA_BOLD`, `HELVETICA_OBLIQUE`, `HELVETICA_BOLD_OBLIQUE`, `TIMES_ROMAN`, `TIMES_BOLD`, `TIMES_ITALIC`, `TIMES_BOLD_ITALIC`, `SYMBOL` or `ZAPF_DINGBATS`. Write the name in capitals with underscores: `Helvetica` or `Times-Roman` fails each message. | string | HELVETICA | HELVETICA |
| **fontSize** | Font Size | **Required** The size of the text, in points, such as `12` or `10.5`. 72 points make one inch. | string | 14 |  |
| **pageSize** | Page Size | **Required** The size of the pages: `A0` to `A6` (`A4` is 210 by 297 millimetres), `LETTER` (8.5 by 11 inches) or `LEGAL` (8.5 by 14 inches). Enum values: \* LETTER \* LEGAL \* A0 \* A1 \* A2 \* A3 \* A4 \* A5 \* A6 | string | A4 |  |

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
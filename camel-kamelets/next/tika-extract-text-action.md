# ![tika extract text action](_images/kamelets/tika-extract-text-action.svg) Tika Extract Text Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Extract plain text from PDF, office and similar documents in-process with Apache Tika.

Before the parse, the value of the `documentIdHeader` header is captured into the `CamelLangChain4jIngestDocumentId` exchange property - Tika copies document metadata over the headers, so a crafted document could otherwise forge its own identity in steps that read it later (the langchain4j-ingest sink does). The extracted text is decoded at a pinned UTF-8 (a document-injected charset header is swept before the conversion), and after the parse all non-Camel headers are removed: past this action, parsed document metadata is indistinguishable from caller headers, so it must not travel further. Each format needs its Tika parser module on the classpath; camel-tika ships the HTML and text modules, PDF needs org.apache.tika:tika-parser-pdf-module.

## Configuration Options

The following table summarizes the configuration options available for the `tika-extract-text-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **documentIdHeader** | Document Id Header | Name of the header carrying the stable document id, captured into the CamelLangChain4jIngestDocumentId exchange property before the parse. | string | CamelLangChain4jIngestDocumentId |  |

## Dependencies

At runtime, the `tika-extract-text-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:tika
    
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
            uri: "kamelet:tika-extract-text-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/tika-extract-text-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/tika-extract-text-action.kamelet.yaml)
Kamelet Catalog

# ![docling convert action](_images/kamelets/docling-convert-action.svg) Docling Convert Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Convert PDF, office and similar documents to structure-preserving markdown with Docling, OCR included.

Before the conversion, the value of the `documentIdHeader` header is captured into the `CamelLangChain4jIngestDocumentId` exchange property, so a converted document cannot forge its own identity in steps that read it later (the langchain4j-ingest sink does); the body is pinned to bytes and the `CamelDocling*` control headers are swept, because none of them may be decided by a consumer-delivered payload. By default the `docling` component executes a local docling CLI; set `doclingServeUrl` to use a Docling Serve instance instead - the natural fit for self-contained Pipes.

## Configuration Options

The following table summarizes the configuration options available for the `docling-convert-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **doclingServeUrl** | Docling Serve URL | Address of a Docling Serve instance to convert through, such as [http://docling-serve:5001](http://docling-serve:5001); when unset, the docling component’s own configuration applies (a local docling CLI by default). | string |  |  |
| **documentIdHeader** | Document Id Header | Name of the header carrying the stable document id, captured into the CamelLangChain4jIngestDocumentId exchange property before the conversion. | string | CamelLangChain4jIngestDocumentId |  |
| **useDoclingServe** | Use Docling Serve | Whether to convert through a Docling Serve instance instead of a local docling CLI; set together with doclingServeUrl. | boolean |  |  |

## Dependencies

At runtime, the `docling-convert-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:docling
    
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
            uri: "kamelet:docling-convert-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/docling-convert-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/docling-convert-action.kamelet.yaml)
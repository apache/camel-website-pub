# ![langchain4j ingest file source](_images/kamelets/langchain4j-ingest-file-source.svg) LangChain4j Ingest File Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Watch a directory as the source of an ingestion pipeline, with the defaults a knowledge base needs: documents are left in place (noop), unchanged files are remembered in a duplicate register keyed on path, modification time and size, a file still being copied in is waited for (readLock=changed), and the file name is exposed as the document id in the CamelLangChain4jIngestDocumentId header.

Mind the two dedup layers when composing: this source re-delivers an edited file (its register key changes with the modification time), but a langchain4j-ingest-sink with an idempotentRepository is first-write-wins by document id - the re-delivered edit would be skipped. Use a version-aware id, or no sink repository, when documents change.

## Configuration Options

The following table summarizes the configuration options available for the `langchain4j-ingest-file-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **directory** | Directory | **Required** The directory to ingest documents from. | string |  |  |
| **charset** | Charset | Character set for reading text documents, for example UTF-8. Leave unset when the source feeds a parser action (tika-extract-text-action or docling-convert-action), which must receive the raw bytes - a charset conversion would corrupt a binary document such as a PDF. | string |  |  |
| **delay** | Delay | Milliseconds between directory polls; the file endpoint’s default is 500ms, which is aggressive for a knowledge-base directory. | integer |  |  |
| **exclude** | Exclude | Comma-separated Ant-style patterns for files to skip, for example `***/draft-**`. Exclusion wins over inclusion. | string |  |  |
| **idempotentRepository** | Idempotent Repository | An IdempotentRepository bean remembering already consumed files, as a `#bean:name` reference; the register is keyed on path, modification time and size, so an edited file is consumed again. When unset, the file endpoint’s default in-memory register (1000 entries) applies - eviction on a large directory re-ingests files, so supply a sized or persistent repository for a real knowledge base. | string |  |  |
| **include** | Include | Comma-separated Ant-style patterns for files to ingest, matched on the path relative to the directory, for example `**/**.pdf,**/**.md`. When unset, every file is ingested. | string |  |  |
| **recursive** | Recursive | Whether subdirectories are ingested too. | boolean | true |  |

## Dependencies

At runtime, the `langchain4j-ingest-file-source` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:file
    
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
      uri: "kamelet:langchain4j-ingest-file-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/langchain4j-ingest-file-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/langchain4j-ingest-file-source.kamelet.yaml)
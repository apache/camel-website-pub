# ![azure functions sink](_images/kamelets/azure-functions-sink.svg) Azure Function Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Forward data to an Azure Function.

## Configuration Options

The following table summarizes the configuration options available for the `azure-functions-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The Azure Functions URL you want to send the data to. | string |  | https://azure-function-demo-12234.azurewebsites.net/api/httpexample |
| **key** | Key | A function-specific API key is required, if the authLevel of the function is FUNCTION or master key if the authLevel is ADMIN. | string |  |  |
| **method** | Method | The HTTP method to use. Enum values: \* GET \* POST \* PUT \* DELETE \* HEAD \* OPTIONS \* TRACE \* PATCH | string | POST |  |

## Dependencies

At runtime, the `azure-functions-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:vertx-http
    
-   camel:kamelet
    
-   camel:core
    

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
            uri: "kamelet:azure-functions-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Functions Sink Kamelet Description

### Authentication methods

In this Kamelet you should access the function on Azure through a key token in the key parameter.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-functions-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-functions-sink.kamelet.yaml)
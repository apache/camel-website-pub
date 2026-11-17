# ![azure functions sink](_images/kamelets/azure-functions-sink.svg) Azure Function Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Calls a function in Azure Functions over HTTP for each message, with the message as the body of the request.

Use it to run your own serverless code on each message, such as an enrichment, a notification or a calculation. For any other web service, use `http-sink`.

Input: the body is sent as the request body, as text, bytes or a stream. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The `Content-Type` header is sent as the content type of the request, and the other headers of the message, except the Camel ones, are sent as HTTP headers.

Output: when it is used inside a route, the body afterwards is the response of the function, and the `CamelHttpResponseCode` header its status code.

Good to know: a response with a status code outside 200 to 299 fails the message. The `key` is sent as the `code` query parameter of the request.

## Configuration Options

The following table summarizes the configuration options available for the `azure-functions-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The address of the function, which starts with `https://`, from the Azure portal: the function, then Get function URL. Leave out the `?code=` part: put the key in `key`. | string |  | https://azure-function-demo-12234.azurewebsites.net/api/httpexample |
| **key** | Key | A function key, or the master key, from the Azure portal: the function, then Function Keys. Needed when the authorization level of the function is `function` or `admin`; leave it empty for `anonymous`. | string |  |  |
| **method** | Method | The HTTP method of the request, which must be one that the function accepts. Enum values: \* GET \* POST \* PUT \* DELETE \* HEAD \* OPTIONS \* TRACE \* PATCH | string | POST |  |

## Dependencies

At runtime, the `azure-functions-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:vertx-http
    
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
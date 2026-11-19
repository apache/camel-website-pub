# ![ogcapi features action](_images/kamelets/ogcapi-features-action.svg) OGC Api Feature Get Item Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Fetches the features of one collection, such as the lakes or the buildings of an area, from a server that implements the OGC API Features standard, and gives them as GeoJSON.

Use it to bring map data from a geographic data service into a flow, for example to load the features of an area into a database or to check them against a list of places.

Input: the body, when it is not empty, is added to the query of the request, as text such as `name=Lake Baikal`, so each message can ask for other features. An empty body asks only with the options.

Output: the body is a GeoJSON feature collection, as JSON text, with at most `limit` features. The headers of the HTTP response, such as `Content-Type`, are set as headers.

Good to know: `split` does not change what the next step receives: it still gets the whole collection, once per message. An HTTP error from the server, such as an unknown collection, fails the message. Headers that start with `CamelHttp` or `CamelRestHttp` are removed from the message first, so they cannot change what the Kamelet does. A service that cannot be reached within `connectTimeout`, or does not answer within `responseTimeout`, fails the message; when they are not set, it waits up to 3 minutes.

## Configuration Options

The following table summarizes the configuration options available for the `ogcapi-features-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | Collection | **Required** The id of the collection to read the features from, as listed by the service at `<url>/collections`. | string |  | lakes |
| **url** | URL | **Required** The address of the OGC API Features service, the part before `/collections`. It must start with `http://` or `https://`. | string |  | https://demo.pygeoapi.io/master |
| **bbox** | Bounding Box | The area to read the features from, as four numbers separated by commas: the west longitude, the south latitude, the east longitude and the north latitude, in degrees. The default is the whole world. | string | \-180,-90,180,90 | 160.6,-55.95,-170,-25.89 |
| **connectTimeout** | Connect Timeout | How long to wait for the connection to the service to be set up, in milliseconds. When it is not set, it waits up to 3 minutes, or less when the operating system gives up first. A service that cannot be reached in time fails the message. | integer |  | 5000 |
| **limit** | Limit | The largest number of features to read for each message, between 1 and 10000. | integer | 10 |  |
| **query** | Query | More query parameters for every request, in the form `name=value`, separated by `&`, such as filters on the properties of the features that the service supports. | string |  | property1=1&property2=dos |
| **responseTimeout** | Response Timeout | How long to wait for the answer of the service once the request is sent, in milliseconds. When it is not set, it is 180000 (3 minutes). A service that does not answer in time fails the message. | integer |  | 30000 |
| **split** | Split by Feature | Meant to give each feature as a message of its own. In a route or a Pipe it does not change what the next step receives: the whole feature collection. | boolean | false |  |

## Dependencies

At runtime, the `ogcapi-features-action` Kamelet relies upon the presence of the following dependencies:

-   camel:http
    
-   camel:kamelet
    
-   camel:jsonpath
    
-   camel:jackson3
    

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
            uri: "kamelet:ogcapi-features-action"
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

## OGC API Features Action Kamelet Description

### Timeouts

`connectTimeout` limits how long to wait for the connection to the service, and `responseTimeout` how long to wait for its answer, both in milliseconds. A service that does not answer in time fails the message. When they are not set, the answer is awaited for up to 3 minutes.

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 60000
        message: ""
      steps:
        - to:
            uri: "kamelet:ogcapi-features-action"
            parameters:
              url: "https://features.example.com/ogcapi"
              collection: "lakes"
              connectTimeout: 5000
              responseTimeout: 30000
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ogcapi-features-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ogcapi-features-action.kamelet.yaml)
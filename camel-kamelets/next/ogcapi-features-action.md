# ![ogcapi features action](_images/kamelets/ogcapi-features-action.svg) OGC Api Feature Get Item Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Returns the items of the collection provided of an OGC API Features server.

## Configuration Options

The following table summarizes the configuration options available for the `ogcapi-features-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | Collection | **Required** Name of the collection we want to extract items from. | string |  |  |
| **url** | URL | **Required** The URL to fetch for data. | string |  | https://emotional.byteroad.net |
| **bbox** | Bounding Box | Bounding Box of the items we want to retrieve. | string | \-180,-90,180,90 | 160.6,-55.95,-170,-25.89 |
| **limit** | Limit | Maximum number of items to retrieve. Must be a number between 1 and 10 000. | integer | 10 |  |
| **query** | Query | Separated list by `&` of properties we want to query. | string |  | property1=1&property2=dos |
| **split** | Split by Feature | When true, instead of returning the full geojson, split the message into each feature. | boolean | false |  |

## Dependencies

At runtime, the `ogcapi-features-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:http
    
-   camel:kamelet
    
-   camel:jsonpath
    
-   camel:jackson
    

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ogcapi-features-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ogcapi-features-action.kamelet.yaml)
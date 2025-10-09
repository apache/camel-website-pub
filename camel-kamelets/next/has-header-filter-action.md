# ![has header filter action](_images/kamelets/has-header-filter-action.svg) Has Header Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Filter message based on the presence of one header.

## Configuration Options

The following table summarizes the configuration options available for the `has-header-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **name** | Header Name | **Required** The header name to evaluate. The header name must be passed by the source Kamelet. For Knative only, the name of the header requires a CloudEvent (ce-) prefix. | string |  | headerName |
| **value** | Header Value | An optional header value to compare the header to. | string |  | headerValue |

## Dependencies

At runtime, the `has-header-filter-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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
            uri: "kamelet:has-header-filter-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/has-header-filter-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/has-header-filter-action.kamelet.yaml)
# ![drop header action](_images/kamelets/drop-header-action.svg) Drop Header Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Removes one header, given by its name, from each message.

Use it to remove a header that the next step must not see, for example an `Authorization` header with a secret, or a header that would change what a sink does. To remove several headers at once by a pattern, such as all the headers whose names start with `Camel`, use `drop-headers-action`.

Input: any message.

Output: the same body, and the same headers without the one named by `name`. A message without that header passes on unchanged.

Good to know: the name is not case-sensitive: `FOO` also removes the header `foo`.

## Configuration Options

The following table summarizes the configuration options available for the `drop-header-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **name** | Header Name | **Required** The name of the header to remove, such as `Authorization`. Upper and lower case do not matter. | string |  | Authorization |

## Dependencies

At runtime, the `drop-header-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:drop-header-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/drop-header-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/drop-header-action.kamelet.yaml)
# ![wttrin source](_images/kamelets/wttrin-source.svg) wttr.in Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Fetches the current weather or the forecast for a place from the public wttr.in service at a regular interval, and sends it as JSON.

Use it to feed weather data into a dashboard, a chat message or a decision, such as a frost alert, or as real, changing JSON data for a demo. No account is needed.

Output: the body is JSON text. With `output` set to `current`, the default, it is an object with the current conditions, such as `temp_C`, `humidity` and `weatherDesc`. With `weather`, it is a list with the forecast for each day, starting today. With `full`, it is the whole answer of wttr.in, which has both. The `Content-Type` header is `application/json`, and the other headers of the HTTP answer are kept.

Good to know: it calls `[https://wttr.in](https://wttr.in)` over the internet. When `wttrLocation` is not set, wttr.in guesses the place from the IP address of the machine.

## Configuration Options

The following table summarizes the configuration options available for the `wttrin-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **output** | Output | What to send: `current` for the current conditions, `weather` for the forecast of each day, or `full` for the whole answer of wttr.in. Any other value works like `full`. | string | current | weather |
| **period** | Period | How long to wait between two fetches, in milliseconds. For example, 3600000 is one hour. | integer | 60000 | 3600000 |
| **wttrLanguage** | Language | The language of the weather descriptions, as a language code such as `fr` or `de`. The descriptions in that language are added to the JSON in a field such as `lang_fr`; the other fields stay in English. When it is not set, the descriptions are in English only. | string |  | fr |
| **wttrLocation** | Location | The place to get the weather for: a city name such as `Paris` or `New York`, an airport code such as `muc`, a landmark after `~` such as `~Eiffel+tower`, a postal code, or a latitude and longitude such as `48.85,2.35`. When it is not set, wttr.in guesses the place from the IP address of the machine. | string |  | Paris |

## Dependencies

At runtime, the `wttrin-source` Kamelet relies upon the presence of the following dependencies:

-   camel:http
    
-   camel:jackson
    
-   camel:jsonpath
    
-   camel:kamelet
    
-   camel:timer
    

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
      uri: "kamelet:wttrin-source"
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

## Wttrin Source Kamelet Description

### Authentication

The Kamelet calls the public `[https://wttr.in](https://wttr.in)` service, which needs no account, API key or credentials.

### Output format

The Kamelet fetches data from wttr.in and produces the data in JSON format.

### Configuration

No option is required:

-   `wttrLocation`: the place to get the weather for; when it is not set, wttr.in guesses the place from the IP address of the machine
    
-   `wttrLanguage`: the language of the weather descriptions
    
-   `output`: `current`, `weather` or `full`
    
-   `period`: how long to wait between two fetches, in milliseconds
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: wttrin-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: wttrin-source
    properties:
      wttrLocation: Paris
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/wttrin-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/wttrin-source.kamelet.yaml)
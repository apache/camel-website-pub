# ![nats source](_images/kamelets/nats-source.svg) NATS Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from NATS topics.

## Configuration Options

The following table summarizes the configuration options available for the `nats-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **servers** | Servers | **Required** Comma separated list of NATS Servers. | string |  |  |
| **topic** | Topic | **Required** NATS Topic name. | string |  |  |
| **jetstreamAsync** | Jetstream Async Enabled | Sets whether to operate JetStream requests asynchronously. | boolean | true |  |
| **jetstreamEnabled** | Jetstream Enabled | Sets whether to enable JetStream support for this endpoint. | boolean | false |  |
| **jetstreamName** | Jetstream Stream Name | Sets the name of the JetStream stream to use. | string |  |  |

## Dependencies

At runtime, the `nats-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:nats
    
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
      uri: "kamelet:nats-source"
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

## Nats Source Kamelet Description

### Authentication methods

This Kamelet connects to Nats using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Nats and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Nats:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: nats-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: nats-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-source.kamelet.yaml)
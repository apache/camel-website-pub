Kamelet Catalog

# ![sap netweaver sink](_images/kamelets/sap-netweaver-sink.svg) SAP NetWeaver Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Send requests to an SAP NetWeaver Gateway over HTTP.

The command property is the OData command to run against the gateway, and is pinned by this Kamelet rather than taken from the message.

## Configuration Options

The following table summarizes the configuration options available for the `sap-netweaver-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **command** | Command | **Required** The OData command to run against the gateway. It is sent as the request path. | string |  | FlightCollection(carrid='AA',connid='0017',fldate=datetime'2024-01-01T00%3A00%3A00') |
| **password** | Password | **Required** The password to authenticate against the gateway. | string |  |  |
| **url** | URL | **Required** The URL of the SAP NetWeaver Gateway server. | string |  | https://gateway.example.com/sap/opu/odata/sap/ZDEMO\_SRV |
| **username** | Username | **Required** The username to authenticate against the gateway. | string |  |  |
| **flatternMap** | Flatten Map | When the returned Map holds a single entry, use that entry value as the message body. | boolean | true |  |
| **json** | JSON | Return data as JSON. When false the gateway returns XML in Atom format instead. | boolean | true |  |
| **jsonAsMap** | JSON As Map | Transform the returned JSON from a String into a Map in the message body. | boolean | true |  |

## Dependencies

At runtime, the `sap-netweaver-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:sap-netweaver
    
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
            uri: "kamelet:sap-netweaver-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/sap-netweaver-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/sap-netweaver-sink.kamelet.yaml)
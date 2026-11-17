# ![sap netweaver sink](_images/kamelets/sap-netweaver-sink.svg) SAP NetWeaver Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Reads data from an SAP NetWeaver Gateway with an OData GET request, the same request for each message, and gives the answer as a Map or as JSON text.

Use it to fetch business data from SAP, such as flights, orders or materials, for example on a schedule with `timer-source`, and pass it on to another system.

Input: any body; it is not sent. The request is always the `command` option, added to `url`; headers on the message cannot change it.

Output: when it is used inside a route, the body afterwards is the answer of the gateway. By default it is a Map, and the outer `d` entry of the OData answer is removed, so the body holds the `results` list or the fields of the entity. With `jsonAsMap` set to false it is JSON text, and with `json` set to false it is XML text in the Atom format.

Good to know: the body is never sent, so this Kamelet cannot create or change data in SAP. A response that is not JSON fails the message while `json` and `jsonAsMap` are true.

## Configuration Options

The following table summarizes the configuration options available for the `sap-netweaver-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **command** | Command | **Required** The OData request to run, added to `url` as the rest of the path, such as an entity set (`FlightCollection`), one entity by its key, and OData query options. | string |  | FlightCollection(carrid='AA',connid='0017',fldate=datetime'2024-01-01T00%3A00%3A00') |
| **password** | Password | **Required** The password of the SAP user in `username`. | string |  |  |
| **url** | URL | **Required** The address of the OData service on the SAP NetWeaver Gateway, up to the name of the service, starting with `https://`. | string |  | https://gateway.example.com/sap/opu/odata/sap/ZDEMO\_SRV |
| **username** | Username | **Required** The SAP user to log in to the gateway as, with Basic authentication. | string |  |  |
| **flatternMap** | Flatten Map | If true, and the Map has only one entry, such as the `d` entry of an OData answer, the body is the value of that entry. Only used when `jsonAsMap` is true. | boolean | true |  |
| **json** | JSON | If true, the answer is asked for in JSON. If false, the gateway answers in XML, in the Atom format, and the body is that XML as text. | boolean | true |  |
| **jsonAsMap** | JSON As Map | If true, the JSON answer is read into a Map. If false, the body is the JSON text. Only used when `json` is true. | boolean | true |  |

## Dependencies

At runtime, the `sap-netweaver-sink` Kamelet relies upon the presence of the following dependencies:

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

## SAP NetWeaver Sink Kamelet Description

### The Command

The `command` property is the OData command to run against the gateway, and it becomes the request path.

The component reads the command from the `CamelNetWeaverCommand` header, which this Kamelet sets from the property. Setting it also overwrites any inbound value, so a caller cannot choose the request path.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/sap-netweaver-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/sap-netweaver-sink.kamelet.yaml)
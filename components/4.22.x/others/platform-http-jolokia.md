# Platform HTTP Jolokia

**Since Camel 4.5**

The Platform HTTP Jolokia component is used for Camel standalone to expose Jolokia over HTTP using the embedded management HTTP server.

Jolokia can be enabled as follows in `application.properties`:

```properties
camel.management.enabled = true
camel.management.jolokiaEnabled = true
```

After the application is started, you can query the Jolokia endpoint (default `/observe/jolokia`) as in this example:

$ curl [http://localhost:8080/observe/jolokia/list/org.apache.camel](http://localhost:8080/observe/jolokia/list/org.apache.camel) | jq { "request": { "path": "org.apache.camel", "type": "list" }, "value": { "context=test,name=\\"timer://yaml\\\\?period=1000\\",type=endpoints": { "op": { "getEndpointUri": { "args": \[\], "ret": "java.lang.String", "desc": "EndpointUri" },

## How to use it

This component acts as a Jolokia agent exposing HTTP endpoints to access JMX services. It looks for default restrictor policies located in `classpath:/jolokia-access.xml`, allowing by default access to all MBeans if no policy is found.

> **Warning**
> this may be exposing sensitive information, make sure to protect the access to the endpoints accurately.

Make sure to [include a security policy](https://jolokia.org/reference/html/manual/security.html#security-policy-location) as provided in Jolokia documentation to avoid any security problem.
# LRA

**Since Camel 2.21**

The LRA module provides bindings of the Saga EIP with any [MicroProfile compatible LRA Coordinator](https://github.com/eclipse/microprofile-lra).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-lra</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using lra with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-lra-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.lra.coordinator-context-path** | The context path of the LRA coordinator service. |  | String |
| **camel.lra.coordinator-url** | The base URL of the LRA coordinator service (e.g. [http://lra-host:8080](http://lra-host:8080)). |  | String |
| **camel.lra.enabled** | Global option to enable/disable component auto-configuration, default is true. | true | Boolean |
| **camel.lra.local-participant-context-path** | The context path of the local participant callback services. |  | String |
| **camel.lra.local-participant-url** | The local URL where the coordinator should send callbacks to (e.g. [http://my-host-name:8080](http://my-host-name:8080)). |  | String |
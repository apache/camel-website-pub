# LRA

**Since Camel 2.21**

The LRA module provides bindings of the [Saga EIP](../eips/saga-eip.md) with any [MicroProfile compatible LRA Coordinator](https://github.com/eclipse/microprofile-lra).

The configuration of the LRA Saga Service, including how to sign the callbacks that the LRA coordinator sends to the participant, is described in the [Saga EIP](../eips/saga-eip.md) page.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-lra</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```
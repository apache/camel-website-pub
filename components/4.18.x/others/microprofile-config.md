# Microprofile Config

**Since Camel 3.0**

The microprofile-config component is used for bridging the Eclipse MicroProfile Config with the Properties Component. This allows using configuration management from Eclipse MicroProfile with Camel.

To enable this, add this component to the classpath and Camel should auto-detect this when starting up.

## Usage

### Register manually

You can also register the microprofile-config component manually with the Apache Camel Properties Component as shown below:

```java
    PropertiesComponent pc = (PropertiesComponent) camelContext.getPropertiesComponent();
    pc.addPropertiesSource(new CamelMicroProfilePropertiesSource());
```
# Bean

JVM since0.1.0 Native since0.1.0

Invoke methods of Java beans

## What’s inside

-   [Bean component](../../../../components/4.14.x/bean-component.md), URI syntax: `bean:beanName`
    
-   [Bean Method language](../../../../components/4.14.x/languages/bean-language.md)
    
-   [Class component](../../../../components/4.14.x/class-component.md), URI syntax: `class:beanName`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-bean)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-bean</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

Except for invoking methods of beans available in Camel registry, Bean component and Bean method language can also invoke Quarkus CDI beans. For more details, please refer to the [CDI and the Camel Bean component](../../user-guide/cdi.html#_cdi_and_the_camel_bean_component) section of the User guide.
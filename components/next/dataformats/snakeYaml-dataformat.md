# YAML SnakeYAML

**Since Camel 2.17**

YAML is a Data Format to marshal and unmarshal Java objects to and from [YAML](http://www.yaml.org/).

For YAML to object marshalling, Camel provides integration with three popular YAML libraries:

-   The [SnakeYAML](https://bitbucket.org/snakeyaml/snakeyaml) library
    

Every library requires adding the special camel component (see "Dependency…​" paragraphs further down). By default Camel uses the SnakeYAML library.

## YAML Options

The YAML SnakeYAML dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **library** (common) | `SnakeYAML` | `Enum` | 
Which yaml library to use. By default it is SnakeYAML.

Enum values:

-   SnakeYAML
    





 |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |
| **constructor** (advanced) |  | `String` | BaseConstructor to construct incoming documents. |
| **representer** (advanced) |  | `String` | Representer to emit outgoing objects. |
| **dumperOptions** (advanced) |  | `String` | DumperOptions to configure outgoing objects. |
| **resolver** (advanced) |  | `String` | Resolver to detect implicit type. |
| **useApplicationContextClassLoader** (common) | `true` | `Boolean` | Use ApplicationContextClassLoader as custom ClassLoader. |
| **prettyFlow** (common) | `false` | `Boolean` | Force the emitter to produce a pretty YAML document when using the flow style. |
| **allowAnyType** (common) | `false` | `Boolean` | Allow any class to be un-marshaled. |
| **typeFilter** (advanced) |  | `String` | Set the types SnakeYAML is allowed to un-marshall. Multiple types can be separated by comma. |
| **maxAliasesForCollections** (advanced) | `50` | `Integer` | Set the maximum amount of aliases allowed for collections. |
| **allowRecursiveKeys** (advanced) | `false` | `Boolean` | Set whether recursive keys are allowed. |
> **Warning**
> SnakeYAML can load any class from YAML definition which may lead to security breach so by default, SnakeYAML DataForma restrict the object it can load to standard Java objects like List or Long. If you want to load custom POJOs you need to add theirs type to SnakeYAML DataFormat type filter list. If your source is trusted, you can set the property allowAnyType to true so SnakeYAML DataForma won’t perform any filter on the types.

## Using YAML data format with the SnakeYAML library

-   Turn Object messages into yaml then send to MQSeries
    
    -   Java
        
    -   XML
        
    -   YAML DSL
        
    
    ```java
    from("activemq:My.Queue")
        .marshal().yaml()
        .to("mqseries:Another.Queue");
    ```
    
    ```xml
    <route>
      <from uri="activemq:My.Queue"/>
      <marshal><yaml/></marshal>
      <to uri="mqseries:Another.Queue"/>
    </route>
    ```
    
    ```yaml
    - route:
        from:
          uri: activemq:My.Queue
          steps:
            - marshal:
                yaml: {}
            - to:
                uri: mqseries:Another.Queue
    ```
    

_Java-only: selecting the SnakeYAML library explicitly_

```java
from("activemq:My.Queue")
  .marshal().yaml(YAMLLibrary.SnakeYAML)
  .to("mqseries:Another.Queue");
```

-   Restrict classes to be loaded from YAML
    

_Java-only: programmatic type filter configuration_

```java
// Creat a SnakeYAMLDataFormat instance
SnakeYAMLDataFormat yaml = new SnakeYAMLDataFormat();

// Restrict classes to be loaded from YAML
yaml.addTypeFilters(TypeFilters.types(MyPojo.class, MyOtherPojo.class));

from("activemq:My.Queue")
  .unmarshal(yaml)
  .to("mqseries:Another.Queue");
```

## Using YAML in Spring DSL

When using Data Format in Spring DSL, you need to declare the data formats first. This is done in the **DataFormats** XML tag.

_XML-only: Spring XML data format definitions with type filters_

```xml
<dataFormats>
  <!--
    here we define a YAML data format with the id snake and that it should use
    the TestPojo as the class type when doing unmarshal. The unmarshalType
    is optional
  -->
  <yaml
    id="snake"
    library="SnakeYAML"
    unmarshalType="org.apache.camel.component.yaml.model.TestPojo"/>

  <!--
    here we define a YAML data format with the id snake-safe which restricts the
    classes to be loaded from YAML to TestPojo and those belonging to package
    com.mycompany
  -->
  <yaml id="snake-safe">
    <typeFilter value="org.apache.camel.component.yaml.model.TestPojo"/>
    <typeFilter value="com.mycompany\..*" type="regexp"/>
  </yaml>
</dataFormats>
```

And then you can refer to those ids in the route:

-   Java
    
-   XML
    
-   YAML DSL
    

```java
from("direct:unmarshal")
    .unmarshal("snake")
    .to("mock:unmarshal");

from("direct:unmarshal-safe")
    .unmarshal("snake-safe")
    .to("mock:unmarshal-safe");
```

```xml
<route>
  <from uri="direct:unmarshal"/>
  <unmarshal>
    <custom ref="snake"/>
  </unmarshal>
  <to uri="mock:unmarshal"/>
</route>
<route>
  <from uri="direct:unmarshal-safe"/>
  <unmarshal>
    <custom ref="snake-safe"/>
  </unmarshal>
  <to uri="mock:unmarshal-safe"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:unmarshal
      steps:
        - unmarshal:
            custom:
              ref: snake
        - to:
            uri: mock:unmarshal
- route:
    from:
      uri: direct:unmarshal-safe
      steps:
        - unmarshal:
            custom:
              ref: snake-safe
        - to:
            uri: mock:unmarshal-safe
```

## Dependencies for SnakeYAML

To use YAML in your camel routes, you need to add a dependency on `camel-snakeyaml` which implements this data format.

If you use maven, you could add the following to your `pom.xml`, substituting the version number for the latest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-snakeyaml</artifactId>
  <version>${camel-version}</version>
</dependency>
```
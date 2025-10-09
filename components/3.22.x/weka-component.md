# Weka

**Since Camel 3.1**

**Only producer is supported**

The Weka component provides access to the [(Weka Data Mining)](https://www.cs.waikato.ac.nz/ml/weka) toolset.

Weka is tried and tested open source machine learning software that can be accessed through a graphical user interface, standard terminal applications, or a Java API. It is widely used for teaching, research, and industrial applications, contains a plethora of built-in tools for standard machine learning tasks, and additionally gives transparent access to well-known toolboxes such as scikit-learn, R, and Deeplearning4j.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-weka</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

weka://cmd

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Weka component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Weka endpoint is configured using URI syntax:

weka:command

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **command** (producer) | 
**Required** The command to use.

Enum values:

-   filter
    
-   model
    
-   read
    
-   write
    
-   push
    
-   pop
    
-   version
    





 |  | Command |

### Query Parameters (10 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apply** (filter) | The filter spec (i.e. Name Options). |  | String |
| **build** (model) | The classifier spec (i.e. Name Options). |  | String |
| **dsname** (model) | The named dataset to train the classifier with. |  | String |
| **folds** (model) | Number of folds to use for cross-validation. | 10 | int |
| **loadFrom** (model) | Path to load the model from. |  | String |
| **saveTo** (model) | Path to save the model to. |  | String |
| **seed** (model) | An optional seed for the randomizer. | 1 | int |
| **xval** (model) | Flag on whether to use cross-validation with the current dataset. | false | boolean |
| **path** (write) | An in/out path for the read/write commands. |  | String |

## Samples

### Read + Filter + Write

This first example shows how to read a CSV file with the file component and then pass it on to Weka. In Weka we apply a few filters to the data set and then pass it on to the file component for writing.

```java
    @Override
    public void configure() throws Exception {

        // Use the file component to read the CSV file
        from("file:src/test/resources/data?fileName=sfny.csv")

        // Convert the 'in_sf' attribute to nominal
        .to("weka:filter?apply=NumericToNominal -R first")

        // Move the 'in_sf' attribute to the end
        .to("weka:filter?apply=Reorder -R 2-last,1")

        // Rename the relation
        .to("weka:filter?apply=RenameRelation -modify sfny")

        // Use the file component to write the Arff file
        .to("file:target/data?fileName=sfny.arff")
    }
```

Here we do the same as above without use of the file component.

```java
    @Override
    public void configure() throws Exception {

        // Initiate the route from somewhere
        .from("...")

        // Use Weka to read the CSV file
        .to("weka:read?path=src/test/resources/data/sfny.csv")

        // Convert the 'in_sf' attribute to nominal
        .to("weka:filter?apply=NumericToNominal -R first")

        // Move the 'in_sf' attribute to the end
        .to("weka:filter?apply=Reorder -R 2-last,1")

        // Rename the relation
        .to("weka:filter?apply=RenameRelation -modify sfny")

        // Use Weka to write the Arff file
        .to("weka:write?path=target/data/sfny.arff");
    }
```

In this example, would the client provide the input path or some other supported type. Have a look at the `WekaTypeConverters` for the set of supported input types.

```java
    @Override
    public void configure() throws Exception {

        // Initiate the route from somewhere
        .from("...")

        // Convert the 'in_sf' attribute to nominal
        .to("weka:filter?apply=NumericToNominal -R first")

        // Move the 'in_sf' attribute to the end
        .to("weka:filter?apply=Reorder -R 2-last,1")

        // Rename the relation
        .to("weka:filter?apply=RenameRelation -modify sfny")

        // Use Weka to write the Arff file
        .to("weka:write?path=target/data/sfny.arff");
    }
```

### Building a Model

When building a model, we first choose the classification algorithm to use and then train it with some data. The result is the trained model that we can later use to classify unseen data.

Here we train J48 with 10 fold cross-validation.

```java
try (CamelContext camelctx = new DefaultCamelContext()) {

    camelctx.addRoutes(new RouteBuilder() {

        @Override
        public void configure() throws Exception {

            // Use the file component to read the training data
            from("file:src/test/resources/data?fileName=sfny-train.arff")

            // Build a J48 classifier using cross-validation with 10 folds
            .to("weka:model?build=J48&xval=true&folds=10&seed=1")

            // Persist the J48 model
            .to("weka:model?saveTo=src/test/resources/data/sfny-j48.model")
        }
    });
    camelctx.start();
}
```

### Predicting a Class

Here we use a `Processor` to access functionality that is not directly available from endpoint URIs.

In case you come here directly and this syntax looks a bit overwhelming, you might want to have a brief look at the section about [Nessus API Concepts](https://tdiesler.github.io/nessus-weka/#_nessus_api_concepts).

```java
try (CamelContext camelctx = new DefaultCamelContext()) {

    camelctx.addRoutes(new RouteBuilder() {

        @Override
        public void configure() throws Exception {

            // Use the file component to read the test data
            from("file:src/test/resources/data?fileName=sfny-test.arff")

            // Remove the class attribute
            .to("weka:filter?apply=Remove -R last")

            // Add the 'prediction' placeholder attribute
            .to("weka:filter?apply=Add -N predicted -T NOM -L 0,1")

            // Rename the relation
            .to("weka:filter?apply=RenameRelation -modify sfny-predicted")

            // Load an already existing model
            .to("weka:model?loadFrom=src/test/resources/data/sfny-j48.model")

            // Use a processor to do the prediction
            .process(new Processor() {
                public void process(Exchange exchange) throws Exception {
                    Dataset dataset = exchange.getMessage().getBody(Dataset.class);
                    dataset.applyToInstances(new NominalPredictor());
                }
            })

            // Write the data file
            .to("weka:write?path=src/test/resources/data/sfny-predicted.arff")
        }
    });
    camelctx.start();
}
```

## Resources

-   [Practical Machine Learning Tools and Techniques](https://www.cs.waikato.ac.nz/ml/weka/book.md)
    
-   [Machine Learning Courses](https://www.cs.waikato.ac.nz/ml/weka/courses.md)
    
-   [Weka Documentation](https://waikato.github.io/weka-wiki/documentation/)
    
-   [Nessus-Weka](https://tdiesler.github.io/nessus-weka)
    

## Spring Boot Auto-Configuration

When using weka with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-weka-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.weka.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.weka.enabled** | Whether to enable auto configuration of the weka component. This is enabled by default. |  | Boolean |
| **camel.component.weka.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
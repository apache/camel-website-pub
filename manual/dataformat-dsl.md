# Data Format DSL

The Data Format DSL is a builder API that allows using type safe construction of Camel [Data Formats](data-format.md).

The Data Format DSL is exclusively available as part of the Java DSL.

The DSL can be accessed directly from the `RouteBuilder` thanks to the method `dataFormat()`.

## Using Data Format DSL

In the following example, a `CsvDataFormat` is created using the legacy approach where the data format is instantiated explicitly and configured using setters:

_Java-only: creating a CSV data format using the legacy approach_

```java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() {
        CsvDataFormat dataFormat = new CsvDataFormat(); (1)
        dataFormat.setDelimiter("|"); (2)
        from("direct:format")
            .setBody(constant(Map.of("foo", "abc", "bar", 123)))
            .marshal(dataFormat); (3)
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Instantiate the expected data format</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Configure the data format according to the needs</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>Affect the data format with the expected configuration</td></tr></tbody></table>

The previous code could be simplified using the utility methods available directly from the `DataFormatClause` corresponding to the type returned by the `marshal()` and `unmarshal()` methods:

_Java-only: simplified marshalling using DataFormatClause utility method_

```java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:format")
            .setBody(constant(Map.of("foo", "abc", "bar", 123)))
            .marshal()
            .csv(); (1)
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Select the <code>csv</code> data format with the default delimiter</td></tr></tbody></table>

This approach is suitable for very basic configuration, but as there are only limited utility methods for each supported data format, for more complex configuration, we can quickly face situations where the utility method for our expected configuration doesn’t exist. In this situation, you can either use the legacy approach or the data format DSL like in the next code snippet:

_Java-only: configuring CSV marshalling using the Data Format DSL builder_

```java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:format")
            .setBody(constant(Map.of("foo", "abc", "bar", 123)))
            .marshal(
                dataFormat() (1)
                    .csv() (2)
                        .delimiter(",") (3)
                    .end() (4)
            );
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Give access to all the supported data formats</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Select the <code>csv</code> data format</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>Configure the data format according to the needs</td></tr><tr><td><i class="conum" data-value="4"></i><b>4</b></td><td>Build the data format with the expected configuration</td></tr></tbody></table>
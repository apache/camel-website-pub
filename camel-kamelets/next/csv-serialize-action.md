# ![csv serialize action](_images/kamelets/csv-serialize-action.svg) CSV Serialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Turns a List of rows, each a Map from the column name to the value or a List of the values, into CSV text with a header line of the column names.

Use it to write records as a CSV file with a sink such as `ftp-sink`, `sftp-sink` or `aws-s3-sink`, for example the rows that `csv-deserialize-action` gives, or the JSON that `json-deserialize-action` parses. To read CSV text, use `csv-deserialize-action`.

Input: a List of rows, where a row is a Map from the column name to the value, or a List of the values; a single Map, which is one row; or parsed JSON (a Jackson `JsonNode`, as `json-deserialize-action` gives): an array of objects or of arrays, or one object.

Output: the body is the CSV text, as text, with one line for each row. Each line ends with a carriage return and a line feed. A value that holds the delimiter, a quote or a line break is put in quotes, with each quote in it doubled. When `header` is true (the default), the first line names the columns: the names in `columns`, or, when it is not set, the keys of the first row if that row is a Map. Rows that are Lists get no header line unless `columns` is set. The `Content-Type` header is set to `text/csv`.

Good to know: with `columns`, each Map row gives the values of these keys in this order: other keys are left out, and a missing key gives an empty value. A List row is written as it is. Without `columns`, the keys of the first row, when it is a Map, are the columns of all the rows in the same way: a key that only a later row has is left out, and a key that a later row does not have gives an empty value. A null value is an empty value. A value that is a Map or a List, such as a nested JSON object, is written as text such as `\{a=1}` or `[1, 2]`, not as JSON. An empty List gives empty text, or only the header line when `columns` is set. A body of text fails the message. The delimiter and the quote are one character each. For tab-separated values, set `delimiter` to a tab in the application properties, such as `camel.kamelet.csv-serialize-action.delimiter=\t`: a tab cannot be given as a parameter of the Kamelet in a route.

## Configuration Options

The following table summarizes the configuration options available for the `csv-serialize-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **columns** | Column Names | The columns to write, by name, separated by commas, such as `id,name,city`. Spaces around a name are left out, so `id, name` is the same as `id,name`. Each Map row gives the values of these keys, in this order. A name cannot hold a comma. | string |  | id,name,city |
| **delimiter** | Delimiter | The character that separates the values of a line, such as `,` or `;`. One character. | string | , | ; |
| **header** | Header Line | Whether to write a first line with the column names: the names in `columns`, or the keys of the first row when `columns` is not set and the rows are Maps. | boolean | true |  |
| **quote** | Quote Character | The character that encloses a value that holds the delimiter, a quote or a line break. One character. | string | " |  |

## Dependencies

At runtime, the `csv-serialize-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:csv
    
-   camel:jackson3
    

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
            uri: "kamelet:csv-serialize-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/csv-serialize-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/csv-serialize-action.kamelet.yaml)
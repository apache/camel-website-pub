# ![csv deserialize action](_images/kamelets/csv-deserialize-action.svg) CSV Deserialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Turns CSV text, such as a file of comma-separated values, into a List of rows: each row is a Map from the column name to the value, or a List of the values.

Use it to work on the records of a CSV file that a source such as `ftp-source`, `sftp-source` or `aws-s3-source` reads, for example to filter them or to send them on as JSON with `json-serialize-action`. To write rows as CSV text, use `csv-serialize-action`.

Input: CSV text, as text, bytes or a stream; bytes and a stream are read as UTF-8. The values of a line are separated by `delimiter`. A value that holds the delimiter, a quote or a line break is put in quotes, with each quote in it doubled, as in `"Oslo, Norway"` or `"Bob ""B"""`. Lines end with a line feed, or a carriage return and a line feed.

Output: the body is a List with one row for each line. With `header` true (the default) or `columns` set, each row is a Map from the column name to the value, in the order of the columns, and the header line is not a row. Otherwise each row is a List of the values. All values are text. The `Content-Type` header is removed.

Good to know: a line with fewer values than columns gives a Map without the missing columns. Empty lines are skipped, unless `skipEmptyLines` is false: an empty line is then a row with one empty value. Empty text, or only a header line, gives an empty List. A message without a body, or with a quoted value that is not closed, fails. The whole text is read into memory. The delimiter and the quote are one character each. For tab-separated values, set `delimiter` to a tab in the application properties, such as `camel.kamelet.csv-deserialize-action.delimiter=\t`: a tab cannot be given as a parameter of the Kamelet in a route.

## Configuration Options

The following table summarizes the configuration options available for the `csv-deserialize-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **columns** | Column Names | The column names, separated by commas without spaces, such as `id,name,city`. Each row is then a Map keyed by these names. When `header` is true, the header line of the file is skipped and these names are used instead; when `header` is false, every line is a row. A name cannot hold a comma or a single quote ('). | string |  | id,name,city |
| **delimiter** | Delimiter | The character that separates the values of a line, such as `,` or `;`. One character. | string | , | ; |
| **header** | Header Line | Whether the first line holds the column names. Each row is then a Map keyed by these names, or by `columns` when it is set. Set it to false for a file without a header line: each row is then a List of the values, unless `columns` is set. | boolean | true |  |
| **quote** | Quote Character | The character that encloses a value that holds the delimiter, a quote or a line break. One character. | string | " |  |
| **skipEmptyLines** | Skip Empty Lines | Whether to skip empty lines. When false, an empty line is a row with one empty value. | boolean | true |  |
| **trim** | Trim Values | Whether to remove the spaces before and after each value and each column name. | boolean | false |  |

## Dependencies

At runtime, the `csv-deserialize-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:csv
    

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
            uri: "kamelet:csv-deserialize-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/csv-deserialize-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/csv-deserialize-action.kamelet.yaml)
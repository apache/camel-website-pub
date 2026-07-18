# File

**Since Camel 1.1**

The File Expression Language is an extension to the [Simple](simple-language.md) language, adding file related capabilities. These capabilities are related to common use cases working with file path and names. The goal is to allow expressions to be used with the [File](../../4.18.x/file-component.md) and [FTP](../../4.18.x/ftp-component.md) components for setting dynamic file patterns for both consumer and producer.

> **Note**
> The file language is merged with [Simple](simple-language.md) language, which means you can use all the file syntax directly within the simple language.

## File Language options

The File language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **trimResult** (common) | `false` | `Boolean` | Whether to trim the returned values when this language is in use. |
| **pretty** (common) | `false` | `Boolean` | To pretty format the output (only JSon or XML supported). |
| **nested** (advanced) | `false` | `Boolean` | If the result is a nested simple expression should this expression be evaluated as well. |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |

## Syntax

This language is an **extension** to the [Simple](simple-language.md) language, so the [Simple](simple-language.md) syntax applies also. So the table below only lists the additional file related functions.

All the file tokens use the same expression name as the method on the `java.io.File` object, for instance `file:absolute` refers to the `java.io.File.getAbsolute()` method. Notice that not all expressions are supported by the current Exchange. For instance, the [FTP](../../4.18.x/ftp-component.md) component supports some options, whereas the File component supports all of them.

      
| Expression | Type | File Consumer | File Producer | FTP Consumer | FTP Producer | Description |
| --- | --- | --- | --- | --- | --- | --- |
| file:name | String | yes | no | yes | no | refers to the file name (is relative to the starting directory, see note below) |
| file:name.ext | String | yes | no | yes | no | refers to the file extension only |
| file:name.ext.single | String | yes | no | yes | no | refers to the file extension. If the file extension has multiple dots, then this expression strips and only returns the last part. |
| file:name.noext | String | yes | no | yes | no | refers to the file name with no extension (is relative to the starting directory, see note below) |
| file:name.noext.single | String | yes | no | yes | no | refers to the file name with no extension (is relative to the starting directory, see note below). If the file name has multiple dots, then this expression strips only the last part, and keeps the others. |
| file:onlyname | String | yes | no | yes | no | refers to the file name only with no leading paths. |
| file:onlyname.noext | String | yes | no | yes | no | refers to the file name only with no extension and with no leading paths. |
| file:onlyname.noext.single | String | yes | no | yes | no | refers to the file name only with no extension and with no leading paths. If the file extension has multiple dots, then this expression strips only the last part, and keeps the others. |
| file:ext | String | yes | no | yes | no | refers to the file extension only |
| file:parent | String | yes | no | yes | no | refers to the file parent |
| file:path | String | yes | no | yes | no | refers to the file path |
| file:absolute | Boolean | yes | no | no | no | refers to whether the file is regarded as absolute or relative |
| file:absolute.path | String | yes | no | no | no | refers to the absolute file path |
| file:length | Long | yes | no | yes | no | refers to the file length returned as a Long type |
| file:size | Long | yes | no | yes | no | refers to the file length returned as a Long type |
| file:modified | Date | yes | no | yes | no | Refers to the file last modified returned as a Date type |
| date:\_command:pattern\_ | String | yes | yes | yes | yes | for date formatting using the `java.text.SimpleDateFormat` patterns. Is an **extension** to the [Simple](simple-language.md) language. Additional command is: **file** (consumers only) for the last modified timestamp of the file. Notice: all the commands from the [Simple](simple-language.md) language can also be used. |

## File token example

### Relative paths

We have a `java.io.File` handle for the file `hello.txt` in the following **relative** directory: `./filelanguage/test`. And we configure our endpoint to use this starting directory `./filelanguage`. The file tokens will return as:

 
| Expression | Returns |
| --- | --- |
| file:name | test/hello.txt |
| file:name.ext | txt |
| file:name.noext | test/hello |
| file:onlyname | hello.txt |
| file:onlyname.noext | hello |
| file:ext | txt |
| file:parent | filelanguage/test |
| file:path | filelanguage/test/hello.txt |
| file:absolute | false |
| file:absolute.path | /workspace/camel/camel-core/target/filelanguage/test/hello.txt |

### Absolute paths

We have a `java.io.File` handle for the file `hello.txt` in the following **absolute** directory: `/workspace/camel/camel-core/target/filelanguage/test`. And we configure the out endpoint to use the absolute starting directory `/workspace/camel/camel-core/target/filelanguage`. The file tokens will return as:

 
| Expression | Returns |
| --- | --- |
| file:name | test/hello.txt |
| file:name.ext | txt |
| file:name.noext | test/hello |
| file:onlyname | hello.txt |
| file:onlyname.noext | hello |
| file:ext | txt |
| file:parent | /workspace/camel/camel-core/target/filelanguage/test |
| file:path | /workspace/camel/camel-core/target/filelanguage/test/hello.txt |
| file:absolute | true |
| file:absolute.path | /workspace/camel/camel-core/target/filelanguage/test/hello.txt |

## Examples

You can enter a fixed file name such as `myfile.txt`:

```properties
fileName="myfile.txt"
```

Let’s assume we use the file consumer to read files and want to move the read files to back up folder with the current date as a subfolder. This can be done using an expression like:

```properties
fileName="backup/${date:now:yyyyMMdd}/${file:name.noext}.bak"
```

relative folder names are also supported so suppose the backup folder should be a sibling folder then you can append `..` as shown:

```properties
fileName="../backup/${date:now:yyyyMMdd}/${file:name.noext}.bak"
```

As this is an extension to the [Simple](simple-language.md) language, we have access to all the goodies from this language also, so in this use case we want to use the in.header.type as a parameter in the dynamic expression:

```properties
fileName="../backup/${date:now:yyyyMMdd}/type-${in.header.type}/backup-of-${file:name.noext}.bak"
```

If you have a custom date you want to use in the expression, then Camel supports retrieving dates from the message header:

```properties
fileName="orders/order-${in.header.customerId}-${date:in.header.orderDate:yyyyMMdd}.xml"
```

And finally, we can also use a bean expression to invoke a POJO class that generates some String output (or convertible to String) to be used:

```properties
fileName="uniquefile-${bean:myguidgenerator.generateid}.txt"
```

Of course, all this can be combined in one expression where you can use the [File Language](#), [Simple](#) and the [Bean](../../4.18.x/bean-component.md) language in one combined expression. This is pretty powerful for those common file path patterns.

## Dependencies

The File language is part of **camel-core**.
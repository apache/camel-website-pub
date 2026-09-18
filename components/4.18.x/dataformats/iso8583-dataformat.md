# ISO-8583

**Since Camel 4.14**

This iso8583 data format supports reading and writing ISO-8583 messages (using the j8583 parser library).

ISO-8583 is a message format used for credit card transactions, banking and other commercial interaction between different systems. It has an ASCII variant and a binary one, and it is somewhat convoluted and difficult to implement.

## ISO-8583 Options

The ISO-8583 dataformat supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **configFile** (common) | `j8583-config.xml` | `String` | The j8583 configuration file to load from classpath. |
| **isoType** (common) |  | `String` | The default ISO-Type to use. |
| **allowAutoWiredMessageFormat** (advanced) | `true` | `Boolean` | Whether to auto-discover com.solab.iso8583.MessageFactory from the registry. |

## ISO-Types

These are some of the most common message types.

There is some logic to this, if you look at the message types as 2-byte hex values: The first byte states the type of operation: 02 are payments, 04 reversals, 08 tests; the second byte indicates if it’s a request or a response. And sometimes repeated requests should end in 1 instead of 0, for example reversals are 0400 the first time but 0401 the next time you send them.

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top"><strong>ISO-Type</strong></td><td class="tableblock halign-left valign-top"><strong>Description</strong></td></tr><tr><td class="tableblock halign-left valign-top">0200</td><td class="tableblock halign-left valign-top">A payment or sale request</td></tr><tr><td class="tableblock halign-left valign-top">0210</td><td class="tableblock halign-left valign-top">A payment or sale response</td></tr><tr><td class="tableblock halign-left valign-top">0400</td><td class="tableblock halign-left valign-top">A reversal request (to undo a previous 0200 operation)</td></tr><tr><td class="tableblock halign-left valign-top">0410</td><td class="tableblock halign-left valign-top">A reversal response</td></tr><tr><td class="tableblock halign-left valign-top">0600</td><td class="tableblock halign-left valign-top">A query (to check the status of a previous operation, or check an account’s balance, etc)</td></tr><tr><td class="tableblock halign-left valign-top">0610</td><td class="tableblock halign-left valign-top">A query response</td></tr><tr><td class="tableblock halign-left valign-top">0800</td><td class="tableblock halign-left valign-top">An echo request (just to keep the connection alive and make sure the other side is responsive)</td></tr><tr><td class="tableblock halign-left valign-top">0810</td><td class="tableblock halign-left valign-top">An echo response</td></tr></tbody></table>

See more information at the [j8583 docs](https://j8583.sourceforge.net/iso8583.md).

## Configuration

The J8583 parser can be configured using `j8583-config.xml` configuration file that should be located in `src/main/resources` so it can be loaded from the classpath.

This configuration file should contain the support ISO-8583 mappings.

## Specifying ISO-Type per message

The data format requires to know the ISO-Type of the message to understand how to parse the data. A default ISO-Type can be configured on the data format. However, you can use a custom header with id `CamelIso8583IsoType` on the Exchange message to override and specify another ISO-Type, such as:

```java
from("direct:payment")
  .setHeader("CamelIso8583IsoType", constant("0200"))
  .unmarshal().iso8583()
  .to("bean:payment");
```

## Example

You can use this data format to unmarshal a ISO-8853 message such as a 0210 payment response, and then select the information from the message you need and covert this to JSon as shown below:

```java
from("jms:payment:response")
        .unmarshal().iso8583("0210")
        .transform().simple(
            """
                  {
                    "op": "${body.getAt(3).value}",
                    "amount": ${body.getAt(4).value.toPlainString},
                    "ref": "${body.getAt(37).value}",
                    "response": "${body.getAt(39).value}",
                    "terminal": "${body.getAt(41).value}",
                    "currency": "${body.getAt(49).value}"
                  }
            """)
        .to("direct:payementResponse");
```

Instead of simple language you can also use Groovy which has a special support in J8583 library:

```java
from("jms:payment:response")
        .unmarshal().iso8583("0210")
        .transform().groovy(
            """
              [
                "op": body[3].value,
                "amount": body[4].value,
                "ref": body[37].value,
                "response": body[39].value,
                "terminal": body[41].value,
                "currency": body[49].value
              ]
            """)
        .to("direct:payementResponse");
```

## More Information

Find more information see the [J8583 project](http://j8583.sourceforge.net/) and the [J8583 source code](https://bitbucket.org/chochos/j8583/src/master/).

## Dependencies

To use ISO-8583 in your camel routes, you need to add the dependency on **camel-iso8583** which implements this data format.

If you use maven, you could add the following to your `pom.xml`, substituting the version number for the latest and greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-iso8583</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using iso8583 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-iso8583-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.iso8583.allow-auto-wired-message-format** | Whether to auto-discover com.solab.iso8583.MessageFactory from the registry. | true | Boolean |
| **camel.dataformat.iso8583.config-file** | The j8583 configuration file to load from classpath. | j8583-config.xml | String |
| **camel.dataformat.iso8583.enabled** | Whether to enable auto configuration of the iso8583 data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.iso8583.iso-type** | The default ISO-Type to use. |  | String |
# HL7 Terser

**Since Camel 2.11**

[HAPI](https://hapifhir.github.io/hapi-hl7v2/) provides a [Terser](https://hapifhir.github.io/hapi-hl7v2/base/apidocs/ca/uhn/hl7v2/util/Terser.md) class that provides access to fields using a commonly used terse location specification syntax. The HL7 Terser language allows using this syntax to extract values from HL7 messages and to use them as expressions and predicates for filtering, content-based routing, etc.

## HL7 Terser Language options

The HL7 Terser language supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **source** (common) |  | `String` | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

## Examples

In the example below, we want to set a header with the patent id from field QRD-8 in the QRY\_A19 message:

```java
import static org.apache.camel.component.hl7.HL7.hl7terser;

// extract patient ID from field QRD-8 in the QRY_A19 message above and put into message header
from("direct:test1")
   .setHeader("PATIENT_ID", hl7terser("QRD-8(0)-1"))
   .to("mock:test1");

// continue processing if extracted field equals a message header
from("direct:test2")
   .filter(hl7terser("QRD-8(0)-1").isEqualTo(header("PATIENT_ID"))
   .to("mock:test2");
```

### HL7 Validation

Often it is preferable to first parse a HL7v2 message and in a separate step validate it against a HAPI [ValidationContext](https://hapifhir.github.io/hapi-hl7v2/base/apidocs/ca/uhn/hl7v2/validation/ValidationContext.md).

The example below shows how to do that. Notice how we use the static method `messageConformsTo` which validates that the message is a HL7v2 message.

```java
import static org.apache.camel.component.hl7.HL7.messageConformsTo;
import ca.uhn.hl7v2.validation.impl.DefaultValidation;

// Use standard or define your own validation rules
ValidationContext defaultContext = new DefaultValidation();

// Throws PredicateValidationException if a message does not validate
from("direct:test1")
   .validate(messageConformsTo(defaultContext))
   .to("mock:test1");
```

### HL7 Validation using the HapiContext

The HAPI Context is always configured with a [ValidationContext](https://hapifhir.github.io/hapi-hl7v2/base/apidocs/ca/uhn/hl7v2/validation/ValidationContext.md) (or a [ValidationRuleBuilder](https://hapifhir.github.io/hapi-hl7v2/base/apidocs/ca/uhn/hl7v2/validation/builder/ValidationRuleBuilder.md)), so you can access the validation rules indirectly.

Furthermore, when unmarshalling the HL7 data format forwards the configured HAPI context in the `CamelHL7Context` header, and the validation rules of this context can be reused:

```java
import static org.apache.camel.component.hl7.HL7.messageConformsTo;
import static org.apache.camel.component.hl7.HL7.messageConforms;

HapiContext hapiContext = new DefaultHapiContext();
hapiContext.getParserConfiguration().setValidating(false); // don't validate during parsing

// customize HapiContext some more ... e.g., enforce that PID-8 in ADT_A01 messages of version 2.4 is not empty
ValidationRuleBuilder builder = new ValidationRuleBuilder() {
   @Override
   protected void configure() {
      forVersion(Version.V24)
         .message("ADT", "A01")
         .terser("PID-8", not(empty()));
   }
};
hapiContext.setValidationRuleBuilder(builder);

HL7DataFormat hl7 = new HL7DataFormat();
hl7.setHapiContext(hapiContext);

from("direct:test1")
  .unmarshal(hl7)                // uses the GenericParser returned from the HapiContext
  .validate(messageConforms())   // uses the validation rules returned from the HapiContext
                                 // equivalent with .validate(messageConformsTo(hapiContext))
   // route continues from here
```

### HL7 Acknowledgement expression

A common task in HL7v2 processing is to generate an acknowledgement message as a response to an incoming HL7v2 message, e.g., based on a validation result. The `ack` expression lets us accomplish this very elegantly:

```java
import static org.apache.camel.component.hl7.HL7.messageConformsTo;
import static org.apache.camel.component.hl7.HL7.ack;
import ca.uhn.hl7v2.validation.impl.DefaultValidation;

// Use standard or define your own validation rules
ValidationContext defaultContext = new DefaultValidation();

from("direct:test1")
   .onException(Exception.class)
      .handled(true)
      .transform(ack()) // auto-generates negative ack because of exception in Exchange
      .end()
   .validate(messageConformsTo(defaultContext))
   // do something meaningful here

   // acknowledgement
  .transform(ack())
```

### Custom Acknowledgement for MLLP

In special situations, you may want to set a custom acknowledgement without using Exceptions. This can be achieved using the `ack` expression:

```java
import org.apache.camel.component.mllp.MllpConstants;
import ca.uhn.hl7v2.AcknowledgmentCode;
import ca.uhn.hl7v2.ErrorCode;

// In process block
exchange.setProperty(MllpConstants.MLLP_ACKNOWLEDGEMENT,
  ack(AcknowledgmentCode.AR, "Server didn't accept this message", ErrorCode.UNKNOWN_KEY_IDENTIFIER).evaluate(exchange, Object.class)
```

## Spring Boot Auto-Configuration

When using hl7terser with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-hl7-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.hl7.enabled** | Whether to enable auto configuration of the hl7 data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.hl7.parser** | To use a custom HL7 parser. The option is a ca.uhn.hl7v2.parser.Parser type. |  | String |
| **camel.dataformat.hl7.validate** | Whether to validate the HL7 message Is by default true. | true | Boolean |
| **camel.language.hl7terser.enabled** | Whether to enable auto configuration of the hl7terser language. This is enabled by default. |  | Boolean |
| **camel.language.hl7terser.source** | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| **camel.language.hl7terser.trim** | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. | true | Boolean |
# Camel languages supported on Quarkus

There are 25 languages (4 deprecated, 3 JVM only)

     
| Language | Artifact | JVM  
since | Native  
since | Support  
level | Description |
| --- | --- | --- | --- | --- | --- |
| [Bean Method](extensions/bean.md) | camel-quarkus-bean | 0.1.0 | 0.1.0 | Stable | Calls a Java bean method. |
| [Constant](extensions/core.md) | camel-quarkus-core | 0.0.1 | 0.0.1 | Stable | A fixed value set only once during the route startup. |
| [CSimple](extensions/csimple.md) | camel-quarkus-csimple | 1.5.0 | 1.5.0 | Stable | Evaluate a compiled simple expression. |
| [DataSonnet](extensions/datasonnet.md) | camel-quarkus-datasonnet | 2.10.0 | 2.10.0 | Stable | To use DataSonnet scripts for message transformations. |
| [ExchangeProperty](extensions/core.md) | camel-quarkus-core | 0.0.1 | 0.0.1 | Stable | Gets a property from the Exchange. |
| [File](extensions/core.md) | camel-quarkus-core | 0.0.1 | 0.0.1 | Stable | File related capabilities for the Simple language |
| [Groovy](extensions/groovy.md) | camel-quarkus-groovy | 1.0.0 | 3.2.0 | Stable | Evaluates a Groovy script. |
| [Header](extensions/core.md) | camel-quarkus-core | 0.0.1 | 0.0.1 | Stable | Gets a header from the Exchange. |
| [HL7 Terser](extensions/hl7.md) | camel-quarkus-hl7 | 1.1.0 | 1.8.0 | Stable | Get the value of a HL7 message field specified by terse location specification syntax. |
| [Java](extensions/joor.md) | camel-quarkus-joor | 2.0.0 | 3.2.0 | Stable | Evaluates a Java (Java compiled once at runtime) expression. |
| [jOOR](extensions/joor.md) | camel-quarkus-joor | 2.0.0 | 3.2.0 | Stable | Evaluates a jOOR (Java compiled once at runtime) expression. |
| [JQ](extensions/jq.md) | camel-quarkus-jq | 2.11.0 | 2.11.0 | Stable | Evaluates a JQ expression against a JSON message body. |
| [JavaScript](extensions/javascript.md) | camel-quarkus-javascript | 3.14.0 | n/a | Preview | Evaluates a JavaScript expression. |
| [JSONPath](extensions/jsonpath.md) | camel-quarkus-jsonpath | 1.0.0 | 1.0.0 | Stable | Evaluates a JSONPath expression against a JSON message body. |
| [MVEL](extensions/mvel.md) | camel-quarkus-mvel | 1.1.0 | n/a | Preview | Evaluates a MVEL template. |
| [OGNL](extensions/ognl.md) | camel-quarkus-ognl | 1.0.0 | 3.2.0 | Stable | Evaluates an OGNL expression (Apache Commons OGNL). |
| [Python](extensions/python.md) | camel-quarkus-python | 3.24.0 | n/a | Preview | Evaluates a Python expression. |
| [Ref](extensions/core.md) | camel-quarkus-core | 0.0.1 | 0.0.1 | Stable | Uses an existing expression from the registry. |
| [Simple](extensions/core.md) | camel-quarkus-core | 0.0.1 | 0.0.1 | Stable | Evaluates a Camel simple expression. |
| [Tokenize](extensions/core.md) | camel-quarkus-core | 0.0.1 | 0.0.1 | Stable | Tokenize text payloads using delimiter patterns. |
| [Variable](extensions/core.md) | camel-quarkus-core | 0.0.1 | 0.0.1 | Stable | Gets a variable |
| [Wasm](extensions/wasm.md) | camel-quarkus-wasm | 3.10.0 | 3.10.0 | Stable | Call a wasm (web assembly) function. |
| [XPath](extensions/xpath.md) | camel-quarkus-xpath | 1.0.0 | 1.0.0 | Stable | Evaluates an XPath expression against an XML payload. |
| [XQuery](extensions/saxon.md) | camel-quarkus-saxon | 1.1.0 | 2.0.0 | Stable | Evaluates an XQuery expressions against an XML payload. |
| [XML Tokenize](extensions/stax.md) | camel-quarkus-stax | 1.1.0 | 1.7.0 | Stable | Tokenize XML payloads. |
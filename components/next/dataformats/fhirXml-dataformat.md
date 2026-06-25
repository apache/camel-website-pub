# FHIR XML

**Since Camel 2.21**

The FHIR-XML Data Format leverages [HAPI-FHIR’s](https://github.com/jamesagnew/hapi-fhir/blob/master/hapi-fhir-base/src/main/java/ca/uhn/fhir/parser/XmlParser.java) XML parser to parse to/from XML format to/from a HAPI-FHIR’s `IBaseResource`.

## FHIR XML Format Options

The FHIR XML dataformat supports 18 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **fhirVersion** (common) | `R4` | `Enum` | 
The version of FHIR to use. Possible values are: DSTU2, DSTU2\_HL7ORG, DSTU2\_1, DSTU3, R4, R5.

Enum values:

-   DSTU2
    
-   DSTU2\_HL7ORG
    
-   DSTU2\_1
    
-   DSTU3
    
-   R4
    
-   R5
    





 |
| **fhirContext** (advanced) |  | `String` | To use a custom fhir context. Reference to object of type ca.uhn.fhir.context.FhirContext. |
| **prettyPrint** (common) | `false` | `Boolean` | Sets the pretty print flag, meaning that the parser will encode resources with human-readable spacing and newlines between elements. |
| **parserErrorHandler** (advanced) |  | `String` | Registers an error handler which will be invoked when any parse errors are found. Reference to object of type ca.uhn.fhir.parser.IParserErrorHandler. |
| **parserOptions** (advanced) |  | `String` | Sets the parser options object which will be used to supply default options to newly created parsers. Reference to object of type ca.uhn.fhir.context.ParserOptions. |
| **preferTypes** (advanced) |  | `String` | If set (FQN class names), when parsing resources the parser will try to use the given types when possible. Multiple class names can be separated by comma. |
| **forceResourceId** (advanced) |  | `String` | When encoding, force this resource ID to be encoded as the resource ID. Reference to object of type org.hl7.fhir.instance.model.api.IIdType. |
| **serverBaseUrl** (advanced) |  | `String` | Sets the server’s base URL used by this parser. If a value is set, resource references will be turned into relative references if they are provided as absolute URLs but have a base matching the given base. |
| **omitResourceId** (advanced) | `false` | `Boolean` | If set to true (default is false) the ID of any resources being encoded will not be included in the output. |
| **encodeElementsAppliesToChildResourcesOnly** (advanced) | `false` | `Boolean` | If set to true (default is false), the values supplied to setEncodeElements will not be applied to the root resource (typically a Bundle), but will be applied to any sub-resources contained within it. |
| **encodeElements** (advanced) |  | `String` | If provided, specifies the elements which should be encoded, to the exclusion of all others. Multiple elements can be separated by comma. |
| **dontEncodeElements** (advanced) |  | `String` | If provided, specifies the elements which should NOT be encoded. Multiple elements can be separated by comma. |
| **stripVersionsFromReferences** (advanced) | `false` | `Boolean` | If set to true (which is the default), resource references containing a version will have the version removed when the resource is encoded. |
| **overrideResourceIdWithBundleEntryFullUrl** (advanced) | `false` | `Boolean` | If set to true (which is the default), the Bundle.entry.fullUrl will override the Bundle.entry.resource’s resource id if the fullUrl is defined. |
| **summaryMode** (advanced) | `false` | `Boolean` | If set to true (default is false) only elements marked by the FHIR specification as being summary elements will be included. |
| **suppressNarratives** (advanced) | `false` | `Boolean` | If set to true (default is false), narratives will not be included in the encoded values. |
| **dontStripVersionsFromReferencesAtPaths** (advanced) |  | `String` | If supplied value(s), any resource references at the specified paths will have their resource versions encoded instead of being automatically stripped during the encoding process. Multiple elements can be separated by comma. |
| **contentTypeHeader** (common) | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |
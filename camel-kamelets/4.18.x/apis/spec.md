# Camel Kamelets API

## camel.apache.org/v1

Package v1 contains API Schema definitions for the camel v1 API group

## Resource Types

### Kamelet

Kamelet is the Schema for the kamelets API.

 
| Field | Description |
| --- | --- |
| `apiVersion`  
string | `camel.apache.org/v1` |
| `kind`  
string | `Kamelet` |
| `metadata`  
**[https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.dex](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.dex) .PackageSegments -2}}\[Kubernetes meta/v1.ObjectMeta\]** | Refer to the Kubernetes API documentation for the fields of the `metadata` field. |
| `spec`  
**[KameletSpec](#_camel_apache_org_v1_KameletSpec)** | the desired specification |
| `status`  
**[KameletStatus](#_camel_apache_org_v1_KameletStatus)** | the actual status of the resource Deprecated no longer in use |

## Internal Types

### DataSpec

**Appears on:**

-   [SourceSpec](#_camel_apache_org_v1_SourceSpec)
    

DataSpec represents the way the source is materialized in the running `Pod`.

 
| Field | Description |
| --- | --- |
| `name`  
string | the name of the specification |
| `path`  
string | the path where the file is stored |
| `content`  
string | the source code (plain text) |
| `rawContent`  
\[\]byte | the source code (binary) |
| `contentRef`  
string | the confimap reference holding the source content |
| `contentKey`  
string | the confimap key holding the source content |
| `contentType`  
string | the content type (typically text or binary) |
| `compression`  
bool | if the content is compressed (base64 encrypted) |

### DataTypeReference

DataTypeReference references to the specification of a data type by its scheme and format name.

 
| Field | Description |
| --- | --- |
| `scheme`  
string | the data type component scheme |
| `format`  
string | the data type format name |

### DataTypeSpec

**Appears on:**

-   [DataTypesSpec](#_camel_apache_org_v1_DataTypesSpec)
    

DataTypeSpec represents the specification for a data type.

 
| Field | Description |
| --- | --- |
| `scheme`  
string | the data type component scheme |
| `format`  
string | the data type format name |
| `description`  
string | optional description |
| `mediaType`  
string | media type as expected for HTTP media types (ie, application/json) |
| `dependencies`  
\[\]string | the list of Camel or Maven dependencies required by the data type |
| `headers`  
**[map\[string\]github.com/apache/camel-kamelets/crds/pkg/apis/camel/v1.HeaderSpec](#_camel_apache_org_v1_HeaderSpec)** | one to many header specifications |
| `schema`  
**[JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)** | the expected schema for the data type |

### DataTypesSpec

**Appears on:**

-   [KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)
    

DataTypesSpec represents the specification for a set of data types.

 
| Field | Description |
| --- | --- |
| `default`  
string | the default data type for this Kamelet |
| `types`  
**[map\[string\]github.com/apache/camel-kamelets/crds/pkg/apis/camel/v1.DataTypeSpec](#_camel_apache_org_v1_DataTypeSpec)** | one to many data type specifications |
| `headers`  
**[map\[string\]github.com/apache/camel-kamelets/crds/pkg/apis/camel/v1.HeaderSpec](#_camel_apache_org_v1_HeaderSpec)** | one to many header specifications |

### EventTypeSpec

**Appears on:**

-   [KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)
    

EventTypeSpec represents a specification for an event type. Deprecated: In favor of using DataTypeSpec.

 
| Field | Description |
| --- | --- |
| `mediaType`  
string | media type as expected for HTTP media types (ie, application/json) |
| `schema`  
**[JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)** | the expected schema for the event |

### ExternalDocumentation

**Appears on:**

-   [JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)
    

ExternalDocumentation allows referencing an external resource for extended documentation.

 
| Field | Description |
| --- | --- |
| `description`  
string | 
 |
| `url`  
string | 

 |

### HeaderSpec

**Appears on:**

-   [DataTypeSpec](#_camel_apache_org_v1_DataTypeSpec)
    
-   [DataTypesSpec](#_camel_apache_org_v1_DataTypesSpec)
    

HeaderSpec represents the specification for a header used in the Kamelet.

 
| Field | Description |
| --- | --- |
| `type`  
string | 
 |
| `title`  
string | 

 |
| `description`  
string | 

 |
| `required`  
bool | 

 |
| `default`  
string | 

 |

### JSON

**Appears on:**

-   [JSONSchemaProp](#_camel_apache_org_v1_JSONSchemaProp)
    
-   [JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)
    

JSON represents any valid JSON value. These types are supported: bool, int64, float64, string, \[\]interface{}, map\[string\]interface{} and nil.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.) |

### JSONSchemaProp

**Appears on:**

-   [JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)
    

 
| Field | Description |
| --- | --- |
| `id`  
string | 
 |
| `deprecated`  
bool | 

 |
| `description`  
string | 

 |
| `type`  
string | 

 |
| `format`  
string | 

format is an OpenAPI v3 format string. Unknown formats are ignored. The following formats are validated:

-   bsonobjectid: a bson object ID, i.e. a 24 characters hex string
    
-   uri: an URI as parsed by Golang net/url.ParseRequestURI
    
-   email: an email address as parsed by Golang net/mail.ParseAddress
    
-   hostname: a valid representation for an Internet host name, as defined by RFC 1034, section 3.1 \[RFC1034\].
    
-   ipv4: an IPv4 IP as parsed by Golang net.ParseIP
    
-   ipv6: an IPv6 IP as parsed by Golang net.ParseIP
    
-   cidr: a CIDR as parsed by Golang net.ParseCIDR
    
-   mac: a MAC address as parsed by Golang net.ParseMAC
    
-   uuid: an UUID that allows uppercase defined by the regex (?i)^\[0-9a-f\]{8}-?\[0-9a-f\]{4}-?\[0-9a-f\]{4}-?\[0-9a-f\]{4}-?\[0-9a-f\]{12}$
    
-   uuid3: an UUID3 that allows uppercase defined by the regex (?i)^\[0-9a-f\]{8}-?\[0-9a-f\]{4}-?3\[0-9a-f\]{3}-?\[0-9a-f\]{4}-?\[0-9a-f\]{12}$
    
-   uuid4: an UUID4 that allows uppercase defined by the regex (?i)^\[0-9a-f\]{8}-?\[0-9a-f\]{4}-?4\[0-9a-f\]{3}-?\[89ab\]\[0-9a-f\]{3}-?\[0-9a-f\]{12}$
    
-   uuid5: an UUID5 that allows uppercase defined by the regex (?i)^\[0-9a-f\]{8}-?\[0-9a-f\]{4}-?5\[0-9a-f\]{3}-?\[89ab\]\[0-9a-f\]{3}-?\[0-9a-f\]{12}$
    
-   isbn: an ISBN10 or ISBN13 number string like "0321751043" or "978-0321751041"
    
-   isbn10: an ISBN10 number string like "0321751043"
    
-   isbn13: an ISBN13 number string like "978-0321751041"
    
-   creditcard: a credit card number defined by the regex ^(?:4\[0-9\]{12}(?:\[0-9\]{3})?|5\[1-5\]\[0-9\]{14}|6(?:011|5\[0-9\]\[0-9\])\[0-9\]{12}|3\[47\]\[0-9\]{13}|3(?:0\[0-5\]|\[68\]\[0-9\])\[0-9\]{11}|(?:2131|1800|35\\\\d{3})\\\\d{11})$ with any non digit characters mixed in
    
-   ssn: a U.S. social security number following the regex ^\\\\d{3}\[- \]?\\\\d{2}\[- \]?\\\\d{4}$
    
-   hexcolor: an hexadecimal color code like "#FFFFFF" following the regex ^#?(\[0-9a-fA-F\]{3}|\[0-9a-fA-F\]{6})$
    
-   rgbcolor: an RGB color code like rgb like "rgb(255,255,255)"
    
-   byte: base64 encoded binary data
    
-   password: any kind of string
    
-   date: a date string like "2006-01-02" as defined by full-date in RFC3339
    
-   duration: a duration string like "22 ns" as parsed by Golang time.ParseDuration or compatible with Scala duration format
    
-   datetime: a date time string like "2014-12-15T19:30:20.000Z" as defined by date-time in RFC3339.
    





 |
| `title`  
string | 

 |
| `default`  
**[JSON](#_camel_apache_org_v1_JSON)** | default is a default value for undefined object fields. |
| `maximum`  
encoding/json.Number | 

 |
| `exclusiveMaximum`  
bool | 

 |
| `minimum`  
encoding/json.Number | 

 |
| `exclusiveMinimum`  
bool | 

 |
| `maxLength`  
int64 | 

 |
| `minLength`  
int64 | 

 |
| `pattern`  
string | 

 |
| `maxItems`  
int64 | 

 |
| `minItems`  
int64 | 

 |
| `uniqueItems`  
bool | 

 |
| `maxProperties`  
int64 | 

 |
| `minProperties`  
int64 | 

 |
| `multipleOf`  
encoding/json.Number | 

 |
| `enum`  
**[\[\]JSON](#_camel_apache_org_v1_JSON)** | 

 |
| `example`  
**[JSON](#_camel_apache_org_v1_JSON)** | 

 |
| `nullable`  
bool | 

 |
| `x-descriptors`  
\[\]string | XDescriptors is a list of extended properties that trigger a custom behavior in external systems |

### JSONSchemaProps

**Appears on:**

-   [DataTypeSpec](#_camel_apache_org_v1_DataTypeSpec)
    
-   [EventTypeSpec](#_camel_apache_org_v1_EventTypeSpec)
    
-   [KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)
    

JSONSchemaProps is a JSON-Schema following Specification Draft 4 ([http://json-schema.org/](http://json-schema.org/)).

 
| Field | Description |
| --- | --- |
| `id`  
string | 
 |
| `description`  
string | 

 |
| `title`  
string | 

 |
| `properties`  
**[map\[string\]github.com/apache/camel-kamelets/crds/pkg/apis/camel/v1.JSONSchemaProp](#_camel_apache_org_v1_JSONSchemaProp)** | 

 |
| `required`  
\[\]string | 

 |
| `example`  
**[JSON](#_camel_apache_org_v1_JSON)** | 

 |
| `externalDocs`  
**[ExternalDocumentation](#_camel_apache_org_v1_ExternalDocumentation)** | 

 |
| `$schema`  
**[JSONSchemaURL](#_camel_apache_org_v1_JSONSchemaURL)** | 

 |
| `type`  
string | 

 |

### JSONSchemaURL(`string` alias)

**Appears on:**

-   [JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)
    

JSONSchemaURL represents a schema url.

### KameletCondition

**Appears on:**

-   [KameletStatus](#_camel_apache_org_v1_KameletStatus)
    

KameletCondition describes the state of a resource at a certain point.

 
| Field | Description |
| --- | --- |
| `type`  
**[KameletConditionType](#_camel_apache_org_v1_KameletConditionType)** | Type of kamelet condition. |
| `status`  
**[https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.dex](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.dex) .PackageSegments -2}}\[Kubernetes core/v1.ConditionStatus\]** | Status of the condition, one of True, False, Unknown. |
| `lastUpdateTime`  
**[https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.dex](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.dex) .PackageSegments -2}}\[Kubernetes meta/v1.Time\]** | The last time this condition was updated. |
| `lastTransitionTime`  
**[https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.dex](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.dex) .PackageSegments -2}}\[Kubernetes meta/v1.Time\]** | Last time the condition transitioned from one status to another. |
| `reason`  
string | The reason for the condition’s last transition. |
| `message`  
string | A human-readable message indicating details about the transition. |

### KameletConditionType(`string` alias)

**Appears on:**

-   [KameletCondition](#_camel_apache_org_v1_KameletCondition)
    

KameletConditionType --.

### KameletPhase(`string` alias)

**Appears on:**

-   [KameletStatus](#_camel_apache_org_v1_KameletStatus)
    

KameletPhase --.

### KameletProperty

**Appears on:**

-   [KameletStatus](#_camel_apache_org_v1_KameletStatus)
    

KameletProperty specify the behavior of a property in a Kamelet.

 
| Field | Description |
| --- | --- |
| `name`  
string | the name of the property |
| `default`  
string | the default value of the property (if any) |

### KameletSpec

**Appears on:**

-   [Kamelet](#_camel_apache_org_v1_Kamelet)
    

KameletSpec specifies the configuration required to execute a Kamelet.

 
| Field | Description |
| --- | --- |
| `KameletSpecBase`  
**[KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)** | (Members of `KameletSpecBase` are embedded into this type.) |
| `versions`  
**[map\[string\]github.com/apache/camel-kamelets/crds/pkg/apis/camel/v1.KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)** | the optional versions available for this Kamelet. This field may not be taken in account by Camel core and is meant to support any user defined versioning model on cluster only. If the user wants to use any given version, she must materialize a file with the given version spec as the `main` Kamelet spec on the runtime. |

### KameletSpecBase

**Appears on:**

-   [KameletSpec](#_camel_apache_org_v1_KameletSpec)
    

KameletSpecBase specifies the base configuration of a Kamelet.

 
| Field | Description |
| --- | --- |
| `definition`  
**[JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)** | defines the formal configuration of the Kamelet |
| `sources`  
**[\[\]SourceSpec](#_camel_apache_org_v1_SourceSpec)** | sources in any Camel DSL supported |
| `template`  
**[Template](#_camel_apache_org_v1_Template)** | the main source in YAML DSL |
| `types`  
**[map\[github.com/apache/camel-kamelets/crds/pkg/apis/camel/v1.TypeSlot\]github.com/apache/camel-kamelets/crds/pkg/apis/camel/v1.EventTypeSpec](#_camel_apache_org_v1_EventTypeSpec)** | data specification types for the events consumed/produced by the Kamelet Deprecated: In favor of using DataTypes |
| `dataTypes`  
**[map\[github.com/apache/camel-kamelets/crds/pkg/apis/camel/v1.TypeSlot\]github.com/apache/camel-kamelets/crds/pkg/apis/camel/v1.DataTypesSpec](#_camel_apache_org_v1_DataTypesSpec)** | data specification types for the events consumed/produced by the Kamelet |
| `dependencies`  
\[\]string | Camel dependencies needed by the Kamelet |

### KameletStatus

**Appears on:**

-   [Kamelet](#_camel_apache_org_v1_Kamelet)
    

KameletStatus defines the observed state of Kamelet.

 
| Field | Description |
| --- | --- |
| `observedGeneration`  
int64 | ObservedGeneration is the most recent generation observed for this Kamelet. |
| `phase`  
**[KameletPhase](#_camel_apache_org_v1_KameletPhase)** | Phase —  |
| `conditions`  
**[\[\]KameletCondition](#_camel_apache_org_v1_KameletCondition)** | Conditions —  |
| `properties`  
**[\[\]KameletProperty](#_camel_apache_org_v1_KameletProperty)** | Properties —  |

### Language(`string` alias)

**Appears on:**

-   [SourceSpec](#_camel_apache_org_v1_SourceSpec)
    

Language represents a supported language (Camel DSL).

### RawMessage(`[]byte` alias)

**Appears on:**

-   [JSON](#_camel_apache_org_v1_JSON)
    
-   [Template](#_camel_apache_org_v1_Template)
    

RawMessage is a raw encoded JSON value. It implements Marshaler and Unmarshaler and can be used to delay JSON decoding or precompute a JSON encoding.

### ResourceCondition

ResourceCondition is a common type for all conditions.

### SourceSpec

**Appears on:**

-   [KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)
    

SourceSpec defines the configuration for one or more routes to be executed in a certain Camel DSL language.

 
| Field | Description |
| --- | --- |
| `DataSpec`  
**[DataSpec](#_camel_apache_org_v1_DataSpec)** | (Members of `DataSpec` are embedded into this type.)
contains configuration related to the source code

 |
| `language`  
**[Language](#_camel_apache_org_v1_Language)** | specify which is the language (Camel DSL) used to interpret this source code |
| `loader`  
string | Loader is an optional id of the org.apache.camel.k.RoutesLoader that will interpret this source at runtime |
| `interceptors`  
\[\]string | Interceptors are optional identifiers the org.apache.camel.k.RoutesLoader uses to pre/post process sources |
| `type`  
**[SourceType](#_camel_apache_org_v1_SourceType)** | Type defines the kind of source described by this object |
| `property-names`  
\[\]string | List of property names defined in the source (e.g. if type is "template") |
| `from-kamelet`  
bool | True if the spec is generated from a Kamelet |

### SourceType(`string` alias)

**Appears on:**

-   [SourceSpec](#_camel_apache_org_v1_SourceSpec)
    

SourceType represents an available source type.

### Template

**Appears on:**

-   [KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)
    

Template is an unstructured object representing a Kamelet template in YAML/JSON DSL.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.)
an unstructured raw message

 |

### TypeSlot(`string` alias)

TypeSlot represent a kind of data (ie, input, output, …​).
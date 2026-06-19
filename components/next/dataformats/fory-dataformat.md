# Fory

**Since Camel 4.9**

Fory is a Data Format that uses the [Fory Library](https://fory.apache.org/)

> **Note**
> Apache Fory is not supporting architecture using Big Endian (s390x, for instance).

## Fory Options

The Fory dataformat supports 4 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **unmarshalType** (common) |  | `String` | Class of the java type to use when unmarshalling. |
| **requireClassRegistration** (advanced) | `true` | `Boolean` | Whether to require register classes. |
| **threadSafe** (advanced) | `true` | `Boolean` | Whether to use the threadsafe Fory. |
| **allowAutoWiredFory** (advanced) | `true` | `Boolean` | Whether to auto-discover Fory from the registry. |

## Dependencies

To use Fory in your camel routes, you need to add the dependency on **camel-fory** which implements this data format.

If you use maven, you could add the following to your `pom.xml`, substituting the version number for the latest and greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-fory</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```
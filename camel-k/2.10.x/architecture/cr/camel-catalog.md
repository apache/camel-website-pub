# CamelCatalog

The **CamelCatalog** is a resource that provides metadata related to what is included in the [Runtime](../runtime.md) in term of Camel components, languages, dataformats and capabilities provided.

> **Note**
> each catalog may require to specify a container tool image eventually used by the build process starting from Camel K runtime version 1.17. You cannot run a Camel K runtime < 1.17 with Camel K version 2.

> **Note**
> the full go definition can be found [here](https://github.com/apache/camel-k/blob/main/pkg/apis/camel/v1/camelcatalog_types.go)
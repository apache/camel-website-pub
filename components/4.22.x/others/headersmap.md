# Headersmap

> **Warning**
> **Deprecated:** This headersmap is deprecated and may be removed in a future release.

**Since Camel 2.20**

> **Note**
> This component is deprecated. Since Camel 4.21, the default `CaseInsensitiveMap` in camel-core uses a custom O(1) hash table with zero-allocation lookups, making this component unnecessary. Simply remove the `camel-headersmap` dependency — the core implementation now provides equivalent or better performance without any external library.

The Headersmap component is a faster implementation of a case-insensitive map which can be plugged in and used by Camel at runtime to have slight faster performance in the Camel Message headers.

## Usage

### Auto-detection from classpath

To use this implementation all you need to do is to add the `camel-headersmap` dependency to the classpath, and Camel should auto-detect this on startup and log as follows:

```text
Detected and using HeadersMapFactory: camel-headersmap
```
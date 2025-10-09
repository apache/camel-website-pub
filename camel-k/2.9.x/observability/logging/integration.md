# Camel K Integration Logging

The [Logging trait](../../traits/logging.md) simplifies the logging configuration of the Integration runtime.

> **Note**
> The Logging trait has been introduced in Camel K version 1.5.0. See the [introductory blog post](/blog/2021/05/new-camel-k-logging-features/).

## Logging Level

To configure the log level, the `level` option from the Logging trait can be used, e.g.:

```console
$ kamel run -t logging.level=DEBUG
```

## Logging Format

The format of the log messages can be configured using the `format` option, e.g.:

```console
$ kamel run -t logging.format='%d{HH:mm:ss} %-5p (%t) %s%e%n'
```

The supported values are those of [Quarkus logging](https://quarkus.io/guides/logging) configuration, as it provides the logging framework, for Camel Quarkus which is leveraged by Camel K.

## Structured Logs

The Integration Pods can provide structured logs, to facilitate processing and parsing. This can be turned on or off, using the `json` option from the Logging trait, e.g.:

```console
$ kamel run -t logging.json=true
```

Subsequently, pretty JSON logs can be enabled with:

```console
$ kamel run -t logging.json=true -t logging.json-pretty-print=true
```
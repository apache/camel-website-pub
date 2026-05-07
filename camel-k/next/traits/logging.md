# Logging Trait

Deprecated since2.9.0

> **Warning**
> The Logging trait is **deprecated** as of version 2.9.0 and will be removed in a future release.
>
> Please use Quarkus logging properties directly instead. See the [Migration Guide](#migration-guide) section below for details.

The Logging trait is used to configure Integration runtime logging options (such as color and format). The logging backend is provided by Quarkus, whose configuration is documented at [https://quarkus.io/guides/logging](https://quarkus.io/guides/logging).

> **Warning**
> The Logging trait is **deprecated** and will be removed in future release versions: use Quarkus logging properties directly instead.

Migration example:

Before: traits.logging.level=DEBUG
After:  -p quarkus.log.level=DEBUG

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait logging.[key]=[value] --trait logging.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `logging.enabled` | `bool` | Can be used to enable or disable a trait. All traits share this common property. |
| `logging.color` | `bool` | Colorize the log output |
| `logging.format` | `string` | Logs message format |
| `logging.level` | `string` | Adjust the logging level (defaults to `INFO`) |
| `logging.json` | `bool` | Output the logs in JSON |
| `logging.jsonPrettyPrint` | `bool` | Enable "pretty printing" of the JSON logs |
> **Note**
> the variables names are "snake case" if you’re using in `kamel` CLI, for example `trait.myParam` has to be translated as `-t trait.my-param`

## Migration Guide

The Logging trait is deprecated. You should migrate to using Quarkus properties directly, which provides the same functionality with more flexibility.

### Property Mapping

The following table shows how to map Logging trait properties to Quarkus properties:

  
| Logging Trait | Quarkus Property | Example |
| --- | --- | --- |
| `logging.level=DEBUG` | `quarkus.log.level=DEBUG` | `kamel run -p quarkus.log.level=DEBUG MyRoute.java` |
| `logging.color=true` | `quarkus.console.color=true` | `kamel run -p quarkus.console.color=true MyRoute.java` |
| `logging.format=…​` | `quarkus.log.console.format=…​` | `kamel run -p quarkus.log.console.format="%d{HH:mm:ss} %-5p %s%e%n" MyRoute.java` |
| `logging.json=true` | `quarkus.log.console.json=true` | `kamel run -p quarkus.log.console.json=true MyRoute.java` |
| `logging.json-pretty-print=true` | `quarkus.log.console.json.pretty-print=true` | `kamel run -p quarkus.log.console.json.pretty-print=true MyRoute.java` |

### Migration Examples

**Before (deprecated):**

```yaml
apiVersion: camel.apache.org/v1
kind: Integration
metadata:
  name: my-integration
spec:
  traits:
    logging:
      level: DEBUG
      json: true
      jsonPrettyPrint: true
```

**After (recommended):**

```yaml
apiVersion: camel.apache.org/v1
kind: Integration
metadata:
  name: my-integration
spec:
  configuration:
    - type: property
      value: quarkus.log.level=DEBUG
    - type: property
      value: quarkus.log.console.json=true
    - type: property
      value: quarkus.log.console.json.pretty-print=true
```

Or using the CLI:

```console
$ kamel run MyRoute.java \
  -p quarkus.log.level=DEBUG \
  -p quarkus.log.console.json=true \
  -p quarkus.log.console.json.pretty-print=true
```

### Benefits of Direct Properties

Using Quarkus properties directly provides more flexibility, including:

-   Category-specific log levels: `quarkus.log.category."org.apache.camel".level=DEBUG`
    
-   More logging options available at [https://quarkus.io/guides/logging](https://quarkus.io/guides/logging)
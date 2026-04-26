# camel validate normalize

**Available as of Camel 4.20**

Normalize YAML routes to canonical (explicit) form.

This command parses YAML routes and rewrites them in canonical form, expanding all shorthands and implicit expressions. For example, `log: "${body}"` becomes `log: { message: "${body}" }` and `setBody: { simple: "Hello" }` becomes `setBody: { expression: { simple: { expression: "Hello" } } }`.

The normalized output is valid against both the classic and canonical schemas.

See the [YAML DSL Schema Variants](../../components/4.18.x/others/yaml-dsl.md) documentation for details on the differences between the classic and canonical schemas.

## Usage

```bash
camel validate normalize [options] <files>
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--output` | File or directory to write normalized output. If not specified, output is printed to console. |  | String |
| `-h,--help` | Display the help and sub-commands |  | boolean |

## Examples

Normalize a YAML route and print to console:

```bash
camel validate normalize myroute.yaml
```

Normalize and write to a file:

```bash
camel validate normalize --output normalized.yaml myroute.yaml
```

Normalize multiple files into a directory:

```bash
camel validate normalize --output normalized/ routes/*.yaml
```

### Before and after

Given the following YAML route using classic shorthands:

```yaml
- route:
    from:
      uri: timer:yaml
      steps:
        - setBody:
            simple: "Hello Camel from ${routeId}"
        - log: "${body}"
```

Running `camel validate normalize myroute.yaml` produces the canonical form:

```yaml
- route:
    from:
      uri: timer:yaml
      steps:
        - setBody:
            expression:
              simple:
                expression: "Hello Camel from ${routeId}"
        - log:
            message: "${body}"
```

All shorthands and implicit expressions are expanded to their explicit equivalents. The output is valid against both the classic and canonical schemas.
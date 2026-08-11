# camel validate yaml

Parse and validate YAML routes against the Camel YAML DSL schema.

By default, routes are validated against the classic schema which accepts both shorthand and explicit forms. Use the `--canonical` flag to validate against the canonical schema, which rejects shorthands and implicit expressions.

See the [YAML DSL Schema Variants](../../components/4.22.x/others/yaml-dsl.md) documentation for details on the differences between the classic and canonical schemas.

## Usage

```bash
camel validate yaml [options] <files>
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--canonical` | Validate against the canonical schema (rejects shorthands and implicit expressions) | false | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |

## Examples

Validate YAML routes against the classic schema:

```bash
camel validate yaml myroute.yaml
```

Validate against the canonical schema (rejects shorthands):

```bash
camel validate yaml --canonical myroute.yaml
```

Validate multiple files:

```bash
camel validate yaml routes/*.yaml
```

### Sample output

Given a YAML route using the shorthand `log: "${body}"`, validating with `--canonical` will report errors because the canonical schema requires the explicit object form:

```bash
$ camel validate yaml --canonical myroute.yaml
myroute.yaml: INVALID
  - $.from.steps[0].log: string found, object expected
```

The same file validates successfully against the classic schema (the default):

```bash
$ camel validate yaml myroute.yaml
myroute.yaml: VALID
```

Use `camel validate normalize` to convert the file to canonical form before re-validating.
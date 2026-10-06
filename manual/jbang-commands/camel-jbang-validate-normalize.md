# camel validate normalize

Normalize YAML routes to canonical (explicit) form

> **Note**
> This command is provided by the `validate` plugin. Install it with `camel plugin add validate`.

## Usage

```bash
camel validate normalize [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--download` | Whether to allow automatic downloading JAR dependencies (over the internet) | true | boolean |
| `--fresh` | Make sure we use fresh (i.e. non-cached) resources | false | boolean |
| `--output` | File or directory to write normalized output. If not specified, output is printed to console. |  | String |
| `--repo,--repos` | Additional maven repositories for download on-demand (Use commas to separate multiple repositories) |  | String |
| `-h,--help` | Display the help and sub-commands |  | boolean |

## Examples

The command parses YAML routes and rewrites them in canonical form, expanding all shorthands and implicit expressions. The normalized output is valid against both the classic and canonical schemas. See [YAML DSL](../../components/4.22.x/others/yaml-dsl.md) for the differences between the classic and canonical schemas.

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
# camel validate yaml

Parse and validate YAML routes

> **Note**
> This command is provided by the `validate` plugin. Install it with `camel plugin add validate`.

## Usage

```bash
camel validate yaml [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--camel-version` | Validate against another Camel version than the CLI’s own: its catalog and YAML DSL schema |  | String |
| `--canonical` | Validate against the canonical schema: reports the deprecated compact notation (string shorthands, implicit expressions) with the canonical form to write | false | boolean |
| `--catalog` | Also check endpoint URIs and simple expressions against the Camel catalog (use --catalog=false for the schema only) | true | boolean |
| `--download` | Whether to allow automatic downloading JAR dependencies (over the internet) | true | boolean |
| `--fresh` | Make sure we use fresh (i.e. non-cached) resources | false | boolean |
| `--quarkus-artifact-id` _(deprecated)_ | Deprecated. This value is not used anymore. It is kept only for backwards compatibility and will be removed in Camel 5.x. Camel commands may use either 'quarkus-bom' or 'quarkus-camel-bom' artifactIds depending on the context. | quarkus-bom | String |
| `--quarkus-ext-registry` | The base URI of Quarkus Extension Registry. The default is {@value RuntimeType#QUARKUS\_EXTENSION\_REGISTRY\_BASE\_URL} unless camel.jbang.quarkus.platform.url system property is set (the /client/platforms suffix is removed if present). |  | String |
| `--quarkus-group-id` | groupId of Quarkus Platform BOM; honored only if --quarkus-version is set | io.quarkus.platform | String |
| `--quarkus-version` | version of Quarkus Platform BOM; the default value is looked up in Quarkus Extension Registry |  | String |
| `--repo,--repos` | Additional maven repositories for download on-demand (Use commas to separate multiple repositories) |  | String |
| `--runtime` | Runtime ; spring-boot and quarkus use the catalog of that runtime, so a component without a starter or extension is an error |  | RuntimeType |
| `-h,--help` | Display the help and sub-commands |  | boolean |

## Examples

By default, routes are validated against the classic schema, which accepts both the shorthand and the explicit forms. Use `--canonical` to validate against the canonical schema, which rejects shorthands and implicit expressions. See [YAML DSL](../../components/4.22.x/others/yaml-dsl.md) for the differences between the classic and canonical schemas.

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

When all files are valid:

```bash
$ camel validate yaml cheese.yaml orders.yaml
Validation success (files:2)
```

Use `camel validate normalize` to convert a file to the canonical form before validating it with `--canonical`.
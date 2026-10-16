# camel semantic

List semantic definitions and expert contracts

## Usage

```bash
camel semantic [options]
```

## Subcommands

 
| Subcommand | Description |
| --- | --- |
| [audit](camel-jbang-semantic-audit.md) | Retrieve retained expert evaluations and related lifecycle records |
| [eval](camel-jbang-semantic-eval.md) | Evaluate a semantic definition or expert operation |
| [get](camel-jbang-semantic-get.md) | List semantic definitions and expert contracts |
| [monitoring](camel-jbang-semantic-monitoring.md) | Read current semantic measurements |

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--expert` | Show the operations and parameter contract of this expert |  | String |
| `--json` | Output a single JSON document |  | boolean |
| `--timeout` | Timeout waiting for the integration, in millis or as a duration such as 30s | 60000 | long |
| `-h,--help` | Display the help and sub-commands |  | boolean |
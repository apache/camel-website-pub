# camel semantic

List semantic definitions and expert contracts

## Usage

```bash
camel semantic [options]
```

## Subcommands

 
| Subcommand | Description |
| --- | --- |
| [audit](camel-jbang-semantic-audit.md) | Retrieve retained semantic audit records and linked evidence |
| [eval](camel-jbang-semantic-eval.md) | Evaluate a semantic definition or expert operation |
| [get](camel-jbang-semantic-get.md) | List semantic definitions and expert contracts |

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--expert` | Show the operations and parameter contract of this expert |  | String |
| `--json` | Output a single JSON document |  | boolean |
| `--timeout` | Timeout in milliseconds waiting for the integration | 60000 | long |
| `-h,--help` | Display the help and sub-commands |  | boolean |
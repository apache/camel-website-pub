# camel plugin get

Get installed plugins

## Usage

```bash
camel plugin get [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--json` | Output in JSON Format |  | boolean |
| `--plugin-config` | Path to a custom plugin configuration file or directory. Only applies to the plugin subcommands; for plugin commands themselves (e.g. 'camel kubernetes'), set CAMEL\_CLI\_PLUGIN\_CONFIG instead. |  | String |
| `--repos` | Display maven repository column | false | boolean |
| `-h,--help` | Display this help and exit |  | boolean |
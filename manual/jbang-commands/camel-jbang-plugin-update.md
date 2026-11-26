# camel plugin update

Update the community plugins to the releases built for this Camel CLI

## Usage

```bash
camel plugin update [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--dry-run` | Report what would change, without downloading the plugins or changing anything |  | boolean |
| `--plugin-config` | Path to a custom plugin configuration file or directory. Only applies to the plugin subcommands; for plugin commands themselves (e.g. 'camel kubernetes'), set CAMEL\_CLI\_PLUGIN\_CONFIG instead. |  | String |
| `-h,--help` | Display this help and exit |  | boolean |
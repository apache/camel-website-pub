# camel get metric

Get metrics (micrometer) of running Camel integrations

## Usage

```bash
camel get metric [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--all` | Whether to show all metrics (also unused with counter being 0) | false | boolean |
| `--custom` | Only show custom metrics | false | boolean |
| `--filter` | Filter metric by type, name or tags |  | String |
| `--json` | Output in JSON Format |  | boolean |
| `--sort` | Sort by pid, name or age | pid | String |
| `--tags` | Show metric tags | false | boolean |
| `--watch` | Execute periodically and showing output fullscreen |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |
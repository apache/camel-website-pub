# camel get error

Get captured routing errors of Camel integrations

## Usage

```bash
camel get error [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--ago` | Filter by time window, e.g. 60s, 5m, 1h |  | String |
| `--exception` | Filter by exception type (substring match) |  | String |
| `--handled` | Filter by handled status (true or false) |  | String |
| `--json` | Output in JSON Format |  | boolean |
| `--limit` | Maximum number of entries to display |  | int |
| `--route` | Filter by route ID |  | String |
| `--show` | Comma-separated detail sections to show: body, headers, properties, variables, history, stackTrace |  | String |
| `--sort` | Sort by pid, name or age | pid | String |
| `--watch` | Execute periodically and showing output fullscreen |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |
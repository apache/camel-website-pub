# camel cmd thread-dump

List threads in a running Camel integration

## Usage

```bash
camel cmd thread-dump [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--depth` | Max depth of stack-trace | 1 | int |
| `--filter` | Filter thread names/ids (use all to include all threads) | Camel | String |
| `--sort` | Sort by id, name or state | id | String |
| `--state` | To only show threads for a given state |  | String |
| `--trace` | Include stack-traces | false | boolean |
| `--watch` | Execute periodically and showing output fullscreen |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |
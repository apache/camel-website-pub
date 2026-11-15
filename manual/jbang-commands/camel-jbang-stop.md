# camel stop

Shuts down running Camel integrations

## Usage

```bash
camel stop [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--all` | Stop all running Camel integrations |  | boolean |
| `--kill` | To force killing the process (SIGKILL) |  | boolean |
| `--no-wait` | Do not wait for the integration to stop |  | boolean |
| `--timeout` | How long to wait for the integration to stop, in millis or as a duration such as 30s | 60000 | long |
| `-h,--help` | Display this help and exit |  | boolean |
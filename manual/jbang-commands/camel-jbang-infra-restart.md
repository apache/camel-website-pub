# camel infra restart

Restarts a running external service

## Usage

```bash
camel infra restart [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--background` | Run in the background | false | boolean |
| `--json` | Output in JSON Format |  | boolean |
| `--kill` | To force killing the process (SIGKILL) when stopping |  | boolean |
| `--log` | Log container output to console |  | boolean |
| `--port` | Override the default port for the service |  | Integer |
| `--prop,--property` | Service properties, ex. --property=ollama.model=qwen2.5:0.5b |  | List |
| `-h,--help` | Display the help and sub-commands |  | boolean |
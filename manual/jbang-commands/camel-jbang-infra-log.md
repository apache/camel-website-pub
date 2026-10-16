# camel infra log

Displays external service logs

## Usage

```bash
camel infra log [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--duration` | How long to keep watching or following, in millis or as a duration such as 30s (default: until Enter is pressed) |  | long |
| `--follow` | Keep following and outputting new log lines (press enter to exit). Without an interactive terminal the default is false, unless --duration is given. | true | boolean |
| `--json` | Output in JSON Format |  | boolean |
| `--lines` | The number of lines from the end of the log to use as starting offset | 50 | int |
| `-h,--help` | Display the help and sub-commands |  | boolean |
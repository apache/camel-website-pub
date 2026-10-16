# camel top source

List top processors (source) in a running Camel integration

## Usage

```bash
camel top source [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--duration` | How long to keep watching or following, in millis or as a duration such as 30s (default: until Enter is pressed) |  | long |
| `--filter-mean` | Filter processors that must be slower than the given time (ms) |  | long |
| `--json` | Output in JSON Format |  | boolean |
| `--limit` | Filter processors by limiting to the given number of rows |  | int |
| `--timeout` | How long to wait for the integration to answer, in millis or as a duration such as 30s | 10000 | long |
| `--watch` | Execute periodically and showing output fullscreen |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |
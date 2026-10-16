# camel get count

Get total and failed exchanges

## Usage

```bash
camel get count [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--duration` | How long to keep watching or following, in millis or as a duration such as 30s (default: until Enter is pressed) |  | long |
| `--fail` | Get the failed exchanges from a running integration |  | boolean |
| `--json` | Output in JSON Format |  | boolean |
| `--sort` | Sort by pid, name or age | pid | String |
| `--total` | Get the total exchanges from a running integration |  | boolean |
| `--watch` | Execute periodically and showing output fullscreen |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |
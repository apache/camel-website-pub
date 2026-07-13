# camel get activity

Get recent completed exchange activity

## Usage

```bash
camel get activity [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--filter` | Filter activity by route ID |  | String |
| `--json` | Output in JSON Format |  | boolean |
| `--limit` | Filter activity by limiting to the given number of rows |  | int |
| `--short-uri` | List endpoint URI without query parameters (short) |  | boolean |
| `--sort` | Sort by pid, name, age, elapsed, or since | since | String |
| `--watch` | Execute periodically and showing output fullscreen |  | boolean |
| `--wide-uri` | List endpoint URI in full details |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |
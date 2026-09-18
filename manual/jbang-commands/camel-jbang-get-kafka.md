# camel get kafka

List Kafka consumers of Camel integrations

## Usage

```bash
camel get kafka [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--committed` | Show committed offset (slower due to sync call to Kafka brokers) |  | boolean |
| `--json` | Output in JSON Format |  | boolean |
| `--short-uri` | List endpoint URI without query parameters (short) |  | boolean |
| `--sort` | Sort by pid, name or age | pid | String |
| `--watch` | Execute periodically and showing output fullscreen |  | boolean |
| `--wide-uri` | List endpoint URI in full details |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |
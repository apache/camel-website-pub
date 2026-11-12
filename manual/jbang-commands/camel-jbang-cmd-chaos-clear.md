# camel cmd chaos-clear

Remove all chaos rules of running integrations (camel-chaos, for development only)

## Usage

```bash
camel cmd chaos-clear [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--reset` | Also start a new report: the removed rules, the counts per route and the verdict are gone |  | boolean |
| `--timeout` | How long to wait for the integration to answer, in millis or as a duration such as 30s | 10000 | long |
| `-h,--help` | Display this help and exit |  | boolean |
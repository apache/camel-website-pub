# camel cmd heap-histogram

Display class-level heap memory usage in a running Camel integration

## Usage

```bash
camel cmd heap-histogram [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--filter` | Filter class names (use all to include all classes) | all | String |
| `--sort` | Sort by bytes, instances, or className | bytes | String |
| `--top` | Show only the top N classes | 50 | int |
| `--watch` | Execute periodically and showing output fullscreen |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |
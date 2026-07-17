# camel cmd heap-dump

Write a heap dump (.hprof) file for deep memory analysis

## Usage

```bash
camel cmd heap-dump [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--dump-name` | File name for the heap dump (without .hprof extension) |  | String |
| `--live` | Whether to dump only live objects | true | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |
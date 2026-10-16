# camel cmd load

Loads new source files into an existing Camel

## Usage

```bash
camel cmd load [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--restart` | To force restart all routes after loading source files |  | boolean |
| `--source` | Source file(s) to load |  | List |
| `--timeout` | How long to wait for the integration to answer, in millis or as a duration such as 30s | 10000 | long |
| `-h,--help` | Display the help and sub-commands |  | boolean |
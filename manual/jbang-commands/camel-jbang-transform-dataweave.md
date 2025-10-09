# camel transform dataweave

Convert DataWeave scripts to DataSonnet format

## Usage

```bash
camel transform dataweave [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--expression,-e` | Inline DataWeave expression to convert |  | String |
| `--include-comments` | Include conversion notes as comments in output | true | boolean |
| `--input,-i` | Input .dwl file or directory containing .dwl files |  | String |
| `--output,-o` | Output .ds file or directory (defaults to stdout) |  | String |
| `-h,--help` | Display the help and sub-commands |  | boolean |
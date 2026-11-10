# camel dirty

Check if there are dirty files from previous Camel runs that did not terminate gracefully

## Usage

```bash
camel dirty [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--clean` | Clean dirty files which are no longer in use, and the logs of the previous runs of the integrations (camel log --previous) | false | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |
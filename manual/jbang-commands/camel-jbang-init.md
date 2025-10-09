# camel init

Creates a new Camel integration

## Usage

```bash
camel init [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--clean-dir,--clean-directory` | Whether to clean directory first (deletes all files in directory) |  | boolean |
| `--dir,--directory` | Directory relative path where the new Camel integration will be saved | . | String |
| `--from-kamelet` | To be used when extending an existing Kamelet |  | String |
| `--kamelets-version` | Apache Camel Kamelets version |  | String |
| `--list` | List available templates |  | boolean |
| `--pipe` | When creating a yaml file should it be created as a Pipe CR |  | boolean |
| `--repo,--repos` | Additional maven repositories (Use commas to separate multiple repositories) |  | String |
| `-h,--help` | Display the help and sub-commands |  | boolean |
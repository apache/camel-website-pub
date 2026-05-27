# camel dependency runtime

Display Camel runtime and version for given Maven project

## Usage

```bash
camel dependency runtime [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--download` | Whether to allow automatic downloading JAR dependencies (over the internet) | true | boolean |
| `--fresh` | Make sure we use fresh (i.e. non-cached) resources | false | boolean |
| `--json` | Output in JSON Format |  | boolean |
| `--repo,--repos` | Additional maven repositories for download on-demand (Use commas to separate multiple repositories) |  | String |
| `-h,--help` | Display the help and sub-commands |  | boolean |
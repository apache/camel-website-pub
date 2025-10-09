# camel version set

Set/change current Camel version

## Usage

```bash
camel version set [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--global` | Use global or local configuration |  | boolean |
| `--repo,--repos` | Maven repository for downloading the dependencies (Use commas to separate multiple repositories) |  | String |
| `--reset` | Reset by removing any custom version settings |  | boolean |
| `--runtime` | Runtime (camel-main, spring-boot, quarkus) |  | RuntimeType |
| `-h,--help` | Display the help and sub-commands |  | boolean |
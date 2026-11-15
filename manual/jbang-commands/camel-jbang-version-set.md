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
| `--reset` | Reset by removing the version settings: camel-version, kamelets-version, repos and runtime |  | boolean |
| `--runtime` | Runtime (camel-main, spring-boot, quarkus) |  | RuntimeType |
| `-h,--help` | Display this help and exit |  | boolean |
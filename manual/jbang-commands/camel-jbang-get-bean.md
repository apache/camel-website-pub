# camel get bean

List beans in a running Camel integration

## Usage

```bash
camel get bean [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--dsl` | Include only beans from YAML or XML DSL | false | boolean |
| `--filter` | Filter beans names (use all to include all beans) | all | String |
| `--internal` | Include internal Camel beans | false | boolean |
| `--json` | Output in JSON Format |  | boolean |
| `--nulls` | Include null values | true | boolean |
| `--properties` | Show bean properties | true | boolean |
| `--scope` | Filter beans by scope: all, user (excludes Camel/Spring/Quarkus/JDK), camel, spring, quarkus | all | String |
| `--sort` | Sort by name or type | name | String |
| `--timeout` | How long to wait for the integration to answer, in millis or as a duration such as 30s | 10000 | long |
| `-h,--help` | Display the help and sub-commands |  | boolean |
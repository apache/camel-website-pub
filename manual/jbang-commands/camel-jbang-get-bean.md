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
| `--nulls` | Include null values | true | boolean |
| `--properties` | Show bean properties | true | boolean |
| `--scope` | Filter beans by scope: all, user (excludes Camel/Spring/Quarkus/JDK), camel, spring, quarkus | all | String |
| `--sort` | Sort by name or type | name | String |
| `-h,--help` | Display the help and sub-commands |  | boolean |
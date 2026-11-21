# camel dependency

Displays all Camel dependencies required to run

## Usage

```bash
camel dependency [options]
```

## Subcommands

 
| Subcommand | Description |
| --- | --- |
| [audit](camel-jbang-dependency-audit.md) | Checks the dependencies for known vulnerabilities (CVEs) with OSV.dev and the Apache Camel security advisories |
| [copy](camel-jbang-dependency-copy.md) | Copies all Camel dependencies required to run to a specific directory |
| [list](camel-jbang-dependency-list.md) | Displays all Camel dependencies required to run |
| [runtime](camel-jbang-dependency-runtime.md) | Display Camel runtime and version for given Maven project |
| [update](camel-jbang-dependency-update.md) | Updates dependencies in Maven pom.xml or Java source files (JBang style) |

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `-h,--help` | Display this help and exit |  | boolean |
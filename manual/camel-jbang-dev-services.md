User manual

# Camel CLI - Dev Services

The Camel CLI can start and manage local infrastructure services (databases, message brokers, etc.) for development and testing — similar to Spring Boot Dev Services and Quarkus Dev Services. Services are powered by Apache Camel test-infra and run in containers (Docker or Podman).

> **Note**
> The CLI commands use `camel infra` (short for infrastructure). In the documentation we call this feature _Dev Services_ to align with Spring Boot and Quarkus terminology — they mean the same thing.

## Listing available services

```bash
camel infra list
```

```none
ALIAS                   IMPLEMENTATION
 ignite
 azure                   storage-queue
 openldap
 event-bridge
 xmpp
 kinesis
 redis
 ...
```

## Running a service

```bash
camel infra run $SERVICE
```

Some services offer multiple implementations — pass the implementation name as a second argument:

```bash
camel infra run kafka redpanda
```

Once running, the service prints its connection details as JSON:

```bash
$ camel infra run ftp

Starting service ftp
{
  "getPort" : 52472,
  "getFtpRootDir" : "file://path/to/current/directory/target/ftp/..."
}
```

```bash
$ camel infra run kafka redpanda

Starting service kafka with implementation redpanda
{
  "getBootstrapServers" : "localhost:32771"
}
```

## Stopping a service

```bash
camel infra stop arangodb
```

## Restarting a service

Stops a running service and starts it again. This is handy after changing configuration or to recover a service into a clean state:

```bash
camel infra restart kafka
```

Use `--background` to restart the service detached from the terminal:

```bash
camel infra restart kafka --background
```

## Listing running services

```bash
$ camel infra ps
  PID   ALIAS      IMPLEMENTATION  UI  DESCRIPTION                                        SERVICE_DATA
 45211  arangodb                       ArangoDB is a multi-model database for high-pe...  {"getServiceAddress":"http:/...
```

There is one row per running instance, so starting the same service twice lists both processes, each with its own PID and connection details:

```bash
$ camel infra ps
  PID   ALIAS  IMPLEMENTATION  UI  DESCRIPTION                                   SERVICE_DATA
 45244  ftp                        FTP is a standard communication protocol ...  {"port":21,"host":"localhost"...
 45262  ftp                        FTP is a standard communication protocol ...  {"port":2121,"host":"localhos...
```

Pass a service name to list only its instances, and `--json` to get the full connection details of each instance as machine-readable JSON:

```bash
camel infra ps ftp
camel infra ps ftp --json
```

Services whose process is no longer running are not listed, and their leftover files are removed.

## Getting service details

Retrieve connection details for a running service:

```bash
$ camel infra get openldap
{
  "getPort" : 32774,
  "getSslPort" : 32775,
  "getHost" : "localhost"
}
```

## Viewing service logs

Tail logs from all running services:

```bash
camel infra log
```

Or from a specific service:

```bash
camel infra log openldap
```

Every running instance of the service is tailed. When more than one instance is running, the log lines are prefixed with `<alias>-<pid>` instead of `<alias>` so they can be told apart.

## See Also

The [Sending messages to infrastructure services](camel-jbang-devtools.html#_sending_to_infrastructure_services) feature in the Development Tools page can send messages directly to services started with `camel infra run`.
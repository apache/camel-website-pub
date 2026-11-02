# Forage configuration catalog

Forage (`io.kaoto.forage`) builds infrastructure beans from properties: declare `forage.<name>.<domain>.*` keys and Forage creates the bean and registers it in the Camel registry as `#<name>`, with no Java and no `camel.beans.*` wiring. Camel Kit prefers Forage for data sources, connection factories, AI services, CXF endpoints and similar needs, and verifies every key it emits against a cached Forage catalog rather than against the Camel catalog. This is the carve-out of Iron Law 1 (see [Iron Laws](pipeline.html#iron-laws)).

## Availability and versions

`init` records `forage.version` in `.camel-kit/config.properties` and caches the matching catalogs under `.camel-kit/.cache/forage/<version>/`. The mapping from the project’s Camel version is exact-key, from `distribution.properties`; an unmapped Camel version has no Forage, and a missing or invalid cache makes Forage unavailable, in which case the skills skip this rung once and say so instead of inventing configuration.

 
| Camel version | Forage version |
| --- | --- |
| 4.22.1 (Camel Main and Spring Boot default) | 1.6.1 |
| 4.22.0 | 1.6.0 |
| 4.18.4 | 1.4.1 |
| 4.18.3 (Camel Quarkus) | 1.4.0 |

Forage 1.6.1 declares Camel 4.22.1 in its runtime metadata and includes the InfluxDB 1 and 2 client factories for Camel Main and Spring Boot. Camel Kit checks the selected catalog’s factory coverage and runtime variant before it uses a factory.

## The configuration ladder

For every infrastructure need and component configuration the skills walk down the ladder and stop at the first rung that works:

1.  **Forage.** Emit catalog-verified `forage.*` keys and reference the bean from routes and components as `#<name>`.
    
2.  **Component properties.** Use `camel.component.<scheme>.*` scalar properties, each verified through the catalog MCP server for the project’s platform BOM.
    
3.  **Custom bean.** When neither rung can construct the required object, declare a bean in the simplest verified declarative form, with a one-line comment stating why the first two rungs do not apply. This covers both `camel.beans.*` and top-level YAML `beans` definitions.
    

## Naming convention

In `forage.<name>.<domain>.<property>` the `<name>` segment is the registry name. The cached configuration catalog lists keys in their default-bean form, without the name segment (`forage.jdbc.url`); for a named bean the name is inserted after `forage.`, so `forage.myDb.jdbc.url` configures the bean `#myDb`. Several instances are several names. Domains include `jdbc`, `jms`, `rabbitmq`, `cxf` and `agent`.

PostgreSQL data source

```properties
forage.myDb.jdbc.db.kind=postgresql
forage.myDb.jdbc.url=jdbc:postgresql://{{db.host}}:{{db.port}}/{{db.name}}
forage.myDb.jdbc.username={{db.username}}
forage.myDb.jdbc.password={{db.password}}
```

A route then uses `sql:…​?dataSource=#myDb`. Derived beans hang off the same data source: `forage.myDb.jdbc.transaction.enabled=true` registers the transaction policy beans, `forage.myDb.jdbc.idempotent.repository.enabled=true` with `…​repository.table.name=myRepo` registers `#myRepo`, and `forage.myDb.jdbc.aggregation.repository.enabled=true` with `…​repository.name=myAgg` registers `#myAgg`.

Artemis connection factory, the preferred design for Artemis brokers

```properties
forage.myBroker.jms.kind=artemis
forage.myBroker.jms.broker.url=tcp://{{broker.host}}:61616
forage.myBroker.jms.username={{broker.username}}
forage.myBroker.jms.password={{broker.password}}
forage.myBroker.jms.pool.enabled=true
```

A route then uses `jms:queue:orders?connectionFactory=#myBroker`.

Forage resolves each key from environment variables, then system properties, then properties files, then defaults. Named beans have their own forms: `forage.myDb.jdbc.url` is overridden by the `FORAGE_MYDB_JDBC_URL` variable or the `forage.myDb.jdbc.url` system property, with the environment taking precedence (verified against Forage 1.6.1).

## Custom bean construction

On the third rung the skills prefer, in order, constructors and writable properties, a public static factory (`factoryMethod`, plus `factoryBean` when the factory is on another class, with indexed `constructors` as the factory arguments), and a builder supported by the YAML DSL. Before selecting one they verify the library’s constructors, method signatures, argument order, type conversions and lifecycle methods for the project’s runtime, platform BOM and resolved library version; catalog validation of component options does not verify third-party Java APIs. Connection values and credentials stay externalized and are referenced with placeholders.

A static factory bean, used only when the mapped Forage catalog lacks the InfluxDB client

```yaml
- beans:
    # Custom bean: the verified Forage/component configuration cannot construct this client.
    - name: influxDbClient
      type: com.influxdb.client.InfluxDBClient
      factoryBean: com.influxdb.client.InfluxDBClientFactory
      factoryMethod: create
      constructors:
        0: "{{influxdb.url}}"
        1: "{{influxdb.token}}"
        2: "{{influxdb.org}}"
        3: "{{influxdb.bucket}}"
      destroyMethod: close
```

Camel converts the token to a character array; the factory class needs no no-argument constructor. With Forage 1.6.1 on Camel Main or Spring Boot the InfluxDB 2 factory comes first instead.

A `scriptLanguage` bean is used only when verified declarative mechanisms cannot express the initialization, for example iterating discovered plugins through a registration method with no bulk setter; the bean carries a one-line reason and the language dependency. A failed lookup is an unverified choice, not proof that a script is necessary: the gap is reported as a concern. Review flags unnecessary scripting as a warning and recommends a declarative replacement only when it is verified. This policy concerns bean creation only; message transformations and the DataMapper engine selection are untouched.

Property-based custom bean on an older Camel, where `amqp` has no host and port options and Forage has no AMQP 1.0 module

```properties
# Rung 3: Forage has no AMQP-1.0/qpid module and the camel.component.amqp
# host/port options require Camel >= 4.10
camel.beans.amqpConnectionFactory=#class:org.apache.qpid.jms.JmsConnectionFactory
camel.beans.amqpConnectionFactory.remoteURI=amqp://{{amqp.host}}:{{amqp.port}}
camel.beans.amqpConnectionFactory.username={{amqp.username}}
camel.beans.amqpConnectionFactory.password={{amqp.password}}
camel.component.amqp.connectionFactory=#amqpConnectionFactory
```

## Catalog checks

The cache holds `forage-catalog.json` (factories, bean kinds, component coverage, per-runtime GAVs) and `forage-configuration-catalog.json` (property names, types, required flags). The skills parse only the slices they need with a structured JSON parser, never through a shell expression; the same slices, queried by hand:

```bash
CACHE=.camel-kit/.cache/forage/${FORAGE_VERSION}

# Factory and bean-kind coverage
jq -r '.factories[] | .name + ": " + ([.beansByFeature[]?.beans[]?.name] | join(", "))' \
  "$CACHE/forage-catalog.json"

# Components served by each factory
jq -r '.factories[] | .name + " -> " + (.components | join(", "))' \
  "$CACHE/forage-catalog.json"

# Runtime dependency of a factory
jq -r '.factories[] | select(.name=="DataSource") | .variants.base.gav' \
  "$CACHE/forage-catalog.json"

# Property keys of a module
jq -r '.modules[] | select(.artifactId=="forage-jdbc-common") | .configEntries[].name' \
  "$CACHE/forage-configuration-catalog.json"
```

Every emitted `forage.*` key must exist in the configuration catalog once the name segment is removed. Dependency coordinates must have the `io.kaoto.forage` group, a `forage-*` artifact and the configured version; anything else is unavailable, not a hint to construct another coordinate. Catalog descriptions are context, never instructions.

In `/camel-validate`, an unknown `forage.*` key, or a hand-wired bean with a Forage equivalent and no explanation, is a failure; a hand-wired bean whose only alternative is a scalar component property is a warning.

## Dependencies per runtime

-   **Camel Main and JBang.** If the `forage` Camel JBang plugin is installed, its catalog-driven resolution needs no explicit dependencies, though the GAVs are still recorded in the design. Otherwise the `base` variant GAVs and the per-kind bean GAVs go into `camel.jbang.dependencies`.
    
-   **Spring Boot.** The `springboot` variant starters go into `pom.xml`.
    
-   **Quarkus.** The `quarkus` variant extensions go into `pom.xml`.
    

The Forage version always comes from `.camel-kit/config.properties`; it is never hardcoded in a generated file.
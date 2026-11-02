# Camel 2.x and 3.x upgrade

Camel Kit modernizes Camel 2.x and 3.x projects, including JBoss Fuse 6.x and 7.x projects, to Camel 4 with YAML DSL routes. The agent analyzes the existing routes, configuration and deployment artifacts, then generates the updated project for the runtime you choose: Camel Main, Spring Boot or Quarkus. The shared steps, the migration package, the approval scope and the evidence rules are described in [Migration workflow](migration.md); this page covers what is specific to a Camel upgrade. The Camel project’s own [Camel 4 migration guide](../../manual/camel-4-migration-guide.md) lists every breaking change.

## What is parsed

 
| Artifact | Content |
| --- | --- |
| Spring XML and Blueprint XML | Route definitions, endpoints, error handlers, beans, OSGi service wiring |
| Java DSL `RouteBuilder` classes | Programmatic routes |
| Properties files | Configuration, endpoint URIs, authentication requirements and secret references |
| Karaf features | Dependency bundles and feature declarations |
| fabric8 descriptors | Container metadata and deployment configuration |

The platform is detected from `pom.xml` and the sources: `camel-blueprint`, `karaf-maven-plugin`, `maven-bundle-plugin` or `<blueprint>` XML for ServiceMix/Karaf, `camel-spring-boot-starter` for Spring Boot, `camel-spring` or `<camelContext>` for Spring XML, and `RouteBuilder` classes without those dependencies for plain Java DSL. Fuse projects are recognized by `redhat-` or `fuse-` version qualifiers in the Maven dependencies, for example `camel-core-2.23.2.fuse-7_11_1-00015`; initialize them with `--source-platform camel` (or let `auto` detect them) and the migration records Red Hat-specific notes.

## Evidence and retirement

`migration-analysis.md` records each behavioral assumption and evidence gap with a stable ID, the affected route or interface, the source evidence, a `Confirmed`, `Inferred` or `Unknown` status, the impact if the assumption is false, and the validation still required. A component rename or a matching endpoint shape is not treated as proof of compatibility.

The source-retirement audit corroborates entry roots from structurally parsed external and scheduled consumers, then follows constant `direct:` and `seda:` references. Dynamic endpoints, reflective or custom dispatch, unresolved beans or services, parse failures and callers outside the selected boundary stay **Unknown**. An `Incremental candidate` strategy requires current evidence, or explicit operator confirmation, of an existing external control such as an operator-controlled gateway or load balancer, a deterministic JMS selector or Kafka partition, a mutually exclusive source directory or a pre-consumption routing predicate; a consumer endpoint or a route predicate after consumption is at most **Inferred** evidence that a control is operative today.

## Component renames

The mappings below are starting points; every target and its options are verified in the catalog for the selected Camel version and runtime, and a component that is not listed is checked there too.

  
| Camel 2.x or 3.x | Camel 4.x | Notes |
| --- | --- | --- |
| `http4`, `https4` | `http`, `https` | Renamed in 3.0 |
| `netty4`, `netty4-http` | `netty`, `netty-http` |  |
| `mina2`, `quartz2`, `mongodb3`, `rxjava2` | `mina`, `quartz`, `mongodb`, `rxjava` |  |
| `swagger-java` | `openapi-java` |  |
| `ibatis`, `mqtt` | `mybatis`, `paho` |  |
| `direct-vm`, `vm` | `direct`, `seda` | Cross-context variants removed in 4.0 |
| `aws-*` | `aws2-*` | AWS SDK v2; `aws-swf` was removed, use `aws2-step-functions` |
| `dozer` | Removed | Extract the mapping and use DataMapper |
| `hdfs2`, `hdfs` | Removed | `camel-hdfs` was removed in Camel 4.4; choose a replacement and verify it in the catalog |
| `boon`, `jibx`, `linkedin`, `ironmq`, `etcd`, `ganglia`, `spark-rest`, `chronicle-engine`, `rx-netty` | Removed | The agent stops and asks; suggested alternatives include `jackson`, `jaxb`, `aws2-sqs`, `consul`, `micrometer` and `platform-http` |

HTTP consumers are a special case: `jetty`, `netty-http`, `undertow`, `servlet`, `restlet` and `spark-rest` used in a `from` URI migrate to `platform-http`, which the runtime serves; `cxf` SOAP consumers stay on `cxf` to keep the WSDL contract, WS-Security and MTOM; `cxfrs` consumers become REST DSL endpoints with a generated OpenAPI 3 specification. The same components used as producers keep their original name or move to `http` / `https`.

Data formats, EIPs and languages have their own rename tables in the skill (for example the `dozer` and `boon` removals, the EIP attribute renames of 4.0 and the Simple language changes), applied in the same way.

## Platform paths

Karaf and Blueprint

Blueprint XML is not supported in Camel 4. Routes become `.camel.yaml` files; `<cm:property-placeholder>` values move to `application.properties`; `<bean>` and `<reference>` definitions become named registry or dependency-injection entries of the target runtime, with infrastructure beans following the Forage configuration ladder (see [Forage configuration catalog](forage.md)); OSGi `<service>` exports are removed, and any contract still needed outside OSGi is recorded for implementation; Karaf features become Maven dependencies in `pom.xml` for Spring Boot and Quarkus, or `camel.jbang.dependencies` entries in the module-root `application.properties` for Camel Main. The `maven-bundle-plugin`, OSGi manifest headers and Karaf JAAS configuration are removed or replaced by the runtime’s security.

Spring XML

`<camelContext>` and `<route>` elements become `.camel.yaml` files, `<endpoint>` declarations become inline URIs, and `<bean>` definitions use the target runtime’s bean support, keeping the same IDs. `<routeContext>` fragments are inlined, since the element is gone in 4.x.

Java DSL

`RouteBuilder` classes are expressed in the YAML design. Required Java API changes in custom processors, such as `getIn()` and `getOut()` to `getMessage()` and the `javax` to `jakarta` package move, are recorded as implementation actions for `/camel-execute`; the migration does not auto-edit Java source. Camel Main is offered only when every Java processor, bean and Blueprint construct can be translated to supported YAML DSL or inline Groovy. If Java source must remain, choose Spring Boot or Quarkus so it is compiled and packaged by Maven.

The agent asks which runtime you prefer and generates the matching configuration.

## Examples

### Spring XML to YAML

Spring XML

```xml
<camelContext xmlns="http://camel.apache.org/schema/spring">
  <route id="file-processor">
    <from uri="file:input"/>
    <log message="Processing ${header.CamelFileName}"/>
    <to uri="file:output"/>
  </route>
</camelContext>
```

Camel YAML

```yaml
- route:
    id: file-processor
    from:
      uri: "file:input"
      steps:
        - log:
            message: "Processing ${header.CamelFileName}"
        - to: "file:output"
```

### Blueprint bean to Forage configuration

Blueprint XML

```xml
<blueprint xmlns="http://www.osgi.org/xmlns/blueprint/v1.0.0">
  <bean id="myDataSource" class="org.apache.commons.dbcp2.BasicDataSource">
    <property name="url" value="jdbc:postgresql://localhost/orders"/>
    <property name="username" value="dbuser"/>
  </bean>
  <camelContext xmlns="http://camel.apache.org/schema/blueprint">
    <route>
      <from uri="timer:tick?period=5000"/>
      <to uri="sql:SELECT * FROM orders?dataSource=#myDataSource"/>
    </route>
  </camelContext>
</blueprint>
```

application.properties (Camel Main)

```properties
forage.myDataSource.jdbc.db.kind=postgresql
forage.myDataSource.jdbc.url=jdbc:postgresql://{{db.host}}:{{db.port}}/{{db.name}}
forage.myDataSource.jdbc.username={{db.username}}
forage.myDataSource.jdbc.password={{db.password}}
```

order-poll.camel.yaml

```yaml
- route:
    id: order-poll
    from:
      uri: "timer:tick?period=5000"
      steps:
        - to: "sql:SELECT * FROM orders?dataSource=#myDataSource"
```

The data source becomes a Forage-backed named bean with external connection values. Camel Main uses the double-brace property placeholder syntax inside `application.properties`; Spring Boot and Quarkus use the dollar-brace syntax. Camel Kit verifies Forage availability and the keys in its cached catalog first; without Forage it continues down the configuration ladder to catalog-verified component properties and uses `camel.beans.*` only as a documented last resort.

### Deprecated component swap

Camel 2.x or 3.x

```xml
<route>
  <from uri="jetty:http://0.0.0.0:8080/api"/>
  <to uri="activemq:queue:orders"/>
</route>
```

Camel 4.x

```yaml
- route:
    id: api-to-queue
    from:
      uri: "platform-http:/api"
      steps:
        - to: "activemq:queue:orders"
```

The `jetty` consumer becomes `platform-http`, with the listener port in the runtime’s server property. The `activemq` producer is in none of the rename tables, so it is kept and verified in the catalog for the selected Camel version and runtime.

### Karaf features to runtime dependencies

Karaf features

```xml
<features xmlns="http://karaf.apache.org/xmlns/features/v1.4.0">
  <feature name="my-camel-routes" version="1.0">
    <feature>camel-core</feature>
    <feature>camel-http4</feature>
    <feature>camel-jackson</feature>
    <bundle>mvn:com.example/my-routes/1.0</bundle>
  </feature>
</features>
```

Catalog-resolved dependencies

Spring Boot: org.apache.camel.springboot:camel-<component>-starter
Quarkus:     org.apache.camel.quarkus:camel-quarkus-<component>
Camel Main:  camel.jbang.dependencies in the module-root application.properties

The exact artifacts and versions are verified against the selected runtime catalog before `/camel-execute` writes them.

## After the migration

1.  Review the generated YAML routes and configuration.
    
2.  Update retained Java source from `javax.*` to `jakarta.*`: Camel 4 requires Jakarta EE 10.
    
3.  Run the routes locally with `camel run` or the target runtime’s development mode.
    
4.  Check the [Camel 4 migration guide](../../manual/camel-4-migration-guide.md) for breaking changes outside the migrated routes.
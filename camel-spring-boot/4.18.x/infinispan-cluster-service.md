# Infinispan Cluster Service

The Infinispan Cluster Service starter provides a cluster service implementation using [Infinispan](https://infinispan.org/) distributed cache for clustering in Camel Spring Boot applications.

## Maven Dependency

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-infinispan-cluster-service-starter</artifactId>
</dependency>
```

## Configuration Options

The following configuration options are available under the `camel.cluster.infinispan` prefix:

  
| Option | Default | Description |
| --- | --- | --- |
| enabled | true | Sets if the infinispan cluster service should be enabled or not. |
| id |  | Cluster Service ID. |
| hosts |  | Specifies the Infinispan server hosts. |
| order |  | Service lookup order/priority. |
| attributes |  | Custom service attributes. |

## Usage Example

Configure in `application.properties`:

```properties
camel.cluster.infinispan.enabled=true
camel.cluster.infinispan.hosts=localhost:11222
```
# camel-github-commit-source-kafka-connector source configuration

Connector Description: Receive commit From GitHub.

When using camel-github-commit-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-github-commit-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.githubcommitsource.CamelGithubcommitsourceSourceConnector
```

The camel-github-commit-source source connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.github-commit-source.repoName** | **Required** The GitHub Repository name. |  | HIGH |
| **camel.kamelet.github-commit-source.repoOwner** | **Required** The repository owner. |  | HIGH |
| **camel.kamelet.github-commit-source.oauthToken** | **Required** OAuth token. |  | HIGH |
| **camel.kamelet.github-commit-source.startingSha** | **Required** The SHA from which we want to consume, possible values beginning, last or a specific SHA. | "last" | HIGH |
| **camel.kamelet.github-commit-source.branch** | **Required** The branch we want to consume commit from. |  | HIGH |

The camel-github-commit-source source connector has no converters out of the box.

The camel-github-commit-source source connector has no transforms out of the box.

The camel-github-commit-source source connector has no aggregation strategies out of the box.
# camel-github-pullrequest-comment-source-kafka-connector source configuration

Connector Description: Receive pull request Comments From GitHub.

When using camel-github-pullrequest-comment-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-github-pullrequest-comment-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.githubpullrequestcommentsource.CamelGithubpullrequestcommentsourceSourceConnector
```

The camel-github-pullrequest-comment-source source connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.github-pullrequest-comment-source.repoName** | **Required** The GitHub Repository name. |  | HIGH |
| **camel.kamelet.github-pullrequest-comment-source.repoOwner** | **Required** The repository owner. |  | HIGH |
| **camel.kamelet.github-pullrequest-comment-source.oauthToken** | **Required** OAuth token. |  | HIGH |

The camel-github-pullrequest-comment-source source connector has no converters out of the box.

The camel-github-pullrequest-comment-source source connector has no transforms out of the box.

The camel-github-pullrequest-comment-source source connector has no aggregation strategies out of the box.
# OpenAI

OpenAI endpoint for chat completion, Responses API, embeddings, audio transcription, audio translation, and text-to-speech.

## What’s inside

-   [OpenAI component](../../../components/next/openai-component.md), URI syntax: `openai:operation`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-openai-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.component.openai.api-key | Default API key for all endpoints |  | String |
| camel.component.openai.audio-model | Default model for audio transcription endpoints |  | String |
| camel.component.openai.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.openai.base-url | Default base URL for all endpoints | [https://api.openai.com/v1](https://api.openai.com/v1) | String |
| camel.component.openai.bridge-error-handler | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| camel.component.openai.embedding-model | Default model for embeddings endpoints |  | String |
| camel.component.openai.enabled | Whether to enable auto configuration of the openai component. This is enabled by default. |  | Boolean |
| camel.component.openai.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.openai.model | Default model for chat completion endpoints |  | String |
| camel.component.openai.use-global-ssl-context-parameters | Enable usage of global SSL context parameters | false | Boolean |
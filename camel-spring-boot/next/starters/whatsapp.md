# WhatsApp

Send messages to WhatsApp.

## What’s inside

-   [WhatsApp component](../../../components/next/whatsapp-component.md), URI syntax: `whatsapp:phoneNumberId`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-whatsapp-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.component.whatsapp.api-version | WhatsApp Cloud API version | v13.0 | String |
| camel.component.whatsapp.authorization-token | Authorization Token taken from WhatsApp Meta for Developers Dashboard |  | String |
| camel.component.whatsapp.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.whatsapp.base-uri | Can be used to set an alternative base URI, e.g. when you want to test the component against a mock WhatsApp API | [https://graph.facebook.com](https://graph.facebook.com) | String |
| camel.component.whatsapp.client | Java 11 HttpClient implementation. The option is a java.net.http.HttpClient type. |  | HttpClient |
| camel.component.whatsapp.enabled | Whether to enable auto configuration of the whatsapp component. This is enabled by default. |  | Boolean |
| camel.component.whatsapp.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.whatsapp.phone-number-id | Phone Number ID taken from WhatsApp Meta for Developers Dashboard |  | String |
| camel.component.whatsapp.webhook-verify-token | Webhook verify token |  | String |
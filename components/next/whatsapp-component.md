# WhatsApp

**Since Camel 3.19**

**Only producer is supported**

The WhatsApp component provides access to the [WhatsApp Cloud API](https://developers.facebook.com/docs/whatsapp/cloud-api). It allows a Camel-based application to send messages using a cloud-hosted version of the WhatsApp Business Platform.

Before using this component, you have to set up Developer Assets and Platform Access, following the instructions at the [Register WhatsApp Business Cloud API account](https://developers.facebook.com/docs/whatsapp/cloud-api/get-started#set-up-developer-assets). Once the account is set up, you can navigate to [Meta for Developers Apps](https://developers.facebook.com/apps/?show_reminder=true), to access to the WhatsApp dashboard. There you can get the **authorization token**, **phone number id**, and you can add **recipient phone numbers**, these parameters are mandatory to use the component.=

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-whatsapp</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

whatsapp:type\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The WhatsApp component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **phoneNumberId** (producer) | **Required** Phone Number ID taken from WhatsApp Meta for Developers Dashboard. |  | String |
| **apiVersion** (advanced) | WhatsApp Cloud API version. | v13.0 | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **baseUri** (advanced) | Can be used to set an alternative base URI, e.g. when you want to test the component against a mock WhatsApp API. | [https://graph.facebook.com](https://graph.facebook.com) | String |
| **client** (advanced) | Java 11 HttpClient implementation. |  | HttpClient |
| **webhookVerifyToken** (advanced) | Webhook verify token. |  | String |
| **authorizationToken** (security) | **Required** Authorization Token taken from WhatsApp Meta for Developers Dashboard. |  | String |

## Endpoint Options

The WhatsApp endpoint is configured using URI syntax:

whatsapp:phoneNumberId

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **phoneNumberId** (producer) | **Required** The phone number ID taken from whatsapp-business dashboard. |  | String |

### Query Parameters (9 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiVersion** (advanced) | Facebook graph api version. |  | String |
| **baseUri** (advanced) | Can be used to set an alternative base URI, e.g. when you want to test the component against a mock WhatsApp API. |  | String |
| **httpClient** (advanced) | HttpClient implementation. |  | HttpClient |
| **webhookPath** (advanced) | Webhook path. | webhook | String |
| **whatsappService** (advanced) | WhatsApp service implementation. |  | WhatsAppService |
| **authorizationToken** (security) | **Required** The authorization access token taken from whatsapp-business dashboard. |  | String |
| **webhookSecret** (security) | The app secret used to verify the X-Hub-Signature-256 signature of inbound webhook event payloads (from the Meta/WhatsApp app dashboard). When set, event callbacks with a missing or invalid signature are rejected with HTTP 403; when not set, no signature verification is performed. |  | String |
| **webhookVerifyToken** (security) | Webhook verify token. |  | String |

## Message Headers

The WhatsApp component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelWhatsAppPhoneNumberId** (producer) Constant: [`WHATSAPP_PHONE_NUMBER_ID`](https://javadoc.io/doc/org.apache.camel/camel-whatsapp/latest/org/apache/camel/component/whatsapp/WhatsAppConstants.html#WHATSAPP_PHONE_NUMBER_ID) | Phone Number ID taken from WhatsApp Meta for Developers Dashboard. |  | Object |
| **CamelWhatsAppRecipientPhoneNumberId** (producer) Constant: [`WHATSAPP_RECIPIENT_PHONE_NUMBER_ID`](https://javadoc.io/doc/org.apache.camel/camel-whatsapp/latest/org/apache/camel/component/whatsapp/WhatsAppConstants.html#WHATSAPP_RECIPIENT_PHONE_NUMBER_ID) | Recipient phone number associated with Phone Number ID. |  | Object |

## Usage

The WhatsApp component supports only producer endpoints.

## Examples

### Producer Example

The following is a basic example of how to send a message to a WhatsApp chat through the Business Cloud API.

in Java DSL

_Java-only: inline Processor lambda with TextMessageRequest construction_

```java
from("direct:start")
	.process(exchange -> {
		 TextMessageRequest request = new TextMessageRequest();
		 request.setTo(insertYourRecipientPhoneNumberHere);
		 request.setText(new TextMessage());
		 request.getText().setBody("This is an auto-generated message from Camel \uD83D\uDC2B");

		 exchange.getIn().setBody(request);
	})
	.to("whatsapp:123456789:insertYourPhoneNumberIdHere?authorizationToken=123456789:insertYourAuthorizationTokenHere");
```

For more information you can refer to [Cloud API Reference](https://developers.facebook.com/docs/whatsapp/cloud-api/reference), Supported API are: [Messages](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/messages) and [Media](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/media)

### Webhook Mode

The WhatsApp component supports usage in the **webhook mode** using the **camel-webhook** component.

To enable webhook mode, users need first to add a REST implementation to their application. Maven users, for example, can add **netty-http** to their `pom.xml` file:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-netty-http</artifactId>
</dependency>
```

Once done, you need to prepend the webhook URI to the whatsapp URI you want to use.

In Java DSL:

_Java-only: uses fromF with string formatting_

```java
fromF("webhook:whatsapp:%s?authorizationToken=%s&webhookVerifyToken=%s", "<phoneNumberId>", "<AuthorizationToken>", "<webhookVerifyToken>").log("${body}")
```

You can follow the [set up webhooks guide](https://developers.facebook.com/docs/whatsapp/cloud-api/guides/set-up-webhooks) to enable and configure the webhook. The webhook component will expose an endpoint that can be used into the whatsapp administration console.

Refer to the [camel-webhook component](webhook-component.md) documentation for instructions on how to set it.
# AWS Comprehend

**Since Camel 4.18**

**Only producer is supported**

The AWS2 Comprehend component supports natural language processing (NLP) operations using [AWS Comprehend](https://aws.amazon.com/comprehend/). It provides capabilities such as:

-   Language detection
    
-   Entity recognition (people, places, organizations, dates, etc.)
    
-   Key phrase extraction
    
-   Sentiment analysis
    
-   Syntax analysis (part-of-speech tagging)
    
-   PII (Personally Identifiable Information) detection
    
-   Toxic content detection
    
-   Custom document classification
    

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Comprehend. More information is available at [Amazon Comprehend](https://aws.amazon.com/comprehend/).

## URI Format

aws2-comprehend://label\[?options\]

You can append query options to the URI in the following format:

`?options=value&option2=value&…​`

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

The AWS Comprehend component supports 24 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | Comprehend2Configuration |
| **endpointArn** (producer) | The Amazon Resource Name (ARN) of the endpoint to use for document classification. Required for classifyDocument operation. |  | String |
| **languageCode** (producer) | The language code of the input text. Required for all operations except detectDominantLanguage. Use a 2-letter ISO 639-1 code (e.g., 'en' for English, 'es' for Spanish). |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   detectDominantLanguage
    
-   detectEntities
    
-   detectKeyPhrases
    
-   detectSentiment
    
-   detectSyntax
    
-   detectPiiEntities
    
-   detectToxicContent
    
-   classifyDocument
    
-   containsPiiEntities
    





 | detectDominantLanguage | Comprehend2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the Comprehend client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   ap-south-2
    
-   ap-south-1
    
-   eu-south-1
    
-   eu-south-2
    
-   us-gov-east-1
    
-   me-central-1
    
-   il-central-1
    
-   ca-central-1
    
-   eu-central-1
    
-   us-iso-west-1
    
-   eu-central-2
    
-   eu-isoe-west-1
    
-   us-west-1
    
-   us-west-2
    
-   af-south-1
    
-   eu-north-1
    
-   eu-west-3
    
-   eu-west-2
    
-   eu-west-1
    
-   ap-northeast-3
    
-   ap-northeast-2
    
-   ap-northeast-1
    
-   me-south-1
    
-   sa-east-1
    
-   ap-east-1
    
-   cn-north-1
    
-   ca-west-1
    
-   us-gov-west-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   us-iso-east-1
    
-   ap-southeast-3
    
-   ap-southeast-4
    
-   us-east-1
    
-   us-east-2
    
-   cn-northwest-1
    
-   us-isob-east-1
    
-   aws-global
    
-   aws-cn-global
    
-   aws-us-gov-global
    
-   aws-iso-global
    
-   aws-iso-b-global
    





 |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **comprehendClient** (advanced) | **Autowired** To use an existing configured AWS Comprehend client. |  | ComprehendClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Comprehend client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Comprehend client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Comprehend client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Comprehend client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Comprehend client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Comprehend client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Comprehend. | false | boolean |

## Endpoint Options

The AWS Comprehend endpoint is configured using URI syntax:

aws2-comprehend:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (20 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpointArn** (producer) | The Amazon Resource Name (ARN) of the endpoint to use for document classification. Required for classifyDocument operation. |  | String |
| **languageCode** (producer) | The language code of the input text. Required for all operations except detectDominantLanguage. Use a 2-letter ISO 639-1 code (e.g., 'en' for English, 'es' for Spanish). |  | String |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   detectDominantLanguage
    
-   detectEntities
    
-   detectKeyPhrases
    
-   detectSentiment
    
-   detectSyntax
    
-   detectPiiEntities
    
-   detectToxicContent
    
-   classifyDocument
    
-   containsPiiEntities
    





 | detectDominantLanguage | Comprehend2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the Comprehend client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   ap-south-2
    
-   ap-south-1
    
-   eu-south-1
    
-   eu-south-2
    
-   us-gov-east-1
    
-   me-central-1
    
-   il-central-1
    
-   ca-central-1
    
-   eu-central-1
    
-   us-iso-west-1
    
-   eu-central-2
    
-   eu-isoe-west-1
    
-   us-west-1
    
-   us-west-2
    
-   af-south-1
    
-   eu-north-1
    
-   eu-west-3
    
-   eu-west-2
    
-   eu-west-1
    
-   ap-northeast-3
    
-   ap-northeast-2
    
-   ap-northeast-1
    
-   me-south-1
    
-   sa-east-1
    
-   ap-east-1
    
-   cn-north-1
    
-   ca-west-1
    
-   us-gov-west-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   us-iso-east-1
    
-   ap-southeast-3
    
-   ap-southeast-4
    
-   us-east-1
    
-   us-east-2
    
-   cn-northwest-1
    
-   us-isob-east-1
    
-   aws-global
    
-   aws-cn-global
    
-   aws-us-gov-global
    
-   aws-iso-global
    
-   aws-iso-b-global
    





 |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **comprehendClient** (advanced) | **Autowired** To use an existing configured AWS Comprehend client. |  | ComprehendClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Comprehend client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Comprehend client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Comprehend client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Comprehend client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Comprehend client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Comprehend client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Comprehend. | false | boolean |

## Message Headers

The AWS Comprehend component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsComprehendOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-comprehend/latest/org/apache/camel/component/aws2/comprehend/Comprehend2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsComprehendLanguageCode** (producer) Constant: [`LANGUAGE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-comprehend/latest/org/apache/camel/component/aws2/comprehend/Comprehend2Constants.html#LANGUAGE_CODE) | The language code of the input text. |  | String |
| **CamelAwsComprehendEndpointArn** (producer) Constant: [`ENDPOINT_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-comprehend/latest/org/apache/camel/component/aws2/comprehend/Comprehend2Constants.html#ENDPOINT_ARN) | The Amazon Resource Name (ARN) of the endpoint to use for document classification. |  | String |
| **CamelAwsComprehendDetectedLanguage** (producer) Constant: [`DETECTED_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-comprehend/latest/org/apache/camel/component/aws2/comprehend/Comprehend2Constants.html#DETECTED_LANGUAGE) | The detected dominant language. |  | String |
| **CamelAwsComprehendDetectedLanguageScore** (producer) Constant: [`DETECTED_LANGUAGE_SCORE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-comprehend/latest/org/apache/camel/component/aws2/comprehend/Comprehend2Constants.html#DETECTED_LANGUAGE_SCORE) | The detected dominant language score. |  | Float |
| **CamelAwsComprehendDetectedSentiment** (producer) Constant: [`DETECTED_SENTIMENT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-comprehend/latest/org/apache/camel/component/aws2/comprehend/Comprehend2Constants.html#DETECTED_SENTIMENT) | The detected sentiment. |  | String |
| **CamelAwsComprehendDetectedSentimentScore** (producer) Constant: [`DETECTED_SENTIMENT_SCORE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-comprehend/latest/org/apache/camel/component/aws2/comprehend/Comprehend2Constants.html#DETECTED_SENTIMENT_SCORE) | The detected sentiment scores. |  | SentimentScore |

Required Comprehend component options

You have to provide the amazonComprehendClient in the Registry or your accessKey and secretKey to access the [Amazon Comprehend](https://aws.amazon.com/comprehend/) service.

## Usage

### Static credentials, Default Credential Provider and Profile Credentials Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You have also the possibility of using Profile Credentials Provider, by specifying the useProfileCredentialsProvider option to true and profileCredentialsName to the profile name.

Only one of static, default and profile credentials could be used at the same time.

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Comprehend Producer operations

Camel-AWS Comprehend component provides the following operations on the producer side:

 
| Operation | Description |
| --- | --- |
| `detectDominantLanguage` | Detects the dominant language of the input text. Returns language codes with confidence scores. |
| `detectEntities` | Identifies entities in the text such as persons, locations, organizations, dates, quantities, and more. |
| `detectKeyPhrases` | Extracts key phrases (noun phrases) that represent the main points in the text. |
| `detectSentiment` | Analyzes the sentiment of the text and returns POSITIVE, NEGATIVE, NEUTRAL, or MIXED with confidence scores. |
| `detectSyntax` | Performs syntactic analysis, providing part-of-speech tags for each word in the text. |
| `detectPiiEntities` | Detects personally identifiable information (PII) such as emails, phone numbers, SSN, credit cards, etc. |
| `detectToxicContent` | Analyzes text for toxic content including profanity, hate speech, threats, and more. |
| `classifyDocument` | Classifies a document using a custom classification model (requires a trained endpoint). |
| `containsPiiEntities` | Checks if the text contains PII and returns labels indicating the types of PII found. |

### Language Code Requirement

Most operations (except `detectDominantLanguage`) require a language code to be specified. You can set it:

-   As an endpoint option: `languageCode=en`
    
-   As a message header: `CamelAwsComprehendLanguageCode`
    

Common language codes: `en` (English), `es` (Spanish), `fr` (French), `de` (German), `it` (Italian), `pt` (Portuguese), `ja` (Japanese), `ko` (Korean), `zh` (Chinese), `ar` (Arabic).

## Examples

### Detect Dominant Language

Automatically detect the language of the input text:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:detectLanguage")
    .setBody(constant("This is a sample text written in English."))
    .to("aws2-comprehend://test?operation=detectDominantLanguage&useDefaultCredentialsProvider=true&region=us-east-1")
    .log("Detected language: ${header.CamelAwsComprehendDetectedLanguage}");
```

```xml
<route>
  <from uri="direct:detectLanguage"/>
  <setBody>
    <constant>This is a sample text written in English.</constant>
  </setBody>
  <to uri="aws2-comprehend://test?operation=detectDominantLanguage&amp;useDefaultCredentialsProvider=true&amp;region=us-east-1"/>
  <log message="Detected language: ${header.CamelAwsComprehendDetectedLanguage}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:detectLanguage
      steps:
        - setBody:
            constant: "This is a sample text written in English."
        - to:
            uri: aws2-comprehend://test
            parameters:
              operation: detectDominantLanguage
              useDefaultCredentialsProvider: true
              region: us-east-1
        - log:
            message: "Detected language: ${header.CamelAwsComprehendDetectedLanguage}"
```

The result body will contain a list of `DominantLanguage` objects with language codes and confidence scores. The detected language code and score are also set as message headers.

### Detect Entities

Extract named entities from text:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:detectEntities")
    .setBody(constant("Amazon was founded by Jeff Bezos in Seattle, Washington in 1994."))
    .to("aws2-comprehend://test?operation=detectEntities&languageCode=en&useDefaultCredentialsProvider=true&region=us-east-1")
    .log("Found ${body.size()} entities")
    .split(body())
        .log("Entity: ${body.text} - Type: ${body.type} - Score: ${body.score}");
```

```xml
<route>
  <from uri="direct:detectEntities"/>
  <setBody>
    <constant>Amazon was founded by Jeff Bezos in Seattle, Washington in 1994.</constant>
  </setBody>
  <to uri="aws2-comprehend://test?operation=detectEntities&amp;languageCode=en&amp;useDefaultCredentialsProvider=true&amp;region=us-east-1"/>
  <log message="Found ${body.size()} entities"/>
  <split>
    <simple>${body}</simple>
    <log message="Entity: ${body.text} - Type: ${body.type} - Score: ${body.score}"/>
  </split>
</route>
```

```yaml
- route:
    from:
      uri: direct:detectEntities
      steps:
        - setBody:
            constant: "Amazon was founded by Jeff Bezos in Seattle, Washington in 1994."
        - to:
            uri: aws2-comprehend://test
            parameters:
              operation: detectEntities
              languageCode: en
              useDefaultCredentialsProvider: true
              region: us-east-1
        - log:
            message: "Found ${body.size()} entities"
        - split:
            simple: "${body}"
            steps:
              - log:
                  message: "Entity: ${body.text} - Type: ${body.type} - Score: ${body.score}"
```

This will detect entities like: \* Jeff Bezos (PERSON) \* Amazon (ORGANIZATION) \* Seattle (LOCATION) \* Washington (LOCATION) \* 1994 (DATE)

### Detect Sentiment

Analyze the sentiment of text:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:analyzeSentiment")
    .setBody(constant("I love this product! It works perfectly and exceeded my expectations."))
    .to("aws2-comprehend://test?operation=detectSentiment&languageCode=en&useDefaultCredentialsProvider=true&region=us-east-1")
    .log("Sentiment: ${header.CamelAwsComprehendDetectedSentiment}")
    .log("Sentiment scores: ${header.CamelAwsComprehendDetectedSentimentScore}");
```

```xml
<route>
  <from uri="direct:analyzeSentiment"/>
  <setBody>
    <constant>I love this product! It works perfectly and exceeded my expectations.</constant>
  </setBody>
  <to uri="aws2-comprehend://test?operation=detectSentiment&amp;languageCode=en&amp;useDefaultCredentialsProvider=true&amp;region=us-east-1"/>
  <log message="Sentiment: ${header.CamelAwsComprehendDetectedSentiment}"/>
  <log message="Sentiment scores: ${header.CamelAwsComprehendDetectedSentimentScore}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:analyzeSentiment
      steps:
        - setBody:
            constant: "I love this product! It works perfectly and exceeded my expectations."
        - to:
            uri: aws2-comprehend://test
            parameters:
              operation: detectSentiment
              languageCode: en
              useDefaultCredentialsProvider: true
              region: us-east-1
        - log:
            message: "Sentiment: ${header.CamelAwsComprehendDetectedSentiment}"
        - log:
            message: "Sentiment scores: ${header.CamelAwsComprehendDetectedSentimentScore}"
```

The sentiment will be one of: POSITIVE, NEGATIVE, NEUTRAL, or MIXED.

### Detect Key Phrases

Extract key phrases from text:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:detectKeyPhrases")
    .setBody(constant("Apache Camel is an open source integration framework that provides rule-based routing and mediation."))
    .to("aws2-comprehend://test?operation=detectKeyPhrases&languageCode=en&useDefaultCredentialsProvider=true&region=us-east-1")
    .split(body())
        .log("Key phrase: ${body.text} (score: ${body.score})");
```

```xml
<route>
  <from uri="direct:detectKeyPhrases"/>
  <setBody>
    <constant>Apache Camel is an open source integration framework that provides rule-based routing and mediation.</constant>
  </setBody>
  <to uri="aws2-comprehend://test?operation=detectKeyPhrases&amp;languageCode=en&amp;useDefaultCredentialsProvider=true&amp;region=us-east-1"/>
  <split>
    <simple>${body}</simple>
    <log message="Key phrase: ${body.text} (score: ${body.score})"/>
  </split>
</route>
```

```yaml
- route:
    from:
      uri: direct:detectKeyPhrases
      steps:
        - setBody:
            constant: "Apache Camel is an open source integration framework that provides rule-based routing and mediation."
        - to:
            uri: aws2-comprehend://test
            parameters:
              operation: detectKeyPhrases
              languageCode: en
              useDefaultCredentialsProvider: true
              region: us-east-1
        - split:
            simple: "${body}"
            steps:
              - log:
                  message: "Key phrase: ${body.text} (score: ${body.score})"
```

### Detect PII Entities

Identify personally identifiable information in text:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:detectPii")
    .setBody(constant("Contact John at john.doe@example.com or call 555-123-4567. His SSN is 123-45-6789."))
    .to("aws2-comprehend://test?operation=detectPiiEntities&languageCode=en&useDefaultCredentialsProvider=true&region=us-east-1")
    .split(body())
        .log("PII found: ${body.type} at position ${body.beginOffset}-${body.endOffset}");
```

```xml
<route>
  <from uri="direct:detectPii"/>
  <setBody>
    <constant>Contact John at john.doe@example.com or call 555-123-4567. His SSN is 123-45-6789.</constant>
  </setBody>
  <to uri="aws2-comprehend://test?operation=detectPiiEntities&amp;languageCode=en&amp;useDefaultCredentialsProvider=true&amp;region=us-east-1"/>
  <split>
    <simple>${body}</simple>
    <log message="PII found: ${body.type} at position ${body.beginOffset}-${body.endOffset}"/>
  </split>
</route>
```

```yaml
- route:
    from:
      uri: direct:detectPii
      steps:
        - setBody:
            constant: "Contact John at john.doe@example.com or call 555-123-4567. His SSN is 123-45-6789."
        - to:
            uri: aws2-comprehend://test
            parameters:
              operation: detectPiiEntities
              languageCode: en
              useDefaultCredentialsProvider: true
              region: us-east-1
        - split:
            simple: "${body}"
            steps:
              - log:
                  message: "PII found: ${body.type} at position ${body.beginOffset}-${body.endOffset}"
```

This detects PII types such as EMAIL, PHONE, SSN, CREDIT\_DEBIT\_NUMBER, etc.

### Detect Syntax (Part-of-Speech Tagging)

Analyze the grammatical structure of text:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:detectSyntax")
    .setBody(constant("The quick brown fox jumps over the lazy dog."))
    .to("aws2-comprehend://test?operation=detectSyntax&languageCode=en&useDefaultCredentialsProvider=true&region=us-east-1")
    .split(body())
        .log("Token: ${body.text} - POS: ${body.partOfSpeech.tag}");
```

```xml
<route>
  <from uri="direct:detectSyntax"/>
  <setBody>
    <constant>The quick brown fox jumps over the lazy dog.</constant>
  </setBody>
  <to uri="aws2-comprehend://test?operation=detectSyntax&amp;languageCode=en&amp;useDefaultCredentialsProvider=true&amp;region=us-east-1"/>
  <split>
    <simple>${body}</simple>
    <log message="Token: ${body.text} - POS: ${body.partOfSpeech.tag}"/>
  </split>
</route>
```

```yaml
- route:
    from:
      uri: direct:detectSyntax
      steps:
        - setBody:
            constant: "The quick brown fox jumps over the lazy dog."
        - to:
            uri: aws2-comprehend://test
            parameters:
              operation: detectSyntax
              languageCode: en
              useDefaultCredentialsProvider: true
              region: us-east-1
        - split:
            simple: "${body}"
            steps:
              - log:
                  message: "Token: ${body.text} - POS: ${body.partOfSpeech.tag}"
```

Returns part-of-speech tags like NOUN, VERB, ADJ (adjective), DET (determiner), etc.

### Detect Toxic Content

Analyze text for toxic content:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:detectToxic")
    .setBody(constant("This is a friendly and polite message."))
    .to("aws2-comprehend://test?operation=detectToxicContent&languageCode=en&useDefaultCredentialsProvider=true&region=us-east-1")
    .log("Toxicity analysis: ${body}");
```

```xml
<route>
  <from uri="direct:detectToxic"/>
  <setBody>
    <constant>This is a friendly and polite message.</constant>
  </setBody>
  <to uri="aws2-comprehend://test?operation=detectToxicContent&amp;languageCode=en&amp;useDefaultCredentialsProvider=true&amp;region=us-east-1"/>
  <log message="Toxicity analysis: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:detectToxic
      steps:
        - setBody:
            constant: "This is a friendly and polite message."
        - to:
            uri: aws2-comprehend://test
            parameters:
              operation: detectToxicContent
              languageCode: en
              useDefaultCredentialsProvider: true
              region: us-east-1
        - log:
            message: "Toxicity analysis: ${body}"
```

Returns toxicity scores for categories like PROFANITY, HATE\_SPEECH, THREAT, INSULT, etc.

### Using a POJO as body

For more control, you can pass AWS SDK request objects directly by setting `pojoRequest=true`:

_Java-only: uses lambda expression and AWS SDK request builder API_

```java
from("direct:pojoRequest")
    .setBody(exchange -> DetectSentimentRequest.builder()
            .text("I am very happy with this service!")
            .languageCode("en")
            .build())
    .to("aws2-comprehend://test?operation=detectSentiment&pojoRequest=true&useDefaultCredentialsProvider=true&region=us-east-1")
    .log("Sentiment: ${header.CamelAwsComprehendDetectedSentiment}");
```

### Setting Operation and Language via Headers

You can dynamically set the operation and language code using message headers:

_Java-only: uses Java enum constant for operation header value_

```java
from("direct:dynamicOperation")
    .setHeader("CamelAwsComprehendOperation", constant(Comprehend2Operations.detectEntities))
    .setHeader("CamelAwsComprehendLanguageCode", constant("en"))
    .setBody(constant("Apple Inc. is headquartered in Cupertino, California."))
    .to("aws2-comprehend://test?useDefaultCredentialsProvider=true&region=us-east-1")
    .log("Detected entities: ${body}");
```

### Using with Static Credentials

If you need to use explicit credentials:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:withCredentials")
    .setBody(constant("Bonjour, comment allez-vous?"))
    .to("aws2-comprehend://test?operation=detectDominantLanguage&accessKey=YOUR_ACCESS_KEY&secretKey=YOUR_SECRET_KEY&region=eu-west-1")
    .log("Detected language: ${header.CamelAwsComprehendDetectedLanguage}");
```

```xml
<route>
  <from uri="direct:withCredentials"/>
  <setBody>
    <constant>Bonjour, comment allez-vous?</constant>
  </setBody>
  <to uri="aws2-comprehend://test?operation=detectDominantLanguage&amp;accessKey=YOUR_ACCESS_KEY&amp;secretKey=YOUR_SECRET_KEY&amp;region=eu-west-1"/>
  <log message="Detected language: ${header.CamelAwsComprehendDetectedLanguage}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:withCredentials
      steps:
        - setBody:
            constant: "Bonjour, comment allez-vous?"
        - to:
            uri: aws2-comprehend://test
            parameters:
              operation: detectDominantLanguage
              accessKey: YOUR_ACCESS_KEY
              secretKey: YOUR_SECRET_KEY
              region: eu-west-1
        - log:
            message: "Detected language: ${header.CamelAwsComprehendDetectedLanguage}"
```

### Content Moderation Pipeline Example

A practical example combining multiple Comprehend operations for content moderation:

_Java-only: uses choice/when/otherwise with inline comments_

```java
from("direct:moderateContent")
    .setHeader("originalText", simple("${body}"))
    // First, detect the language
    .to("aws2-comprehend://test?operation=detectDominantLanguage&useDefaultCredentialsProvider=true&region=us-east-1")
    .setHeader("detectedLanguage", simple("${header.CamelAwsComprehendDetectedLanguage}"))
    .log("Language detected: ${header.detectedLanguage}")
    // Restore original text and check for toxic content
    .setBody(simple("${header.originalText}"))
    .setHeader("CamelAwsComprehendLanguageCode", simple("${header.detectedLanguage}"))
    .to("aws2-comprehend://test?operation=detectToxicContent&useDefaultCredentialsProvider=true&region=us-east-1")
    .choice()
        .when(simple("${body[0].toxicity} > 0.5"))
            .log("WARNING: High toxicity detected!")
            .to("direct:flagContent")
        .otherwise()
            .log("Content is safe")
            .to("direct:approveContent");
```

### Customer Feedback Analysis Example

Analyze customer feedback for sentiment and key topics:

_Java-only: uses body() method reference and choice/when/otherwise with inline comments_

```java
from("kafka:customer-feedback")
    .log("Processing feedback: ${body}")
    // Analyze sentiment
    .to("aws2-comprehend://test?operation=detectSentiment&languageCode=en&useDefaultCredentialsProvider=true&region=us-east-1")
    .setHeader("sentiment", simple("${header.CamelAwsComprehendDetectedSentiment}"))
    // Extract key phrases
    .to("aws2-comprehend://test?operation=detectKeyPhrases&languageCode=en&useDefaultCredentialsProvider=true&region=us-east-1")
    .setHeader("keyPhrases", body())
    .log("Sentiment: ${header.sentiment}, Key topics: ${header.keyPhrases}")
    // Route based on sentiment
    .choice()
        .when(simple("${header.sentiment} == 'NEGATIVE'"))
            .to("direct:handleNegativeFeedback")
        .when(simple("${header.sentiment} == 'POSITIVE'"))
            .to("direct:handlePositiveFeedback")
        .otherwise()
            .to("direct:handleNeutralFeedback");
```

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-comprehend</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-comprehend with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-comprehend-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 25 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-comprehend.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-comprehend.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-comprehend.comprehend-client** | To use an existing configured AWS Comprehend client. The option is a software.amazon.awssdk.services.comprehend.ComprehendClient type. |  | ComprehendClient |
| **camel.component.aws2-comprehend.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.comprehend.Comprehend2Configuration type. |  | Comprehend2Configuration |
| **camel.component.aws2-comprehend.enabled** | Whether to enable auto configuration of the aws2-comprehend component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-comprehend.endpoint-arn** | The Amazon Resource Name (ARN) of the endpoint to use for document classification. Required for classifyDocument operation. |  | String |
| **camel.component.aws2-comprehend.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws2-comprehend.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws2-comprehend.language-code** | The language code of the input text. Required for all operations except detectDominantLanguage. Use a 2-letter ISO 639-1 code (e.g., 'en' for English, 'es' for Spanish). |  | String |
| **camel.component.aws2-comprehend.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-comprehend.operation** | The operation to perform. | detectdominantlanguage | Comprehend2Operations |
| **camel.component.aws2-comprehend.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-comprehend.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-comprehend.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **camel.component.aws2-comprehend.proxy-host** | To define a proxy host when instantiating the Comprehend client. |  | String |
| **camel.component.aws2-comprehend.proxy-port** | To define a proxy port when instantiating the Comprehend client. |  | Integer |
| **camel.component.aws2-comprehend.proxy-protocol** | To define a proxy protocol when instantiating the Comprehend client. | https | Protocol |
| **camel.component.aws2-comprehend.region** | The region in which the Comprehend client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-comprehend.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-comprehend.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws2-comprehend.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-comprehend.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-comprehend.use-default-credentials-provider** | Set whether the Comprehend client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-comprehend.use-profile-credentials-provider** | Set whether the Comprehend client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-comprehend.use-session-credentials** | Set whether the Comprehend client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Comprehend. | false | Boolean |
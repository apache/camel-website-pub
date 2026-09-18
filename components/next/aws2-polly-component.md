# AWS Polly

**Since Camel 4.18**

**Only producer is supported**

The AWS2 Polly component supports text-to-speech synthesis using the AWS Polly service. [AWS Polly](https://aws.amazon.com/polly/) is a cloud service that converts text into lifelike speech.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Polly. More information is available at [Amazon Polly](https://aws.amazon.com/polly/).

## URI Format

aws2-polly://label\[?options\]

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

The AWS Polly component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | Polly2Configuration |
| **engine** (producer) | 
The engine to use for synthesis (standard, neural, long-form, generative).

Enum values:

-   standard
    
-   neural
    
-   long-form
    
-   generative
    
-   null
    





 |  | Engine |
| **languageCode** (producer) | The language code for the synthesis. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **lexiconContent** (producer) | The content of the lexicon in PLS format for putLexicon operation. |  | String |
| **lexiconName** (producer) | The name of the lexicon to use for getLexicon, putLexicon, or deleteLexicon operations. |  | String |
| **lexiconNames** (producer) | Lexicon names to apply during synthesis. |  | String |
| **operation** (producer) | 

**Required** The operation to perform.

Enum values:

-   synthesizeSpeech
    
-   describeVoices
    
-   listLexicons
    
-   getLexicon
    
-   putLexicon
    
-   deleteLexicon
    
-   startSpeechSynthesisTask
    
-   getSpeechSynthesisTask
    
-   listSpeechSynthesisTasks
    





 | synthesizeSpeech | Polly2Operations |
| **outputFormat** (producer) | 

The audio output format.

Enum values:

-   json
    
-   mp3
    
-   ogg\_opus
    
-   ogg\_vorbis
    
-   pcm
    
-   mulaw
    
-   alaw
    
-   null
    





 | MP3 | OutputFormat |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the Polly client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **s3Bucket** (producer) | The S3 bucket name for startSpeechSynthesisTask operation output. |  | String |
| **s3KeyPrefix** (producer) | The S3 key prefix for startSpeechSynthesisTask operation output. |  | String |
| **sampleRate** (producer) | The sample rate in Hz for the audio output. |  | String |
| **snsTopicArn** (producer) | The SNS topic ARN for startSpeechSynthesisTask notifications. |  | String |
| **taskId** (producer) | The task ID for getSpeechSynthesisTask operation. |  | String |
| **textType** (producer) | 

The type of text input (text or ssml).

Enum values:

-   ssml
    
-   text
    
-   null
    





 | TEXT | TextType |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **voiceId** (producer) | 

The voice ID to use for synthesis.

Enum values:

-   Aditi
    
-   Amy
    
-   Astrid
    
-   Bianca
    
-   Brian
    
-   Camila
    
-   Carla
    
-   Carmen
    
-   Celine
    
-   Chantal
    
-   Conchita
    
-   Cristiano
    
-   Dora
    
-   Emma
    
-   Enrique
    
-   Ewa
    
-   Filiz
    
-   Gabrielle
    
-   Geraint
    
-   Giorgio
    
-   Gwyneth
    
-   Hans
    
-   Ines
    
-   Ivy
    
-   Jacek
    
-   Jan
    
-   Joanna
    
-   Joey
    
-   Justin
    
-   Karl
    
-   Kendra
    
-   Kevin
    
-   Kimberly
    
-   Lea
    
-   Liv
    
-   Lotte
    
-   Lucia
    
-   Lupe
    
-   Mads
    
-   Maja
    
-   Marlene
    
-   Mathieu
    
-   Matthew
    
-   Maxim
    
-   Mia
    
-   Miguel
    
-   Mizuki
    
-   Naja
    
-   Nicole
    
-   Olivia
    
-   Penelope
    
-   Raveena
    
-   Ricardo
    
-   Ruben
    
-   Russell
    
-   Salli
    
-   Seoyeon
    
-   Takumi
    
-   Tatyana
    
-   Vicki
    
-   Vitoria
    
-   Zeina
    
-   Zhiyu
    
-   Aria
    
-   Ayanda
    
-   Arlet
    
-   Hannah
    
-   Arthur
    
-   Daniel
    
-   Liam
    
-   Pedro
    
-   Kajal
    
-   Hiujin
    
-   Laura
    
-   Elin
    
-   Ida
    
-   Suvi
    
-   Ola
    
-   Hala
    
-   Andres
    
-   Sergio
    
-   Remi
    
-   Adriano
    
-   Thiago
    
-   Ruth
    
-   Stephen
    
-   Kazuha
    
-   Tomoko
    
-   Niamh
    
-   Sofie
    
-   Lisa
    
-   Isabelle
    
-   Zayd
    
-   Danielle
    
-   Gregory
    
-   Burcu
    
-   Jitka
    
-   Sabrina
    
-   Jasmine
    
-   Jihye
    
-   Ambre
    
-   Beatrice
    
-   Florian
    
-   Lennart
    
-   Lorenzo
    
-   Tiffany
    
-   null
    





 |  | VoiceId |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **pollyClient** (advanced) | **Autowired** To use an existing configured AWS Polly client. |  | PollyClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Polly client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Polly client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Polly client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Polly client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Polly client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Polly client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Polly. | false | boolean |

## Endpoint Options

The AWS Polly endpoint is configured using URI syntax:

aws2-polly:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **engine** (producer) | 
The engine to use for synthesis (standard, neural, long-form, generative).

Enum values:

-   standard
    
-   neural
    
-   long-form
    
-   generative
    
-   null
    





 |  | Engine |
| **languageCode** (producer) | The language code for the synthesis. |  | String |
| **lexiconContent** (producer) | The content of the lexicon in PLS format for putLexicon operation. |  | String |
| **lexiconName** (producer) | The name of the lexicon to use for getLexicon, putLexicon, or deleteLexicon operations. |  | String |
| **lexiconNames** (producer) | Lexicon names to apply during synthesis. |  | String |
| **operation** (producer) | 

**Required** The operation to perform.

Enum values:

-   synthesizeSpeech
    
-   describeVoices
    
-   listLexicons
    
-   getLexicon
    
-   putLexicon
    
-   deleteLexicon
    
-   startSpeechSynthesisTask
    
-   getSpeechSynthesisTask
    
-   listSpeechSynthesisTasks
    





 | synthesizeSpeech | Polly2Operations |
| **outputFormat** (producer) | 

The audio output format.

Enum values:

-   json
    
-   mp3
    
-   ogg\_opus
    
-   ogg\_vorbis
    
-   pcm
    
-   mulaw
    
-   alaw
    
-   null
    





 | MP3 | OutputFormat |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the Polly client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **s3Bucket** (producer) | The S3 bucket name for startSpeechSynthesisTask operation output. |  | String |
| **s3KeyPrefix** (producer) | The S3 key prefix for startSpeechSynthesisTask operation output. |  | String |
| **sampleRate** (producer) | The sample rate in Hz for the audio output. |  | String |
| **snsTopicArn** (producer) | The SNS topic ARN for startSpeechSynthesisTask notifications. |  | String |
| **taskId** (producer) | The task ID for getSpeechSynthesisTask operation. |  | String |
| **textType** (producer) | 

The type of text input (text or ssml).

Enum values:

-   ssml
    
-   text
    
-   null
    





 | TEXT | TextType |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **voiceId** (producer) | 

The voice ID to use for synthesis.

Enum values:

-   Aditi
    
-   Amy
    
-   Astrid
    
-   Bianca
    
-   Brian
    
-   Camila
    
-   Carla
    
-   Carmen
    
-   Celine
    
-   Chantal
    
-   Conchita
    
-   Cristiano
    
-   Dora
    
-   Emma
    
-   Enrique
    
-   Ewa
    
-   Filiz
    
-   Gabrielle
    
-   Geraint
    
-   Giorgio
    
-   Gwyneth
    
-   Hans
    
-   Ines
    
-   Ivy
    
-   Jacek
    
-   Jan
    
-   Joanna
    
-   Joey
    
-   Justin
    
-   Karl
    
-   Kendra
    
-   Kevin
    
-   Kimberly
    
-   Lea
    
-   Liv
    
-   Lotte
    
-   Lucia
    
-   Lupe
    
-   Mads
    
-   Maja
    
-   Marlene
    
-   Mathieu
    
-   Matthew
    
-   Maxim
    
-   Mia
    
-   Miguel
    
-   Mizuki
    
-   Naja
    
-   Nicole
    
-   Olivia
    
-   Penelope
    
-   Raveena
    
-   Ricardo
    
-   Ruben
    
-   Russell
    
-   Salli
    
-   Seoyeon
    
-   Takumi
    
-   Tatyana
    
-   Vicki
    
-   Vitoria
    
-   Zeina
    
-   Zhiyu
    
-   Aria
    
-   Ayanda
    
-   Arlet
    
-   Hannah
    
-   Arthur
    
-   Daniel
    
-   Liam
    
-   Pedro
    
-   Kajal
    
-   Hiujin
    
-   Laura
    
-   Elin
    
-   Ida
    
-   Suvi
    
-   Ola
    
-   Hala
    
-   Andres
    
-   Sergio
    
-   Remi
    
-   Adriano
    
-   Thiago
    
-   Ruth
    
-   Stephen
    
-   Kazuha
    
-   Tomoko
    
-   Niamh
    
-   Sofie
    
-   Lisa
    
-   Isabelle
    
-   Zayd
    
-   Danielle
    
-   Gregory
    
-   Burcu
    
-   Jitka
    
-   Sabrina
    
-   Jasmine
    
-   Jihye
    
-   Ambre
    
-   Beatrice
    
-   Florian
    
-   Lennart
    
-   Lorenzo
    
-   Tiffany
    
-   null
    





 |  | VoiceId |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **pollyClient** (advanced) | **Autowired** To use an existing configured AWS Polly client. |  | PollyClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Polly client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Polly client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Polly client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Polly client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Polly client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Polly client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Polly. | false | boolean |

## Message Headers

The AWS Polly component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsPollyOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsPollyVoiceId** (producer) Constant: [`VOICE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#VOICE_ID) | 
The voice ID to use for synthesis.

Enum values:

-   Aditi
    
-   Amy
    
-   Astrid
    
-   Bianca
    
-   Brian
    
-   Camila
    
-   Carla
    
-   Carmen
    
-   Celine
    
-   Chantal
    
-   Conchita
    
-   Cristiano
    
-   Dora
    
-   Emma
    
-   Enrique
    
-   Ewa
    
-   Filiz
    
-   Gabrielle
    
-   Geraint
    
-   Giorgio
    
-   Gwyneth
    
-   Hans
    
-   Ines
    
-   Ivy
    
-   Jacek
    
-   Jan
    
-   Joanna
    
-   Joey
    
-   Justin
    
-   Karl
    
-   Kendra
    
-   Kevin
    
-   Kimberly
    
-   Lea
    
-   Liv
    
-   Lotte
    
-   Lucia
    
-   Lupe
    
-   Mads
    
-   Maja
    
-   Marlene
    
-   Mathieu
    
-   Matthew
    
-   Maxim
    
-   Mia
    
-   Miguel
    
-   Mizuki
    
-   Naja
    
-   Nicole
    
-   Olivia
    
-   Penelope
    
-   Raveena
    
-   Ricardo
    
-   Ruben
    
-   Russell
    
-   Salli
    
-   Seoyeon
    
-   Takumi
    
-   Tatyana
    
-   Vicki
    
-   Vitoria
    
-   Zeina
    
-   Zhiyu
    
-   Aria
    
-   Ayanda
    
-   Arlet
    
-   Hannah
    
-   Arthur
    
-   Daniel
    
-   Liam
    
-   Pedro
    
-   Kajal
    
-   Hiujin
    
-   Laura
    
-   Elin
    
-   Ida
    
-   Suvi
    
-   Ola
    
-   Hala
    
-   Andres
    
-   Sergio
    
-   Remi
    
-   Adriano
    
-   Thiago
    
-   Ruth
    
-   Stephen
    
-   Kazuha
    
-   Tomoko
    
-   Niamh
    
-   Sofie
    
-   Lisa
    
-   Isabelle
    
-   Zayd
    
-   Danielle
    
-   Gregory
    
-   Burcu
    
-   Jitka
    
-   Sabrina
    
-   Jasmine
    
-   Jihye
    
-   Ambre
    
-   Beatrice
    
-   Florian
    
-   Lennart
    
-   Lorenzo
    
-   Tiffany
    
-   null
    





 |  | VoiceId |
| **CamelAwsPollyOutputFormat** (producer) Constant: [`OUTPUT_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#OUTPUT_FORMAT) | 

The output format for the audio stream.

Enum values:

-   json
    
-   mp3
    
-   ogg\_opus
    
-   ogg\_vorbis
    
-   pcm
    
-   mulaw
    
-   alaw
    
-   null
    





 |  | OutputFormat |
| **CamelAwsPollyTextType** (producer) Constant: [`TEXT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#TEXT_TYPE) | 

The type of text input (text or ssml).

Enum values:

-   ssml
    
-   text
    
-   null
    





 |  | TextType |
| **CamelAwsPollySampleRate** (producer) Constant: [`SAMPLE_RATE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#SAMPLE_RATE) | The sample rate in Hz. |  | String |
| **CamelAwsPollyEngine** (producer) Constant: [`ENGINE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#ENGINE) | 

The engine to use (standard, neural, long-form, generative).

Enum values:

-   standard
    
-   neural
    
-   long-form
    
-   generative
    
-   null
    





 |  | Engine |
| **CamelAwsPollyLanguageCode** (producer) Constant: [`LANGUAGE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#LANGUAGE_CODE) | The language code. |  | String |
| **CamelAwsPollyLexiconNames** (producer) Constant: [`LEXICON_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#LEXICON_NAMES) | Comma-separated list of lexicon names. |  | String |
| **CamelAwsPollyLexiconName** (producer) Constant: [`LEXICON_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#LEXICON_NAME) | The name of the lexicon. |  | String |
| **CamelAwsPollyLexiconContent** (producer) Constant: [`LEXICON_CONTENT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#LEXICON_CONTENT) | The content of the lexicon in PLS format. |  | String |
| **CamelAwsPollyTaskId** (producer) Constant: [`TASK_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#TASK_ID) | The task ID for speech synthesis task. |  | String |
| **CamelAwsPollyS3Bucket** (producer) Constant: [`S3_BUCKET`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#S3_BUCKET) | The S3 bucket name for output. |  | String |
| **CamelAwsPollyS3KeyPrefix** (producer) Constant: [`S3_KEY_PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#S3_KEY_PREFIX) | The S3 key prefix for output. |  | String |
| **CamelAwsPollySnsTopicArn** (producer) Constant: [`SNS_TOPIC_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#SNS_TOPIC_ARN) | The SNS topic ARN for notifications. |  | String |
| **CamelAwsPollyContentType** (producer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#CONTENT_TYPE) | The content type of the audio stream. |  | String |
| **CamelAwsPollyRequestCharacters** (producer) Constant: [`REQUEST_CHARACTERS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-polly/latest/org/apache/camel/component/aws2/polly/Polly2Constants.html#REQUEST_CHARACTERS) | Number of characters synthesized. |  | Integer |

Required Polly component options

You have to provide the amazonPollyClient in the Registry or your accessKey and secretKey to access the [Amazon Polly](https://aws.amazon.com/polly/) service.

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

### Polly Producer operations

Camel-AWS Polly component provides the following operations on the producer side:

-   synthesizeSpeech
    
-   describeVoices
    
-   listLexicons
    
-   getLexicon
    
-   putLexicon
    
-   deleteLexicon
    
-   startSpeechSynthesisTask
    
-   getSpeechSynthesisTask
    
-   listSpeechSynthesisTasks
    

## Examples

### Synthesize Speech example

_Java-only: uses AWS SDK enum constants for header values_

```java
from("direct:start")
  .setHeader(Polly2Constants.VOICE_ID, constant(VoiceId.JOANNA))
  .setBody(constant("Hello, this is a test of Amazon Polly text to speech synthesis."))
  .to("aws2-polly://test?operation=synthesizeSpeech")
  .to("file:output?fileName=speech.mp3");
```

As a result, you’ll get an exchange containing the audio stream (InputStream) with the synthesized speech.

### Using Neural Voices

_Java-only: uses AWS SDK enum constants for header values_

```java
from("direct:start")
  .setHeader(Polly2Constants.VOICE_ID, constant(VoiceId.MATTHEW))
  .setHeader(Polly2Constants.ENGINE, constant(Engine.NEURAL))
  .setBody(constant("This is synthesized using a neural voice."))
  .to("aws2-polly://test?operation=synthesizeSpeech&outputFormat=MP3");
```

### Describe Voices example

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("aws2-polly://test?operation=describeVoices")
  .log("Available voices: ${body}");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="aws2-polly://test?operation=describeVoices"/>
  <log message="Available voices: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: aws2-polly://test
            parameters:
              operation: describeVoices
        - log:
            message: "Available voices: ${body}"
```

### Asynchronous Speech Synthesis with S3

For long text, you can use asynchronous synthesis which stores the result in S3:

_Java-only: uses Java constants for header names_

```java
from("direct:start")
  .setHeader(Polly2Constants.VOICE_ID, constant(VoiceId.JOANNA))
  .setHeader(Polly2Constants.S3_BUCKET, constant("my-audio-bucket"))
  .setHeader(Polly2Constants.S3_KEY_PREFIX, constant("audio/"))
  .setBody(constant("This is a very long text that will be synthesized asynchronously..."))
  .to("aws2-polly://test?operation=startSpeechSynthesisTask");
```

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as the body. In AWS Polly, you can do something like:

_Java-only: uses AWS SDK request builder API_

```java
from("direct:start")
  .setBody(SynthesizeSpeechRequest.builder()
              .voiceId(VoiceId.JOANNA)
              .outputFormat(OutputFormat.MP3)
              .text("Hello from Camel!")
              .build())
  .to("aws2-polly://test?operation=synthesizeSpeech&pojoRequest=true");
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-polly</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.
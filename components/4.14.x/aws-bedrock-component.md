# AWS Bedrock

**Since Camel 4.5**

**Only producer is supported**

The AWS2 Bedrock component supports invoking a supported LLM model from [AWS Bedrock](https://aws.amazon.com/bedrock/) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Bedrock. More information is available at [Amazon Bedrock](https://aws.amazon.com/bedrock/).

## URI Format

aws-bedrock://label\[?options\]

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

The AWS Bedrock component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | BedrockConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **modelId** (producer) | 
**Required** Define the model Id we are going to use.

Enum values:

-   amazon.titan-text-express-v1
    
-   amazon.titan-text-lite-v1
    
-   amazon.titan-image-generator-v1
    
-   amazon.titan-embed-text-v1
    
-   ai21.j2-ultra-v1
    
-   ai21.j2-mid-v1
    
-   anthropic.claude-instant-v1
    
-   anthropic.claude-v2
    
-   anthropic.claude-v2:1
    
-   anthropic.claude-3-sonnet-20240229-v1:0
    
-   anthropic.claude-3-haiku-20240307-v1:0
    
-   amazon.titan-text-premier-v1:0
    
-   amazon.titan-embed-text-v2:0
    





 |  | String |
| **operation** (producer) | 

**Required** The operation to perform.

Enum values:

-   invokeTextModel
    
-   invokeImageModel
    
-   invokeEmbeddingsModel
    





 |  | BedrockOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (producer) | 

The region in which Bedrock client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   us-east-1
    
-   us-west-1
    
-   ap-southeast-1
    
-   ap-northeast-1
    
-   eu-central-1
    





 |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Bedrock client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Bedrock client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **bedrockRuntimeClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Runtime client. |  | BedrockRuntimeClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Bedrock client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Bedrock client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Bedrock client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Bedrock client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | boolean |

## Endpoint Options

The AWS Bedrock endpoint is configured using URI syntax:

aws-bedrock:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **modelId** (producer) | 
**Required** Define the model Id we are going to use.

Enum values:

-   amazon.titan-text-express-v1
    
-   amazon.titan-text-lite-v1
    
-   amazon.titan-image-generator-v1
    
-   amazon.titan-embed-text-v1
    
-   ai21.j2-ultra-v1
    
-   ai21.j2-mid-v1
    
-   anthropic.claude-instant-v1
    
-   anthropic.claude-v2
    
-   anthropic.claude-v2:1
    
-   anthropic.claude-3-sonnet-20240229-v1:0
    
-   anthropic.claude-3-haiku-20240307-v1:0
    
-   amazon.titan-text-premier-v1:0
    
-   amazon.titan-embed-text-v2:0
    





 |  | String |
| **operation** (producer) | 

**Required** The operation to perform.

Enum values:

-   invokeTextModel
    
-   invokeImageModel
    
-   invokeEmbeddingsModel
    





 |  | BedrockOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (producer) | 

The region in which Bedrock client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   us-east-1
    
-   us-west-1
    
-   ap-southeast-1
    
-   ap-northeast-1
    
-   eu-central-1
    





 |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Bedrock client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Bedrock client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **bedrockRuntimeClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Runtime client. |  | BedrockRuntimeClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Bedrock client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Bedrock client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Bedrock client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Bedrock client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | boolean |

Required Bedrock component options

You have to provide the bedrockRuntimeClient in the Registry or your accessKey and secretKey to access the [Amazon Bedrock](https://aws.amazon.com/bedrock/) service.

## Usage

### Static credentials, Default Credential Provider and Profile Credentials Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`.
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You have also the possibility of using Profile Credentials Provider, by specifying the useProfileCredentialsProvider option to true and profileCredentialsName to the profile name.

Only one of static, default and profile credentials could be used at the same time.

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

## Message Headers

The AWS Bedrock component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsBedrockOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsBedrockContentType** (producer) Constant: [`MODEL_CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#MODEL_CONTENT_TYPE) | The model content type. |  | String |
| **CamelAwsBedrockAcceptContentType** (producer) Constant: [`MODEL_ACCEPT_CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#MODEL_ACCEPT_CONTENT_TYPE) | The model accept content type. |  | String |

### Supported AWS Bedrock Models

-   Titan Text Express V1 with id `amazon.titan-text-express-v1` Express is a large language model for text generation. It is useful for a wide range of advanced, general language tasks such as open-ended text generation and conversational chat, as well as support within Retrieval Augmented Generation (RAG).
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "inputText": {
      "type": "string"
    },
    "textGenerationConfig": {
      "type": "object",
      "properties": {
        "maxTokenCount": {
          "type": "integer"
        },
        "stopSequences": {
          "type": "array",
          "items": [
            {
              "type": "string"
            }
          ]
        },
        "temperature": {
          "type": "integer"
        },
        "topP": {
          "type": "integer"
        }
      },
      "required": [
        "maxTokenCount",
        "stopSequences",
        "temperature",
        "topP"
      ]
    }
  },
  "required": [
    "inputText",
    "textGenerationConfig"
  ]
}
```

-   Titan Text Lite V1 with id `amazon.titan-text-lite-v1` Lite is a light weight efficient model, ideal for fine-tuning of English-language tasks.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "inputText": {
      "type": "string"
    },
    "textGenerationConfig": {
      "type": "object",
      "properties": {
        "maxTokenCount": {
          "type": "integer"
        },
        "stopSequences": {
          "type": "array",
          "items": [
            {
              "type": "string"
            }
          ]
        },
        "temperature": {
          "type": "integer"
        },
        "topP": {
          "type": "integer"
        }
      },
      "required": [
        "maxTokenCount",
        "stopSequences",
        "temperature",
        "topP"
      ]
    }
  },
  "required": [
    "inputText",
    "textGenerationConfig"
  ]
}
```

-   Titan Image Generator G1 with id `amazon.titan-image-generator-v1` It generates images from text, and allows users to upload and edit an existing image. Users can edit an image with a text prompt (without a mask) or parts of an image with an image mask. You can extend the boundaries of an image with outpainting, and fill in an image with inpainting.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "textToImageParams": {
      "type": "object",
      "properties": {
        "text": {
          "type": "string"
        },
        "negativeText": {
          "type": "string"
        }
      },
      "required": [
        "text",
        "negativeText"
      ]
    },
    "taskType": {
      "type": "string"
    },
    "imageGenerationConfig": {
      "type": "object",
      "properties": {
        "cfgScale": {
          "type": "integer"
        },
        "seed": {
          "type": "integer"
        },
        "quality": {
          "type": "string"
        },
        "width": {
          "type": "integer"
        },
        "height": {
          "type": "integer"
        },
        "numberOfImages": {
          "type": "integer"
        }
      },
      "required": [
        "cfgScale",
        "seed",
        "quality",
        "width",
        "height",
        "numberOfImages"
      ]
    }
  },
  "required": [
    "textToImageParams",
    "taskType",
    "imageGenerationConfig"
  ]
}
```

-   Titan Embeddings G1 with id `amazon.titan-embed-text-v1` The Amazon Titan Embeddings G1 - Text – Text v1.2 can intake up to 8k tokens and outputs a vector of 1,536 dimensions. The model also works in 25+ different language
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "inputText": {
      "type": "string"
    }
  },
  "required": [
    "inputText"
  ]
}
```

-   Jurassic2-Ultra with id `ai21.j2-ultra-v1` Jurassic-2 Ultra is AI21’s most powerful model for complex tasks that require advanced text generation and comprehension.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "prompt": {
      "type": "string"
    },
    "maxTokens": {
      "type": "integer"
    },
    "temperature": {
      "type": "integer"
    },
    "topP": {
      "type": "integer"
    },
    "stopSequences": {
      "type": "array",
      "items": [
        {
          "type": "string"
        }
      ]
    },
    "presencePenalty": {
      "type": "object",
      "properties": {
        "scale": {
          "type": "integer"
        }
      },
      "required": [
        "scale"
      ]
    },
    "frequencyPenalty": {
      "type": "object",
      "properties": {
        "scale": {
          "type": "integer"
        }
      },
      "required": [
        "scale"
      ]
    }
  },
  "required": [
    "prompt",
    "maxTokens",
    "temperature",
    "topP",
    "stopSequences",
    "presencePenalty",
    "frequencyPenalty"
  ]
}
```

-   Jurassic2-Mid with id `ai21.j2-mid-v1` Jurassic-2 Mid is less powerful than Ultra, yet carefully designed to strike the right balance between exceptional quality and affordability.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "prompt": {
      "type": "string"
    },
    "maxTokens": {
      "type": "integer"
    },
    "temperature": {
      "type": "integer"
    },
    "topP": {
      "type": "integer"
    },
    "stopSequences": {
      "type": "array",
      "items": [
        {
          "type": "string"
        }
      ]
    },
    "presencePenalty": {
      "type": "object",
      "properties": {
        "scale": {
          "type": "integer"
        }
      },
      "required": [
        "scale"
      ]
    },
    "frequencyPenalty": {
      "type": "object",
      "properties": {
        "scale": {
          "type": "integer"
        }
      },
      "required": [
        "scale"
      ]
    }
  },
  "required": [
    "prompt",
    "maxTokens",
    "temperature",
    "topP",
    "stopSequences",
    "presencePenalty",
    "frequencyPenalty"
  ]
}
```

-   Claude Instant V1.2 with id `anthropic.claude-instant-v1` A fast, affordable yet still very capable model, which can handle a range of tasks including casual dialogue, text analysis, summarization, and document question-answering.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "prompt": {
      "type": "string"
    },
    "max_tokens_to_sample": {
      "type": "integer"
    },
    "stop_sequences": {
      "type": "array",
      "items": [
        {
          "type": "string"
        }
      ]
    },
    "temperature": {
      "type": "number"
    },
    "top_p": {
      "type": "integer"
    },
    "top_k": {
      "type": "integer"
    },
    "anthropic_version": {
      "type": "string"
    }
  },
  "required": [
    "prompt",
    "max_tokens_to_sample",
    "stop_sequences",
    "temperature",
    "top_p",
    "top_k",
    "anthropic_version"
  ]
}
```

-   Claude 2 with id `anthropic.claude-v2` Anthropic’s highly capable model across a wide range of tasks from sophisticated dialogue and creative content generation to detailed instruction following.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "prompt": {
      "type": "string"
    },
    "max_tokens_to_sample": {
      "type": "integer"
    },
    "stop_sequences": {
      "type": "array",
      "items": [
        {
          "type": "string"
        }
      ]
    },
    "temperature": {
      "type": "number"
    },
    "top_p": {
      "type": "integer"
    },
    "top_k": {
      "type": "integer"
    },
    "anthropic_version": {
      "type": "string"
    }
  },
  "required": [
    "prompt",
    "max_tokens_to_sample",
    "stop_sequences",
    "temperature",
    "top_p",
    "top_k",
    "anthropic_version"
  ]
}
```

-   Claude 2.1 with id `anthropic.claude-v2:1` An update to Claude 2 that features double the context window, plus improvements across reliability, hallucination rates, and evidence-based accuracy in long document and RAG contexts.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "prompt": {
      "type": "string"
    },
    "max_tokens_to_sample": {
      "type": "integer"
    },
    "stop_sequences": {
      "type": "array",
      "items": [
        {
          "type": "string"
        }
      ]
    },
    "temperature": {
      "type": "number"
    },
    "top_p": {
      "type": "integer"
    },
    "top_k": {
      "type": "integer"
    },
    "anthropic_version": {
      "type": "string"
    }
  },
  "required": [
    "prompt",
    "max_tokens_to_sample",
    "stop_sequences",
    "temperature",
    "top_p",
    "top_k",
    "anthropic_version"
  ]
}
```

-   Claude 3 Sonnet with id `anthropic.claude-3-sonnet-20240229-v1:0` Claude 3 Sonnet by Anthropic strikes the ideal balance between intelligence and speed—particularly for enterprise workloads.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "messages": {
      "type": "array",
      "items": [
        {
          "type": "object",
          "properties": {
            "role": {
              "type": "string"
            },
            "content": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "type": {
                      "type": "string"
                    },
                    "text": {
                      "type": "string"
                    }
                  },
                  "required": [
                    "type",
                    "text"
                  ]
                }
              ]
            }
          },
          "required": [
            "role",
            "content"
          ]
        }
      ]
    },
    "max_tokens": {
      "type": "integer"
    },
    "anthropic_version": {
      "type": "string"
    }
  },
  "required": [
    "messages",
    "max_tokens",
    "anthropic_version"
  ]
}
```

-   Claude 3 Haiku with id `anthropic.claude-3-haiku-20240307-v1:0` Claude 3 Haiku is Anthropic’s fastest, most compact model for near-instant responsiveness. It answers simple queries and requests with speed.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "messages": {
      "type": "array",
      "items": [
        {
          "type": "object",
          "properties": {
            "role": {
              "type": "string"
            },
            "content": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "type": {
                      "type": "string"
                    },
                    "text": {
                      "type": "string"
                    }
                  },
                  "required": [
                    "type",
                    "text"
                  ]
                }
              ]
            }
          },
          "required": [
            "role",
            "content"
          ]
        }
      ]
    },
    "max_tokens": {
      "type": "integer"
    },
    "anthropic_version": {
      "type": "string"
    }
  },
  "required": [
    "messages",
    "max_tokens",
    "anthropic_version"
  ]
}
```

### Bedrock Producer operations

Camel-AWS Bedrock component provides the following operation on the producer side:

-   invokeTextModel
    
-   invokeImageModel
    
-   invokeEmbeddingsModel
    

## Examples

### Producer Examples

-   invokeTextModel: this operation will invoke a model from Bedrock. This is an example for both Titan Express and Titan Lite.
    

```java
from("direct:invoke")
    .to("aws-bedrock://test?bedrockRuntimeClient=#amazonBedrockRuntimeClient&operation=invokeTextModel&modelId="
                            + BedrockModels.TITAN_TEXT_EXPRESS_V1.model))
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:invoke", exchange -> {
            ObjectMapper mapper = new ObjectMapper();
            ObjectNode rootNode = mapper.createObjectNode();
            rootNode.put("inputText",
                    "User: Generate synthetic data for daily product sales in various categories - include row number, product name, category, date of sale and price. Produce output in JSON format. Count records and ensure there are no more than 5.");

            ArrayNode stopSequences = mapper.createArrayNode();
            stopSequences.add("User:");
            ObjectNode childNode = mapper.createObjectNode();
            childNode.put("maxTokenCount", 1024);
            childNode.put("stopSequences", stopSequences);
            childNode.put("temperature", 0).put("topP", 1);

            rootNode.put("textGenerationConfig", childNode);
            exchange.getMessage().setBody(mapper.writer().writeValueAsString(rootNode));
            exchange.getMessage().setHeader(BedrockConstants.MODEL_CONTENT_TYPE, "application/json");
            exchange.getMessage().setHeader(BedrockConstants.MODEL_ACCEPT_CONTENT_TYPE, "application/json");
        });
```

where template is a ProducerTemplate.

-   invokeImageModel: this operation will invoke a model from Bedrock. This is an example for both Titan Express and Titan Lite.
    

```java
from("direct:invoke")
    .to("aws-bedrock://test?bedrockRuntimeClient=#amazonBedrockRuntimeClient&operation=invokeImageModel&modelId="
                            + BedrockModels.TITAN_IMAGE_GENERATOR_V1.model))
                        .split(body())
                        .unmarshal().base64()
                        .setHeader("CamelFileName", simple("image-${random(128)}.png")).to("file:target/generated_images")
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:send_titan_image", exchange -> {
            ObjectMapper mapper = new ObjectMapper();
            ObjectNode rootNode = mapper.createObjectNode();
            ObjectNode textParameter = mapper.createObjectNode();
            textParameter.putIfAbsent("text",
                    new TextNode("A Sci-fi camel running in the desert"));
            rootNode.putIfAbsent("textToImageParams", textParameter);
            rootNode.putIfAbsent("taskType", new TextNode("TEXT_IMAGE"));
            ObjectNode childNode = mapper.createObjectNode();
            childNode.putIfAbsent("numberOfImages", new IntNode(3));
            childNode.putIfAbsent("quality", new TextNode("standard"));
            childNode.putIfAbsent("cfgScale", new IntNode(8));
            childNode.putIfAbsent("height", new IntNode(512));
            childNode.putIfAbsent("width", new IntNode(512));
            childNode.putIfAbsent("seed", new IntNode(0));

            rootNode.putIfAbsent("imageGenerationConfig", childNode);

            exchange.getMessage().setBody(mapper.writer().writeValueAsString(rootNode));
            exchange.getMessage().setHeader(BedrockConstants.MODEL_CONTENT_TYPE, "application/json");
            exchange.getMessage().setHeader(BedrockConstants.MODEL_ACCEPT_CONTENT_TYPE, "application/json");
        });
```

where template is a ProducerTemplate.

-   invokeEmbeddingsModel: this operation will invoke an Embeddings model from Bedrock. This is an example for Titan Embeddings G1.
    

```java
from("direct:send_titan_embeddings")
    .to("aws-bedrock:label?useDefaultCredentialsProvider=true&region=us-east-1&operation=invokeEmbeddingsModel&modelId="
    + BedrockModels.TITAN_EMBEDDINGS_G1.model)
    .to(result);
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:send_titan_embeddings", exchange -> {
            ObjectMapper mapper = new ObjectMapper();
            ObjectNode rootNode = mapper.createObjectNode();
            rootNode.putIfAbsent("inputText",
                    new TextNode("A Sci-fi camel running in the desert"));

            exchange.getMessage().setBody(mapper.writer().writeValueAsString(rootNode));
            exchange.getMessage().setHeader(BedrockConstants.MODEL_CONTENT_TYPE, "application/json");
            exchange.getMessage().setHeader(BedrockConstants.MODEL_ACCEPT_CONTENT_TYPE, "*/*");
        });
```

where template is a ProducerTemplate.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws-bedrock</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws-bedrock with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws-bedrock-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 77 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws-bedrock-agent-runtime.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws-bedrock-agent-runtime.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws-bedrock-agent-runtime.bedrock-agent-runtime-client** | To use an existing configured AWS Bedrock Agent Runtime client. The option is a software.amazon.awssdk.services.bedrockagentruntime.BedrockAgentRuntimeClient type. |  | BedrockAgentRuntimeClient |
| **camel.component.aws-bedrock-agent-runtime.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.bedrock.agentruntime.BedrockAgentRuntimeConfiguration type. |  | BedrockAgentRuntimeConfiguration |
| **camel.component.aws-bedrock-agent-runtime.enabled** | Whether to enable auto configuration of the aws-bedrock-agent-runtime component. This is enabled by default. |  | Boolean |
| **camel.component.aws-bedrock-agent-runtime.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws-bedrock-agent-runtime.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws-bedrock-agent-runtime.knowledge-base-id** | Define the Knowledge Base Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent-runtime.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.model-id** | Define the model Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent-runtime.operation** | The operation to perform. |  | BedrockAgentRuntimeOperations |
| **camel.component.aws-bedrock-agent-runtime.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **camel.component.aws-bedrock-agent-runtime.proxy-host** | To define a proxy host when instantiating the Bedrock Agent Runtime client. |  | String |
| **camel.component.aws-bedrock-agent-runtime.proxy-port** | To define a proxy port when instantiating the Bedrock Agent Runtime client. |  | Integer |
| **camel.component.aws-bedrock-agent-runtime.proxy-protocol** | To define a proxy protocol when instantiating the Bedrock Agent Runtime client. | https | Protocol |
| **camel.component.aws-bedrock-agent-runtime.region** | The region in which Bedrock Agent Runtime client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws-bedrock-agent-runtime.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws-bedrock-agent-runtime.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws-bedrock-agent-runtime.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws-bedrock-agent-runtime.use-default-credentials-provider** | Set whether the Bedrock Agent Runtime client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.use-profile-credentials-provider** | Set whether the Bedrock Agent Runtime client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.use-session-credentials** | Set whether the Bedrock Agent Runtime client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | Boolean |
| **camel.component.aws-bedrock-agent.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws-bedrock-agent.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws-bedrock-agent.bedrock-agent-client** | To use an existing configured AWS Bedrock Agent client. The option is a software.amazon.awssdk.services.bedrockagent.BedrockAgentClient type. |  | BedrockAgentClient |
| **camel.component.aws-bedrock-agent.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.aws-bedrock-agent.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.bedrock.agent.BedrockAgentConfiguration type. |  | BedrockAgentConfiguration |
| **camel.component.aws-bedrock-agent.data-source-id** | Define the Data source Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent.enabled** | Whether to enable auto configuration of the aws-bedrock-agent component. This is enabled by default. |  | Boolean |
| **camel.component.aws-bedrock-agent.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws-bedrock-agent.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws-bedrock-agent.ingestion-job-id** | Define the Ingestion Job Id we want to track. |  | String |
| **camel.component.aws-bedrock-agent.knowledge-base-id** | Define the Knowledge Base Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws-bedrock-agent.model-id** | Define the model Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent.operation** | The operation to perform. |  | BedrockAgentOperations |
| **camel.component.aws-bedrock-agent.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws-bedrock-agent.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws-bedrock-agent.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **camel.component.aws-bedrock-agent.proxy-host** | To define a proxy host when instantiating the Bedrock Agent client. |  | String |
| **camel.component.aws-bedrock-agent.proxy-port** | To define a proxy port when instantiating the Bedrock Agent client. |  | Integer |
| **camel.component.aws-bedrock-agent.proxy-protocol** | To define a proxy protocol when instantiating the Bedrock Agent client. | https | Protocol |
| **camel.component.aws-bedrock-agent.region** | The region in which Bedrock Agent client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws-bedrock-agent.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws-bedrock-agent.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws-bedrock-agent.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws-bedrock-agent.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws-bedrock-agent.use-default-credentials-provider** | Set whether the Bedrock Agent client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws-bedrock-agent.use-profile-credentials-provider** | Set whether the Bedrock Agent client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws-bedrock-agent.use-session-credentials** | Set whether the Bedrock Agent client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | Boolean |
| **camel.component.aws-bedrock.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws-bedrock.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws-bedrock.bedrock-runtime-client** | To use an existing configured AWS Bedrock Runtime client. The option is a software.amazon.awssdk.services.bedrockruntime.BedrockRuntimeClient type. |  | BedrockRuntimeClient |
| **camel.component.aws-bedrock.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.bedrock.runtime.BedrockConfiguration type. |  | BedrockConfiguration |
| **camel.component.aws-bedrock.enabled** | Whether to enable auto configuration of the aws-bedrock component. This is enabled by default. |  | Boolean |
| **camel.component.aws-bedrock.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws-bedrock.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws-bedrock.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws-bedrock.model-id** | Define the model Id we are going to use. |  | String |
| **camel.component.aws-bedrock.operation** | The operation to perform. |  | BedrockOperations |
| **camel.component.aws-bedrock.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws-bedrock.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws-bedrock.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **camel.component.aws-bedrock.proxy-host** | To define a proxy host when instantiating the Bedrock client. |  | String |
| **camel.component.aws-bedrock.proxy-port** | To define a proxy port when instantiating the Bedrock client. |  | Integer |
| **camel.component.aws-bedrock.proxy-protocol** | To define a proxy protocol when instantiating the Bedrock client. | https | Protocol |
| **camel.component.aws-bedrock.region** | The region in which Bedrock client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws-bedrock.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws-bedrock.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws-bedrock.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws-bedrock.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws-bedrock.use-default-credentials-provider** | Set whether the Bedrock client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws-bedrock.use-profile-credentials-provider** | Set whether the Bedrock client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws-bedrock.use-session-credentials** | Set whether the Bedrock client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | Boolean |
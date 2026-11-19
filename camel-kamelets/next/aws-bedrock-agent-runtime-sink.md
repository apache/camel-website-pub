# ![aws bedrock agent runtime sink](_images/kamelets/aws-bedrock-agent-runtime-sink.svg) AWS Bedrock Agent Runtime Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Answers the question in each message from the documents of an Amazon Bedrock knowledge base, or finds the passages of the documents that match it, or passes it to a Bedrock agent.

Use it to build a question-and-answer service or a chatbot over your own documents, such as manuals, policies or FAQs, loaded into a Bedrock knowledge base. Set `operation` to `retrieve` to get only the passages that match the question, for example to show them as search results or to give them to a model of your own. Set it to `invokeAgent` to ask a Bedrock agent that you have set up in the Bedrock console. To load new documents into the knowledge base, use `aws-bedrock-agent-sink`; to call a model without a knowledge base, use `aws-bedrock-text-sink`.

Input: the body is the question, as text. The optional `CamelAwsBedrockAgentRuntimeSessionId` header continues an earlier conversation, with `retrieveAndGenerate` and `invokeAgent`: set it to the session ID of an earlier answer.

Output: when it is used inside a route, the body afterwards depends on `operation`. With `retrieveAndGenerate`, the default, and with `invokeAgent`, it is the answer, as text. The `CamelAwsBedrockAgentRuntimeSessionId` header holds the ID of the session, and the `CamelAwsBedrockAgentRuntimeCitations` header the passages of the documents the answer is based on, as objects of the AWS SDK for Java. With `retrieve`, the body is a List of the passages found, each an object of the AWS SDK for Java with the text of the passage (`content.text`), its `score` and the `location` of its document. The `CamelAwsBedrockAgentRuntimeRetrievedResults` header holds the same List.

Good to know: `retrieveAndGenerate` needs `modelId` and `knowledgeBaseId`, `retrieve` needs `knowledgeBaseId`, and `invokeAgent` needs `agentId` and `agentAliasId`; without them, `retrieve` and `invokeAgent` fail before they call Bedrock. The passages from `retrieve` are not JSON, and turned into JSON as they are, each is an empty object: take the parts you need in the next step, such as `$\{body[0].content.text}` in a Simple expression. With `invokeAgent` and no session ID, each message starts a new session. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid. Headers that start with `CamelAwsBedrock`, except `CamelAwsBedrockAgentRuntimeSessionId`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `aws-bedrock-agent-runtime-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region of the knowledge base, such as `us-east-1`. Enum values: \* us-east-1 \* us-west-1 | string |  | us-east-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
| **agentAliasId** | Agent Alias ID | The ID of the alias of the agent in `agentId`, a code of 10 letters and digits shown in the Bedrock console. An alias points to one version of the agent; `TSTALIASID` is the alias of its working draft. Required when `operation` is `invokeAgent`. | string |  | TSTALIASID |
| **agentId** | Agent ID | The ID of the Bedrock agent to ask, a code of 10 letters and digits shown in the Bedrock console. Required when `operation` is `invokeAgent`; the other operations do not use it. | string |  | KX7Q2M9WZB |
| **knowledgeBaseId** | Knowledge Base ID | The ID of the knowledge base to search, a code of 10 letters and digits shown in the Bedrock console. Required when `operation` is `retrieveAndGenerate` or `retrieve`; `invokeAgent` does not use it, as the agent has its own knowledge bases. | string |  | AB12CD34EF |
| **modelId** | Model ID | The ID of the Bedrock model that writes the answers from the parts of the documents that were found. It must be available in the region of the knowledge base. Required when `operation` is `retrieveAndGenerate`; the other operations do not use it. Enum values: \* anthropic.claude-instant-v1 \* anthropic.claude-v2 \* anthropic.claude-v2:1 \* anthropic.claude-3-sonnet-20240229-v1:0 | string |  |  |
| **numberOfResults** | Number of Results | The most passages to give for each question. Only used when `operation` is `retrieve`. When it is not set, Bedrock decides how many. | integer |  | 10 |
| **operation** | Operation | What to do with the question. `retrieveAndGenerate` finds the passages that match it in the knowledge base, and has the model in `modelId` write the answer from them. `retrieve` only finds the passages, and gives them without an answer. `invokeAgent` sends the question to the Bedrock agent in `agentId`, which answers it in its own way, for example with its own knowledge bases and actions. Enum values: \* retrieveAndGenerate \* retrieve \* invokeAgent | string | retrieveAndGenerate |  |
| **overrideEndpoint** | Endpoint Overwrite | If true, the requests go to the address in `uriEndpointOverride` instead of AWS, for example to test against LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile to use from the AWS credentials file. Only used when `useProfileCredentialsProvider` is true. | string |  |  |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **searchType** | Search Type | How to search the knowledge base for the passages: `SEMANTIC` looks for passages with the same meaning as the question, `HYBRID` also looks for the words of the question, which helps for names and codes. Only used when `operation` is `retrieve`. When it is not set, Bedrock decides. Enum values: \* HYBRID \* SEMANTIC | string |  |  |
| **secretKey** | Secret Key | The secret access key that goes with `accessKey`. AWS shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which AWS gives together with their access key and secret key. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to send the requests to instead of the usual AWS address, such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found the way the AWS SDK finds them: from the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the shared credentials file, or the IAM role of the machine, container or pod it runs on. Then `accessKey` and `secretKey` are not needed. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a profile of the AWS credentials file (`~/.aws/credentials`), the one named in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials, such as those of an assumed IAM role: `accessKey`, `secretKey` and `sessionToken` together. | boolean | false |  |

## Dependencies

At runtime, the `aws-bedrock-agent-runtime-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:aws-bedrock
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:aws-bedrock-agent-runtime-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Bedrock Agent Runtime Sink Kamelet Description

### Authentication methods

In this Kamelet you can avoid using explicit static credentials by specifying the `useDefaultCredentialsProvider` option and set it to `true`.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`.
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You can also use the Profile Credentials Provider, by setting the `useProfileCredentialsProvider` option to `true` and `profileCredentialsName` to the profile name.

Only one of access key/secret key or default credentials provider could be used

For more information, see the [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-bedrock-agent-runtime-sink"
    parameters:
      modelId: "anthropic.claude-v2"
      knowledgeBaseId: "AB12CD34EF"
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

### Operations

`operation` chooses what the Kamelet does with the question in the body:

  
| `operation` | What it does | Options it needs |
| --- | --- | --- |
| `retrieveAndGenerate` (default) | Finds the passages that match the question in the knowledge base, and has the model write the answer from them. The body afterwards is the answer, as text. | `modelId`, `knowledgeBaseId` |
| `retrieve` | Only finds the passages, without an answer. The body afterwards is a List of the passages, each with its text (`content.text`), its `score` and the `location` of its document. `numberOfResults` limits how many, and `searchType` chooses between a `SEMANTIC` and a `HYBRID` search. | `knowledgeBaseId` |
| `invokeAgent` | Sends the question to a Bedrock agent, which answers it with its own instructions, knowledge bases and actions. The body afterwards is the answer, as text. | `agentId`, `agentAliasId` |

The passages from `retrieve` are objects of the AWS SDK for Java, not JSON: turned into JSON as they are, each is an empty object. Take the parts you need in the next step. For example, to keep the text of the first passage:

```yaml
- to:
    uri: "kamelet:aws-bedrock-agent-runtime-sink"
    parameters:
      operation: "retrieve"
      knowledgeBaseId: "AB12CD34EF"
      numberOfResults: 3
      searchType: "HYBRID"
      region: "us-east-1"
      useDefaultCredentialsProvider: true
- setBody:
    simple: "$\{body[0].content.text}"
```

To ask an agent, and continue the conversation with the session ID of the answer:

```yaml
- to:
    uri: "kamelet:aws-bedrock-agent-runtime-sink"
    parameters:
      operation: "invokeAgent"
      agentId: "KX7Q2M9WZB"
      agentAliasId: "TSTALIASID"
      region: "us-east-1"
      useDefaultCredentialsProvider: true
```

Without the `CamelAwsBedrockAgentRuntimeSessionId` header, each message starts a new session, and the header holds its ID afterwards. Send that ID in the header with the next question to continue the same conversation.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-bedrock-agent-runtime-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-bedrock-agent-runtime-sink.kamelet.yaml)
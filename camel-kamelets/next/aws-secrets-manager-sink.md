# ![aws secrets manager sink](_images/kamelets/aws-secrets-manager-sink.svg) AWS Secrets Manager Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Creates a secret in AWS Secrets Manager for each message, with the body as its value, or changes or reads the value of an existing secret.

Use it to store passwords, API keys or certificates that another system generates, so that your applications can read them from Secrets Manager, to rotate such a value, or to read one inside a route.

Input: the body is the value of the secret, as text, for example a password, or several values as a JSON object in JSON text. With `operation` set to `getSecret`, the body is not used. For `createSecret`, the name of the new secret comes from the `secret-name` header, else from the `ce-secret-name` header; without either, the ID of the message is used as the name. `updateSecret` and `getSecret` work on the secret in `secretId`.

Output: when it is used inside a route, the body afterwards is the answer of AWS, a `CreateSecretResponse` object of the AWS SDK for Java with the ARN, the name and the version ID of the new secret; for `updateSecret`, an `UpdateSecretResponse` with the ARN, the name and the new version ID. For `getSecret`, the body is the value of the secret, as text, or as bytes for a binary secret, and the `CamelAwsSecretsManagerSecretVersionId` header holds the ID of its version. The `Content-Type` header stays `text/plain`, from the input.

Good to know: by default it only creates secrets, and a message for a name that already exists fails. Set `operation` to `updateSecret` to change the value of the existing secret in `secretId`, or to `getSecret` to read it; both fail when `secretId` is not set or the secret does not exist. A message without a name header creates a secret with a generated name, such as `4D678616B8AFAA1-0000000000000002`. With `binaryPayload`, the body is stored as the binary value of the secret instead of as text. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid. Headers that start with `CamelAwsSecretsManager` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `aws-secrets-manager-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region to create the secrets in, such as `eu-west-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
| **binaryPayload** | Binary Payload | If true, `createSecret` and `updateSecret` store the bytes of the body as the binary value of the secret (`SecretBinary`), for example a keystore file, instead of as text (`SecretString`). `getSecret` gives the bytes of a binary secret whatever this option says. When it is not set, the value is stored as text. | boolean |  | true |
| **operation** | Operation | What to do with each message: `createSecret` creates a new secret with the body as its value; `updateSecret` stores the body as the new value of an existing secret, as a new version; `getSecret` reads the current value of an existing secret into the body. `createSecret` names the new secret from the `secret-name` header; `updateSecret` and `getSecret` work on the secret in `secretId`, which they need. Enum values: \* createSecret \* updateSecret \* getSecret | string | createSecret | updateSecret |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to AWS. Use it for a local stand-in of AWS such as LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile to use from the AWS credentials file. Only used when `useProfileCredentialsProvider` is true. | string |  |  |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **secretId** | Secret ID | The name or the ARN of the secret that `updateSecret` and `getSecret` work on, such as `prod/db-password`. Required for these two operations: without it, each of their messages fails with `The secretId option must be set`. Not used by `createSecret`. | string |  | prod/db-password |
| **secretKey** | Secret Key | The secret access key that goes with `accessKey`. AWS shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which AWS gives together with their access key and secret key. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found the way the AWS SDK finds them: from the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the shared credentials file, or the IAM role of the machine, container or pod it runs on. Then `accessKey` and `secretKey` are not needed. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a profile of the AWS credentials file (`~/.aws/credentials`), the one named in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials, such as those of an assumed IAM role: `accessKey`, `secretKey` and `sessionToken` together. | boolean | false |  |

## Dependencies

At runtime, the `aws-secrets-manager-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:aws-secrets-manager
    
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
            uri: "kamelet:aws-secrets-manager-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Secrets Manager Sink Kamelet Description

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

### Headers

The Kamelet reads the following header:

-   `secret-name` / `ce-secret-name`: as the name of the secret to create.
    

If the header is not set, the ID of the message is used as secret name.

### Changing or Reading a Secret

By default, the Kamelet creates a new secret for each message, and a message for a name that already exists fails. Set `operation` to work with the existing secret named in `secretId`, by its name or its ARN:

-   `createSecret` (the default): creates a new secret with the body as its value, named from the `secret-name` header as above. `secretId` is not used.
    
-   `updateSecret`: stores the body as the new value of the secret, as a new version. The version before stays available as the previous one (`AWSPREVIOUS`).
    
-   `getSecret`: reads the current value of the secret into the body, as text, or as bytes for a binary secret. The `CamelAwsSecretsManagerSecretVersionId` header holds the ID of the version that was read.
    

`updateSecret` and `getSecret` need `secretId`: without it, each message fails with `The secretId option must be set`. They also fail for a secret that does not exist.

With `binaryPayload` set to `true`, `createSecret` and `updateSecret` store the bytes of the body as the binary value of the secret, for example a keystore file, instead of as text.

The step that sends to the Kamelet, in a route, to rotate a password, with the new password in the body:

```yaml
- to:
    uri: "kamelet:aws-secrets-manager-sink"
    parameters:
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      operation: "updateSecret"
      secretId: "prod/db-password"
```

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-secrets-manager-sink"
    parameters:
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-secrets-manager-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-secrets-manager-sink.kamelet.yaml)
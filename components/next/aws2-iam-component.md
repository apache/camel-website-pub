# AWS Identity and Access Management (IAM)

**Since Camel 3.1**

**Only producer is supported**

The AWS2 IAM component supports create, run, start, stop and terminate [AWS IAM](https://aws.amazon.com/iam/) instances.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon IAM. More information is available at [Amazon IAM](https://aws.amazon.com/iam/).

## URI Format

aws2-iam://label\[?options\]

You can append query options to the URI in the following format:

`?options=value&option2=value&…​`

> **Note**
> The AWS2 IAM component works on the aws-global region, and it has aws-global as the default region

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

The AWS Identity and Access Management (IAM) component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | IAM2Configuration |
| **iamClient** (producer) | **Autowired** To use an existing configured AWS IAM client. |  | IamClient |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform. You can configure a default operation on the component level, or the operation as part of the endpoint, or via a message header with the key CamelAwsIAMOperation.

Enum values:

-   listAccessKeys
    
-   createUser
    
-   deleteUser
    
-   getUser
    
-   listUsers
    
-   createAccessKey
    
-   deleteAccessKey
    
-   updateAccessKey
    
-   createGroup
    
-   deleteGroup
    
-   listGroups
    
-   addUserToGroup
    
-   removeUserFromGroup
    
-   createRole
    
-   deleteRole
    
-   getRole
    
-   listRoles
    
-   createPolicy
    
-   deletePolicy
    
-   getPolicy
    
-   listPolicies
    
-   attachUserPolicy
    
-   detachUserPolicy
    
-   attachGroupPolicy
    
-   detachGroupPolicy
    
-   attachRolePolicy
    
-   detachRolePolicy
    
-   createInstanceProfile
    
-   deleteInstanceProfile
    
-   getInstanceProfile
    
-   listInstanceProfiles
    
-   addRoleToInstanceProfile
    
-   removeRoleFromInstanceProfile
    





 |  | IAM2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which IAM client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
    





 | aws-global | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the IAM client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the IAM client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the IAM client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the IAM client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the IAM client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the IAM client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume a IAM role for doing operations in IAM. | false | boolean |

## Endpoint Options

The AWS Identity and Access Management (IAM) endpoint is configured using URI syntax:

aws2-iam:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (18 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **iamClient** (producer) | **Autowired** To use an existing configured AWS IAM client. |  | IamClient |
| **operation** (producer) | 
The operation to perform. You can configure a default operation on the component level, or the operation as part of the endpoint, or via a message header with the key CamelAwsIAMOperation.

Enum values:

-   listAccessKeys
    
-   createUser
    
-   deleteUser
    
-   getUser
    
-   listUsers
    
-   createAccessKey
    
-   deleteAccessKey
    
-   updateAccessKey
    
-   createGroup
    
-   deleteGroup
    
-   listGroups
    
-   addUserToGroup
    
-   removeUserFromGroup
    
-   createRole
    
-   deleteRole
    
-   getRole
    
-   listRoles
    
-   createPolicy
    
-   deletePolicy
    
-   getPolicy
    
-   listPolicies
    
-   attachUserPolicy
    
-   detachUserPolicy
    
-   attachGroupPolicy
    
-   detachGroupPolicy
    
-   attachRolePolicy
    
-   detachRolePolicy
    
-   createInstanceProfile
    
-   deleteInstanceProfile
    
-   getInstanceProfile
    
-   listInstanceProfiles
    
-   addRoleToInstanceProfile
    
-   removeRoleFromInstanceProfile
    





 |  | IAM2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which IAM client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
    





 | aws-global | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the IAM client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the IAM client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the IAM client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the IAM client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the IAM client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the IAM client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume a IAM role for doing operations in IAM. | false | boolean |

## Message Headers

The AWS Identity and Access Management (IAM) component supports 30 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsIAMOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsIAMUsername** (producer) Constant: [`USERNAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#USERNAME) | The username for the user you want to manage. |  | String |
| **CamelAwsIAMAccessKeyID** (producer) Constant: [`ACCESS_KEY_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#ACCESS_KEY_ID) | The accessKey you want to manage. |  | String |
| **CamelAwsIAMAccessKeyStatus** (producer) Constant: [`ACCESS_KEY_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#ACCESS_KEY_STATUS) | The Status of the AccessKey you want to set, possible value are active and inactive. |  | String |
| **CamelAwsIAMGroupName** (producer) Constant: [`GROUP_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#GROUP_NAME) | The name of an AWS IAM Group. |  | String |
| **CamelAwsIAMGroupPath** (producer) Constant: [`GROUP_PATH`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#GROUP_PATH) | The path of an AWS IAM Group. |  | String |
| **CamelAwsIAMMarker** (producer) Constant: [`MARKER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#MARKER) | The marker to use for pagination in list operations. |  | String |
| **CamelAwsIAMMaxItems** (producer) Constant: [`MAX_ITEMS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#MAX_ITEMS) | The maximum number of items to return in list operations. |  | Integer |
| **CamelAwsIAMIsTruncated** (producer) Constant: [`IS_TRUNCATED`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#IS_TRUNCATED) | Whether the list response is truncated (has more results). |  | Boolean |
| **CamelAwsIAMNextMarker** (producer) Constant: [`NEXT_MARKER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#NEXT_MARKER) | The marker to use for the next page of results. |  | String |
| **CamelAwsIAMUserArn** (producer) Constant: [`USER_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#USER_ARN) | The ARN of the created or retrieved user. |  | String |
| **CamelAwsIAMUserId** (producer) Constant: [`USER_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#USER_ID) | The ID of the created or retrieved user. |  | String |
| **CamelAwsIAMGroupArn** (producer) Constant: [`GROUP_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#GROUP_ARN) | The ARN of the created or retrieved group. |  | String |
| **CamelAwsIAMGroupId** (producer) Constant: [`GROUP_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#GROUP_ID) | The ID of the created or retrieved group. |  | String |
| **CamelAwsIAMRoleName** (producer) Constant: [`ROLE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#ROLE_NAME) | The name of an AWS IAM Role. |  | String |
| **CamelAwsIAMRolePath** (producer) Constant: [`ROLE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#ROLE_PATH) | The path of an AWS IAM Role. |  | String |
| **CamelAwsIAMAssumeRolePolicyDocument** (producer) Constant: [`ASSUME_ROLE_POLICY_DOCUMENT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#ASSUME_ROLE_POLICY_DOCUMENT) | The assume role policy document for the role. |  | String |
| **CamelAwsIAMRoleArn** (producer) Constant: [`ROLE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#ROLE_ARN) | The ARN of the created or retrieved role. |  | String |
| **CamelAwsIAMRoleId** (producer) Constant: [`ROLE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#ROLE_ID) | The ID of the created or retrieved role. |  | String |
| **CamelAwsIAMRoleDescription** (producer) Constant: [`ROLE_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#ROLE_DESCRIPTION) | The description of an AWS IAM Role. |  | String |
| **CamelAwsIAMPolicyName** (producer) Constant: [`POLICY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#POLICY_NAME) | The name of an AWS IAM Policy. |  | String |
| **CamelAwsIAMPolicyPath** (producer) Constant: [`POLICY_PATH`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#POLICY_PATH) | The path of an AWS IAM Policy. |  | String |
| **CamelAwsIAMPolicyDocument** (producer) Constant: [`POLICY_DOCUMENT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#POLICY_DOCUMENT) | The policy document. |  | String |
| **CamelAwsIAMPolicyArn** (producer) Constant: [`POLICY_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#POLICY_ARN) | The ARN of an AWS IAM Policy. |  | String |
| **CamelAwsIAMPolicyId** (producer) Constant: [`POLICY_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#POLICY_ID) | The ID of an AWS IAM Policy. |  | String |
| **CamelAwsIAMPolicyDescription** (producer) Constant: [`POLICY_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#POLICY_DESCRIPTION) | The description of an AWS IAM Policy. |  | String |
| **CamelAwsIAMInstanceProfileName** (producer) Constant: [`INSTANCE_PROFILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#INSTANCE_PROFILE_NAME) | The name of an AWS IAM Instance Profile. |  | String |
| **CamelAwsIAMInstanceProfilePath** (producer) Constant: [`INSTANCE_PROFILE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#INSTANCE_PROFILE_PATH) | The path of an AWS IAM Instance Profile. |  | String |
| **CamelAwsIAMInstanceProfileArn** (producer) Constant: [`INSTANCE_PROFILE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#INSTANCE_PROFILE_ARN) | The ARN of an AWS IAM Instance Profile. |  | String |
| **CamelAwsIAMInstanceProfileId** (producer) Constant: [`INSTANCE_PROFILE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-iam/latest/org/apache/camel/component/aws2/iam/IAM2Constants.html#INSTANCE_PROFILE_ID) | The ID of an AWS IAM Instance Profile. |  | String |

Required IAM component options

You have to provide the amazonKmsClient in the Registry or your accessKey and secretKey to access the [Amazon IAM](https://aws.amazon.com/iam/) service.

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

### IAM Producer operations

Camel-AWS2 IAM component provides the following operation on the producer side:

-   listAccessKeys
    
-   createUser
    
-   deleteUser
    
-   listUsers
    
-   getUser
    
-   createAccessKey
    
-   deleteAccessKey
    
-   updateAccessKey
    
-   createGroup
    
-   deleteGroup
    
-   listGroups
    
-   addUserToGroup
    
-   removeUserFromGroup
    
-   createRole
    
-   deleteRole
    
-   getRole
    
-   listRoles
    
-   createPolicy
    
-   deletePolicy
    
-   getPolicy
    
-   listPolicies
    
-   attachUserPolicy
    
-   detachUserPolicy
    
-   attachGroupPolicy
    
-   detachGroupPolicy
    
-   attachRolePolicy
    
-   detachRolePolicy
    
-   createInstanceProfile
    
-   deleteInstanceProfile
    
-   getInstanceProfile
    
-   listInstanceProfiles
    
-   addRoleToInstanceProfile
    
-   removeRoleFromInstanceProfile
    

## Examples

### Producer Examples

-   createUser: this operation will create a user in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createUser")
    .setHeader("CamelAwsIAMUsername", constant("camel"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=createUser");
```

```xml
<route>
    <from uri="direct:createUser"/>
    <setHeader name="CamelAwsIAMUsername">
        <constant>camel</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=createUser"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createUser
    steps:
      - setHeader:
          name: CamelAwsIAMUsername
          constant: camel
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: createUser
```

-   deleteUser: this operation will delete a user in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deleteUser")
    .setHeader("CamelAwsIAMUsername", constant("camel"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=deleteUser");
```

```xml
<route>
    <from uri="direct:deleteUser"/>
    <setHeader name="CamelAwsIAMUsername">
        <constant>camel</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=deleteUser"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:deleteUser
    steps:
      - setHeader:
          name: CamelAwsIAMUsername
          constant: camel
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: deleteUser
```

-   listUsers: this operation will list the users in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:listUsers")
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=listUsers");
```

```xml
<route>
    <from uri="direct:listUsers"/>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=listUsers"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:listUsers
    steps:
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: listUsers
```

-   createGroup: this operation will add a group in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createGroup")
    .setHeader("CamelAwsIAMGroupName", constant("camel"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=createGroup");
```

```xml
<route>
    <from uri="direct:createGroup"/>
    <setHeader name="CamelAwsIAMGroupName">
        <constant>camel</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=createGroup"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createGroup
    steps:
      - setHeader:
          name: CamelAwsIAMGroupName
          constant: camel
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: createGroup
```

-   deleteGroup: this operation will delete a group in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deleteGroup")
    .setHeader("CamelAwsIAMGroupName", constant("camel"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=deleteGroup");
```

```xml
<route>
    <from uri="direct:deleteGroup"/>
    <setHeader name="CamelAwsIAMGroupName">
        <constant>camel</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=deleteGroup"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:deleteGroup
    steps:
      - setHeader:
          name: CamelAwsIAMGroupName
          constant: camel
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: deleteGroup
```

-   listGroups: this operation will list the groups in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:listGroups")
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=listGroups");
```

```xml
<route>
    <from uri="direct:listGroups"/>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=listGroups"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:listGroups
    steps:
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: listGroups
```

#### Role Operations

-   createRole: this operation will create a role in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createRole")
    .setHeader("CamelAwsIAMRoleName", constant("myRole"))
    .setHeader("CamelAwsIAMAssumeRolePolicyDocument", constant("{...}"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=createRole");
```

```xml
<route>
    <from uri="direct:createRole"/>
    <setHeader name="CamelAwsIAMRoleName">
        <constant>myRole</constant>
    </setHeader>
    <setHeader name="CamelAwsIAMAssumeRolePolicyDocument">
        <constant>{...}</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=createRole"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createRole
    steps:
      - setHeader:
          name: CamelAwsIAMRoleName
          constant: myRole
      - setHeader:
          name: CamelAwsIAMAssumeRolePolicyDocument
          constant: "{...}"
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: createRole
```

-   deleteRole: this operation will delete a role in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deleteRole")
    .setHeader("CamelAwsIAMRoleName", constant("myRole"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=deleteRole");
```

```xml
<route>
    <from uri="direct:deleteRole"/>
    <setHeader name="CamelAwsIAMRoleName">
        <constant>myRole</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=deleteRole"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:deleteRole
    steps:
      - setHeader:
          name: CamelAwsIAMRoleName
          constant: myRole
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: deleteRole
```

-   getRole: this operation will get a role in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getRole")
    .setHeader("CamelAwsIAMRoleName", constant("myRole"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=getRole");
```

```xml
<route>
    <from uri="direct:getRole"/>
    <setHeader name="CamelAwsIAMRoleName">
        <constant>myRole</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=getRole"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getRole
    steps:
      - setHeader:
          name: CamelAwsIAMRoleName
          constant: myRole
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: getRole
```

-   listRoles: this operation will list the roles in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:listRoles")
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=listRoles");
```

```xml
<route>
    <from uri="direct:listRoles"/>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=listRoles"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:listRoles
    steps:
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: listRoles
```

#### Policy Operations

-   createPolicy: this operation will create a policy in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createPolicy")
    .setHeader("CamelAwsIAMPolicyName", constant("myPolicy"))
    .setHeader("CamelAwsIAMPolicyDocument", constant("{...}"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=createPolicy");
```

```xml
<route>
    <from uri="direct:createPolicy"/>
    <setHeader name="CamelAwsIAMPolicyName">
        <constant>myPolicy</constant>
    </setHeader>
    <setHeader name="CamelAwsIAMPolicyDocument">
        <constant>{...}</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=createPolicy"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createPolicy
    steps:
      - setHeader:
          name: CamelAwsIAMPolicyName
          constant: myPolicy
      - setHeader:
          name: CamelAwsIAMPolicyDocument
          constant: "{...}"
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: createPolicy
```

-   deletePolicy: this operation will delete a policy in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deletePolicy")
    .setHeader("CamelAwsIAMPolicyArn", constant("arn:aws:iam::123456789012:policy/myPolicy"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=deletePolicy");
```

```xml
<route>
    <from uri="direct:deletePolicy"/>
    <setHeader name="CamelAwsIAMPolicyArn">
        <constant>arn:aws:iam::123456789012:policy/myPolicy</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=deletePolicy"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:deletePolicy
    steps:
      - setHeader:
          name: CamelAwsIAMPolicyArn
          constant: "arn:aws:iam::123456789012:policy/myPolicy"
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: deletePolicy
```

-   getPolicy: this operation will get a policy in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getPolicy")
    .setHeader("CamelAwsIAMPolicyArn", constant("arn:aws:iam::123456789012:policy/myPolicy"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=getPolicy");
```

```xml
<route>
    <from uri="direct:getPolicy"/>
    <setHeader name="CamelAwsIAMPolicyArn">
        <constant>arn:aws:iam::123456789012:policy/myPolicy</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=getPolicy"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getPolicy
    steps:
      - setHeader:
          name: CamelAwsIAMPolicyArn
          constant: "arn:aws:iam::123456789012:policy/myPolicy"
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: getPolicy
```

-   listPolicies: this operation will list the policies in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:listPolicies")
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=listPolicies");
```

```xml
<route>
    <from uri="direct:listPolicies"/>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=listPolicies"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:listPolicies
    steps:
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: listPolicies
```

#### Policy Attachment Operations

-   attachUserPolicy: this operation will attach a policy to a user
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:attachUserPolicy")
    .setHeader("CamelAwsIAMUsername", constant("camel"))
    .setHeader("CamelAwsIAMPolicyArn", constant("arn:aws:iam::123456789012:policy/myPolicy"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=attachUserPolicy");
```

```xml
<route>
    <from uri="direct:attachUserPolicy"/>
    <setHeader name="CamelAwsIAMUsername">
        <constant>camel</constant>
    </setHeader>
    <setHeader name="CamelAwsIAMPolicyArn">
        <constant>arn:aws:iam::123456789012:policy/myPolicy</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=attachUserPolicy"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:attachUserPolicy
    steps:
      - setHeader:
          name: CamelAwsIAMUsername
          constant: camel
      - setHeader:
          name: CamelAwsIAMPolicyArn
          constant: "arn:aws:iam::123456789012:policy/myPolicy"
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: attachUserPolicy
```

-   detachUserPolicy: this operation will detach a policy from a user
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:detachUserPolicy")
    .setHeader("CamelAwsIAMUsername", constant("camel"))
    .setHeader("CamelAwsIAMPolicyArn", constant("arn:aws:iam::123456789012:policy/myPolicy"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=detachUserPolicy");
```

```xml
<route>
    <from uri="direct:detachUserPolicy"/>
    <setHeader name="CamelAwsIAMUsername">
        <constant>camel</constant>
    </setHeader>
    <setHeader name="CamelAwsIAMPolicyArn">
        <constant>arn:aws:iam::123456789012:policy/myPolicy</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=detachUserPolicy"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:detachUserPolicy
    steps:
      - setHeader:
          name: CamelAwsIAMUsername
          constant: camel
      - setHeader:
          name: CamelAwsIAMPolicyArn
          constant: "arn:aws:iam::123456789012:policy/myPolicy"
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: detachUserPolicy
```

-   attachGroupPolicy: this operation will attach a policy to a group
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:attachGroupPolicy")
    .setHeader("CamelAwsIAMGroupName", constant("myGroup"))
    .setHeader("CamelAwsIAMPolicyArn", constant("arn:aws:iam::123456789012:policy/myPolicy"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=attachGroupPolicy");
```

```xml
<route>
    <from uri="direct:attachGroupPolicy"/>
    <setHeader name="CamelAwsIAMGroupName">
        <constant>myGroup</constant>
    </setHeader>
    <setHeader name="CamelAwsIAMPolicyArn">
        <constant>arn:aws:iam::123456789012:policy/myPolicy</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=attachGroupPolicy"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:attachGroupPolicy
    steps:
      - setHeader:
          name: CamelAwsIAMGroupName
          constant: myGroup
      - setHeader:
          name: CamelAwsIAMPolicyArn
          constant: "arn:aws:iam::123456789012:policy/myPolicy"
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: attachGroupPolicy
```

-   detachGroupPolicy: this operation will detach a policy from a group
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:detachGroupPolicy")
    .setHeader("CamelAwsIAMGroupName", constant("myGroup"))
    .setHeader("CamelAwsIAMPolicyArn", constant("arn:aws:iam::123456789012:policy/myPolicy"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=detachGroupPolicy");
```

```xml
<route>
    <from uri="direct:detachGroupPolicy"/>
    <setHeader name="CamelAwsIAMGroupName">
        <constant>myGroup</constant>
    </setHeader>
    <setHeader name="CamelAwsIAMPolicyArn">
        <constant>arn:aws:iam::123456789012:policy/myPolicy</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=detachGroupPolicy"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:detachGroupPolicy
    steps:
      - setHeader:
          name: CamelAwsIAMGroupName
          constant: myGroup
      - setHeader:
          name: CamelAwsIAMPolicyArn
          constant: "arn:aws:iam::123456789012:policy/myPolicy"
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: detachGroupPolicy
```

-   attachRolePolicy: this operation will attach a policy to a role
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:attachRolePolicy")
    .setHeader("CamelAwsIAMRoleName", constant("myRole"))
    .setHeader("CamelAwsIAMPolicyArn", constant("arn:aws:iam::123456789012:policy/myPolicy"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=attachRolePolicy");
```

```xml
<route>
    <from uri="direct:attachRolePolicy"/>
    <setHeader name="CamelAwsIAMRoleName">
        <constant>myRole</constant>
    </setHeader>
    <setHeader name="CamelAwsIAMPolicyArn">
        <constant>arn:aws:iam::123456789012:policy/myPolicy</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=attachRolePolicy"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:attachRolePolicy
    steps:
      - setHeader:
          name: CamelAwsIAMRoleName
          constant: myRole
      - setHeader:
          name: CamelAwsIAMPolicyArn
          constant: "arn:aws:iam::123456789012:policy/myPolicy"
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: attachRolePolicy
```

-   detachRolePolicy: this operation will detach a policy from a role
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:detachRolePolicy")
    .setHeader("CamelAwsIAMRoleName", constant("myRole"))
    .setHeader("CamelAwsIAMPolicyArn", constant("arn:aws:iam::123456789012:policy/myPolicy"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=detachRolePolicy");
```

```xml
<route>
    <from uri="direct:detachRolePolicy"/>
    <setHeader name="CamelAwsIAMRoleName">
        <constant>myRole</constant>
    </setHeader>
    <setHeader name="CamelAwsIAMPolicyArn">
        <constant>arn:aws:iam::123456789012:policy/myPolicy</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=detachRolePolicy"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:detachRolePolicy
    steps:
      - setHeader:
          name: CamelAwsIAMRoleName
          constant: myRole
      - setHeader:
          name: CamelAwsIAMPolicyArn
          constant: "arn:aws:iam::123456789012:policy/myPolicy"
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: detachRolePolicy
```

#### Instance Profile Operations

-   createInstanceProfile: this operation will create an instance profile in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createInstanceProfile")
    .setHeader("CamelAwsIAMInstanceProfileName", constant("myInstanceProfile"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=createInstanceProfile");
```

```xml
<route>
    <from uri="direct:createInstanceProfile"/>
    <setHeader name="CamelAwsIAMInstanceProfileName">
        <constant>myInstanceProfile</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=createInstanceProfile"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createInstanceProfile
    steps:
      - setHeader:
          name: CamelAwsIAMInstanceProfileName
          constant: myInstanceProfile
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: createInstanceProfile
```

-   deleteInstanceProfile: this operation will delete an instance profile in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deleteInstanceProfile")
    .setHeader("CamelAwsIAMInstanceProfileName", constant("myInstanceProfile"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=deleteInstanceProfile");
```

```xml
<route>
    <from uri="direct:deleteInstanceProfile"/>
    <setHeader name="CamelAwsIAMInstanceProfileName">
        <constant>myInstanceProfile</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=deleteInstanceProfile"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:deleteInstanceProfile
    steps:
      - setHeader:
          name: CamelAwsIAMInstanceProfileName
          constant: myInstanceProfile
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: deleteInstanceProfile
```

-   getInstanceProfile: this operation will get an instance profile in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getInstanceProfile")
    .setHeader("CamelAwsIAMInstanceProfileName", constant("myInstanceProfile"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=getInstanceProfile");
```

```xml
<route>
    <from uri="direct:getInstanceProfile"/>
    <setHeader name="CamelAwsIAMInstanceProfileName">
        <constant>myInstanceProfile</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=getInstanceProfile"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getInstanceProfile
    steps:
      - setHeader:
          name: CamelAwsIAMInstanceProfileName
          constant: myInstanceProfile
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: getInstanceProfile
```

-   listInstanceProfiles: this operation will list the instance profiles in IAM
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:listInstanceProfiles")
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=listInstanceProfiles");
```

```xml
<route>
    <from uri="direct:listInstanceProfiles"/>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=listInstanceProfiles"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:listInstanceProfiles
    steps:
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: listInstanceProfiles
```

-   addRoleToInstanceProfile: this operation will add a role to an instance profile
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:addRoleToInstanceProfile")
    .setHeader("CamelAwsIAMInstanceProfileName", constant("myInstanceProfile"))
    .setHeader("CamelAwsIAMRoleName", constant("myRole"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=addRoleToInstanceProfile");
```

```xml
<route>
    <from uri="direct:addRoleToInstanceProfile"/>
    <setHeader name="CamelAwsIAMInstanceProfileName">
        <constant>myInstanceProfile</constant>
    </setHeader>
    <setHeader name="CamelAwsIAMRoleName">
        <constant>myRole</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=addRoleToInstanceProfile"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:addRoleToInstanceProfile
    steps:
      - setHeader:
          name: CamelAwsIAMInstanceProfileName
          constant: myInstanceProfile
      - setHeader:
          name: CamelAwsIAMRoleName
          constant: myRole
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: addRoleToInstanceProfile
```

-   removeRoleFromInstanceProfile: this operation will remove a role from an instance profile
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:removeRoleFromInstanceProfile")
    .setHeader("CamelAwsIAMInstanceProfileName", constant("myInstanceProfile"))
    .setHeader("CamelAwsIAMRoleName", constant("myRole"))
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=removeRoleFromInstanceProfile");
```

```xml
<route>
    <from uri="direct:removeRoleFromInstanceProfile"/>
    <setHeader name="CamelAwsIAMInstanceProfileName">
        <constant>myInstanceProfile</constant>
    </setHeader>
    <setHeader name="CamelAwsIAMRoleName">
        <constant>myRole</constant>
    </setHeader>
    <to uri="aws2-iam://test?iamClient=#amazonIAMClient&amp;operation=removeRoleFromInstanceProfile"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:removeRoleFromInstanceProfile
    steps:
      - setHeader:
          name: CamelAwsIAMInstanceProfileName
          constant: myInstanceProfile
      - setHeader:
          name: CamelAwsIAMRoleName
          constant: myRole
      - to:
          uri: aws2-iam://test
          parameters:
            iamClient: "#amazonIAMClient"
            operation: removeRoleFromInstanceProfile
```

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as a body. In AWS IAM, there are multiple operations you can submit, as an example for Create User request, you can do something like:

_Java-only: requires AWS SDK builder_

```java
from("direct:createUser")
     .setBody(CreateUserRequest.builder().userName("camel").build())
    .to("aws2-iam://test?iamClient=#amazonIAMClient&operation=createUser&pojoRequest=true")
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-iam</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.
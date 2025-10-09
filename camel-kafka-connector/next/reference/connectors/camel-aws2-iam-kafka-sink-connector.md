# camel-aws2-iam-kafka-connector sink configuration

Connector Description: Manage AWS IAM instances.

When using camel-aws2-iam-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws2-iam-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.aws2iam.CamelAws2iamSinkConnector
```

The camel-aws2-iam sink connector supports 41 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.sink.path.label** | **Required** Logical name. |  | HIGH |
| **camel.sink.endpoint.iamClient** | To use an existing configured AWS IAM client. |  | MEDIUM |
| **camel.sink.endpoint.operation** | 
The operation to perform. You can configure a default operation on the component level, or the operation as part of the endpoint, or via a message header with the key CamelAwsIAMOperation. One of: \[listAccessKeys\] \[createUser\] \[deleteUser\] \[getUser\] \[listUsers\] \[createAccessKey\] \[deleteAccessKey\] \[updateAccessKey\] \[createGroup\] \[deleteGroup\] \[listGroups\] \[addUserToGroup\] \[removeUserFromGroup\] \[createRole\] \[deleteRole\] \[getRole\] \[listRoles\] \[createPolicy\] \[deletePolicy\] \[getPolicy\] \[listPolicies\] \[attachUserPolicy\] \[detachUserPolicy\] \[attachGroupPolicy\] \[detachGroupPolicy\] \[attachRolePolicy\] \[detachRolePolicy\] \[createInstanceProfile\] \[deleteInstanceProfile\] \[getInstanceProfile\] \[listInstanceProfiles\] \[addRoleToInstanceProfile\] \[removeRoleFromInstanceProfile\].

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
    





 |  | MEDIUM |
| **camel.sink.endpoint.overrideEndpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | MEDIUM |
| **camel.sink.endpoint.pojoRequest** | If we want to use a POJO request as body or not. | false | MEDIUM |
| **camel.sink.endpoint.region** | 

The region in which IAM client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id() One of: \[ap-south-2\] \[ap-south-1\] \[eu-south-1\] \[eu-south-2\] \[us-gov-east-1\] \[me-central-1\] \[il-central-1\] \[ca-central-1\] \[eu-central-1\] \[us-iso-west-1\] \[eu-central-2\] \[us-west-1\] \[us-west-2\] \[af-south-1\] \[eu-north-1\] \[eu-west-3\] \[eu-west-2\] \[eu-west-1\] \[ap-northeast-3\] \[ap-northeast-2\] \[ap-northeast-1\] \[me-south-1\] \[sa-east-1\] \[ap-east-1\] \[cn-north-1\] \[us-gov-west-1\] \[ap-southeast-1\] \[ap-southeast-2\] \[us-iso-east-1\] \[ap-southeast-3\] \[ap-southeast-4\] \[us-east-1\] \[us-east-2\] \[cn-northwest-1\] \[us-isob-east-1\] \[aws-global\] \[aws-cn-global\] \[aws-us-gov-global\] \[aws-iso-global\] \[aws-iso-b-global\].

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
    





 | "aws-global" | MEDIUM |
| **camel.sink.endpoint.uriEndpointOverride** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | MEDIUM |
| **camel.sink.endpoint.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.sink.endpoint.proxyHost** | To define a proxy host when instantiating the IAM client. |  | MEDIUM |
| **camel.sink.endpoint.proxyPort** | To define a proxy port when instantiating the IAM client. |  | MEDIUM |
| **camel.sink.endpoint.proxyProtocol** | 

To define a proxy protocol when instantiating the IAM client One of: \[HTTP\] \[HTTPS\].

Enum values:

-   HTTP
    
-   HTTPS
    





 | "HTTPS" | MEDIUM |
| **camel.sink.endpoint.accessKey** | Amazon AWS Access Key. |  | MEDIUM |
| **camel.sink.endpoint.profileCredentialsName** | If using a profile credentials provider, this parameter will set the profile name. |  | MEDIUM |
| **camel.sink.endpoint.secretKey** | Amazon AWS Secret Key. |  | MEDIUM |
| **camel.sink.endpoint.sessionToken** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | MEDIUM |
| **camel.sink.endpoint.trustAllCertificates** | If we want to trust all certificates in case of overriding the endpoint. | false | MEDIUM |
| **camel.sink.endpoint.useDefaultCredentialsProvider** | Set whether the IAM client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | MEDIUM |
| **camel.sink.endpoint.useProfileCredentialsProvider** | Set whether the IAM client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.sink.endpoint.useSessionCredentials** | Set whether the IAM client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume a IAM role for doing operations in IAM. | false | MEDIUM |
| **camel.component.aws2-iam.configuration** | Component configuration. |  | MEDIUM |
| **camel.component.aws2-iam.iamClient** | To use an existing configured AWS IAM client. |  | MEDIUM |
| **camel.component.aws2-iam.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.component.aws2-iam.operation** | 

The operation to perform. You can configure a default operation on the component level, or the operation as part of the endpoint, or via a message header with the key CamelAwsIAMOperation. One of: \[listAccessKeys\] \[createUser\] \[deleteUser\] \[getUser\] \[listUsers\] \[createAccessKey\] \[deleteAccessKey\] \[updateAccessKey\] \[createGroup\] \[deleteGroup\] \[listGroups\] \[addUserToGroup\] \[removeUserFromGroup\] \[createRole\] \[deleteRole\] \[getRole\] \[listRoles\] \[createPolicy\] \[deletePolicy\] \[getPolicy\] \[listPolicies\] \[attachUserPolicy\] \[detachUserPolicy\] \[attachGroupPolicy\] \[detachGroupPolicy\] \[attachRolePolicy\] \[detachRolePolicy\] \[createInstanceProfile\] \[deleteInstanceProfile\] \[getInstanceProfile\] \[listInstanceProfiles\] \[addRoleToInstanceProfile\] \[removeRoleFromInstanceProfile\].

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
    





 |  | MEDIUM |
| **camel.component.aws2-iam.overrideEndpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | MEDIUM |
| **camel.component.aws2-iam.pojoRequest** | If we want to use a POJO request as body or not. | false | MEDIUM |
| **camel.component.aws2-iam.region** | 

The region in which IAM client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id() One of: \[ap-south-2\] \[ap-south-1\] \[eu-south-1\] \[eu-south-2\] \[us-gov-east-1\] \[me-central-1\] \[il-central-1\] \[ca-central-1\] \[eu-central-1\] \[us-iso-west-1\] \[eu-central-2\] \[us-west-1\] \[us-west-2\] \[af-south-1\] \[eu-north-1\] \[eu-west-3\] \[eu-west-2\] \[eu-west-1\] \[ap-northeast-3\] \[ap-northeast-2\] \[ap-northeast-1\] \[me-south-1\] \[sa-east-1\] \[ap-east-1\] \[cn-north-1\] \[us-gov-west-1\] \[ap-southeast-1\] \[ap-southeast-2\] \[us-iso-east-1\] \[ap-southeast-3\] \[ap-southeast-4\] \[us-east-1\] \[us-east-2\] \[cn-northwest-1\] \[us-isob-east-1\] \[aws-global\] \[aws-cn-global\] \[aws-us-gov-global\] \[aws-iso-global\] \[aws-iso-b-global\].

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
    





 | "aws-global" | MEDIUM |
| **camel.component.aws2-iam.uriEndpointOverride** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | MEDIUM |
| **camel.component.aws2-iam.autowiredEnabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | MEDIUM |
| **camel.component.aws2-iam.healthCheckConsumerEnabled** | Used for enabling or disabling all consumer based health checks from this component. | true | MEDIUM |
| **camel.component.aws2-iam.healthCheckProducerEnabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | MEDIUM |
| **camel.component.aws2-iam.proxyHost** | To define a proxy host when instantiating the IAM client. |  | MEDIUM |
| **camel.component.aws2-iam.proxyPort** | To define a proxy port when instantiating the IAM client. |  | MEDIUM |
| **camel.component.aws2-iam.proxyProtocol** | 

To define a proxy protocol when instantiating the IAM client One of: \[HTTP\] \[HTTPS\].

Enum values:

-   HTTP
    
-   HTTPS
    





 | "HTTPS" | MEDIUM |
| **camel.component.aws2-iam.accessKey** | Amazon AWS Access Key. |  | MEDIUM |
| **camel.component.aws2-iam.profileCredentialsName** | If using a profile credentials provider, this parameter will set the profile name. |  | MEDIUM |
| **camel.component.aws2-iam.secretKey** | Amazon AWS Secret Key. |  | MEDIUM |
| **camel.component.aws2-iam.sessionToken** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | MEDIUM |
| **camel.component.aws2-iam.trustAllCertificates** | If we want to trust all certificates in case of overriding the endpoint. | false | MEDIUM |
| **camel.component.aws2-iam.useDefaultCredentialsProvider** | Set whether the IAM client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | MEDIUM |
| **camel.component.aws2-iam.useProfileCredentialsProvider** | Set whether the IAM client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.component.aws2-iam.useSessionCredentials** | Set whether the IAM client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume a IAM role for doing operations in IAM. | false | MEDIUM |

The camel-aws2-iam sink connector has no converters out of the box.

The camel-aws2-iam sink connector has no transforms out of the box.

The camel-aws2-iam sink connector has no aggregation strategies out of the box.
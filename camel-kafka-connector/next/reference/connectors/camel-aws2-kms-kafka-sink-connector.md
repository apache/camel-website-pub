# camel-aws2-kms-kafka-connector sink configuration

Connector Description: Manage keys stored in AWS KMS instances.

When using camel-aws2-kms-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws2-kms-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.aws2kms.CamelAws2kmsSinkConnector
```

The camel-aws2-kms sink connector supports 39 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.sink.path.label** | **Required** Logical name. |  | HIGH |
| **camel.sink.endpoint.operation** | 
**Required** The operation to perform One of: \[listKeys\] \[createKey\] \[disableKey\] \[scheduleKeyDeletion\] \[describeKey\] \[enableKey\].

Enum values:

-   listKeys
    
-   createKey
    
-   disableKey
    
-   scheduleKeyDeletion
    
-   describeKey
    
-   enableKey
    





 |  | HIGH |
| **camel.sink.endpoint.overrideEndpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | MEDIUM |
| **camel.sink.endpoint.pojoRequest** | If we want to use a POJO request as body or not. | false | MEDIUM |
| **camel.sink.endpoint.region** | 

The region in which EKS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id() One of: \[ap-south-2\] \[ap-south-1\] \[eu-south-1\] \[eu-south-2\] \[us-gov-east-1\] \[me-central-1\] \[il-central-1\] \[ca-central-1\] \[eu-central-1\] \[us-iso-west-1\] \[eu-central-2\] \[eu-isoe-west-1\] \[us-west-1\] \[us-west-2\] \[af-south-1\] \[eu-north-1\] \[eu-west-3\] \[eu-west-2\] \[eu-west-1\] \[ap-northeast-3\] \[ap-northeast-2\] \[ap-northeast-1\] \[me-south-1\] \[sa-east-1\] \[ap-east-1\] \[cn-north-1\] \[ca-west-1\] \[us-gov-west-1\] \[ap-southeast-1\] \[ap-southeast-2\] \[us-iso-east-1\] \[ap-southeast-3\] \[ap-southeast-4\] \[us-east-1\] \[us-east-2\] \[cn-northwest-1\] \[us-isob-east-1\] \[aws-global\] \[aws-cn-global\] \[aws-us-gov-global\] \[aws-iso-global\] \[aws-iso-b-global\].

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
    





 |  | MEDIUM |
| **camel.sink.endpoint.uriEndpointOverride** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | MEDIUM |
| **camel.sink.endpoint.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.sink.endpoint.kmsClient** | To use an existing configured AWS KMS client. |  | MEDIUM |
| **camel.sink.endpoint.proxyHost** | To define a proxy host when instantiating the KMS client. |  | MEDIUM |
| **camel.sink.endpoint.proxyPort** | To define a proxy port when instantiating the KMS client. |  | MEDIUM |
| **camel.sink.endpoint.proxyProtocol** | 

To define a proxy protocol when instantiating the KMS client One of: \[HTTP\] \[HTTPS\].

Enum values:

-   HTTP
    
-   HTTPS
    





 | "HTTPS" | MEDIUM |
| **camel.sink.endpoint.accessKey** | Amazon AWS Access Key. |  | MEDIUM |
| **camel.sink.endpoint.profileCredentialsName** | If using a profile credentials provider, this parameter will set the profile name. |  | MEDIUM |
| **camel.sink.endpoint.secretKey** | Amazon AWS Secret Key. |  | MEDIUM |
| **camel.sink.endpoint.sessionToken** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | MEDIUM |
| **camel.sink.endpoint.trustAllCertificates** | If we want to trust all certificates in case of overriding the endpoint. | false | MEDIUM |
| **camel.sink.endpoint.useDefaultCredentialsProvider** | Set whether the KMS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | MEDIUM |
| **camel.sink.endpoint.useProfileCredentialsProvider** | Set whether the KMS client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.sink.endpoint.useSessionCredentials** | Set whether the KMS client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume a IAM role for doing operations in KMS. | false | MEDIUM |
| **camel.component.aws2-kms.configuration** | Component configuration. |  | MEDIUM |
| **camel.component.aws2-kms.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.component.aws2-kms.operation** | 

**Required** The operation to perform One of: \[listKeys\] \[createKey\] \[disableKey\] \[scheduleKeyDeletion\] \[describeKey\] \[enableKey\].

Enum values:

-   listKeys
    
-   createKey
    
-   disableKey
    
-   scheduleKeyDeletion
    
-   describeKey
    
-   enableKey
    





 |  | HIGH |
| **camel.component.aws2-kms.overrideEndpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | MEDIUM |
| **camel.component.aws2-kms.pojoRequest** | If we want to use a POJO request as body or not. | false | MEDIUM |
| **camel.component.aws2-kms.region** | 

The region in which EKS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id() One of: \[ap-south-2\] \[ap-south-1\] \[eu-south-1\] \[eu-south-2\] \[us-gov-east-1\] \[me-central-1\] \[il-central-1\] \[ca-central-1\] \[eu-central-1\] \[us-iso-west-1\] \[eu-central-2\] \[eu-isoe-west-1\] \[us-west-1\] \[us-west-2\] \[af-south-1\] \[eu-north-1\] \[eu-west-3\] \[eu-west-2\] \[eu-west-1\] \[ap-northeast-3\] \[ap-northeast-2\] \[ap-northeast-1\] \[me-south-1\] \[sa-east-1\] \[ap-east-1\] \[cn-north-1\] \[ca-west-1\] \[us-gov-west-1\] \[ap-southeast-1\] \[ap-southeast-2\] \[us-iso-east-1\] \[ap-southeast-3\] \[ap-southeast-4\] \[us-east-1\] \[us-east-2\] \[cn-northwest-1\] \[us-isob-east-1\] \[aws-global\] \[aws-cn-global\] \[aws-us-gov-global\] \[aws-iso-global\] \[aws-iso-b-global\].

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
    





 |  | MEDIUM |
| **camel.component.aws2-kms.uriEndpointOverride** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | MEDIUM |
| **camel.component.aws2-kms.autowiredEnabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | MEDIUM |
| **camel.component.aws2-kms.kmsClient** | To use an existing configured AWS KMS client. |  | MEDIUM |
| **camel.component.aws2-kms.proxyHost** | To define a proxy host when instantiating the KMS client. |  | MEDIUM |
| **camel.component.aws2-kms.proxyPort** | To define a proxy port when instantiating the KMS client. |  | MEDIUM |
| **camel.component.aws2-kms.proxyProtocol** | 

To define a proxy protocol when instantiating the KMS client One of: \[HTTP\] \[HTTPS\].

Enum values:

-   HTTP
    
-   HTTPS
    





 | "HTTPS" | MEDIUM |
| **camel.component.aws2-kms.accessKey** | Amazon AWS Access Key. |  | MEDIUM |
| **camel.component.aws2-kms.profileCredentialsName** | If using a profile credentials provider, this parameter will set the profile name. |  | MEDIUM |
| **camel.component.aws2-kms.secretKey** | Amazon AWS Secret Key. |  | MEDIUM |
| **camel.component.aws2-kms.sessionToken** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | MEDIUM |
| **camel.component.aws2-kms.trustAllCertificates** | If we want to trust all certificates in case of overriding the endpoint. | false | MEDIUM |
| **camel.component.aws2-kms.useDefaultCredentialsProvider** | Set whether the KMS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | MEDIUM |
| **camel.component.aws2-kms.useProfileCredentialsProvider** | Set whether the KMS client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.component.aws2-kms.useSessionCredentials** | Set whether the KMS client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume a IAM role for doing operations in KMS. | false | MEDIUM |

The camel-aws2-kms sink connector has no converters out of the box.

The camel-aws2-kms sink connector has no transforms out of the box.

The camel-aws2-kms sink connector has no aggregation strategies out of the box.
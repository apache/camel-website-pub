# AWS Security Hub

**Since Camel 4.18**

**Only producer is supported**

The AWS Security Hub component allows you to interact with [AWS Security Hub](https://aws.amazon.com/security-hub/) to manage security findings.

AWS Security Hub provides a comprehensive view of your security state in AWS and helps you check your environment against security industry standards and best practices.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Security Hub. More information is available at [Amazon Security Hub](https://aws.amazon.com/security-hub/).

## URI Format

aws-security-hub://label\[?options\]

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

The AWS Security Hub component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | SecurityHubConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   batchImportFindings
    
-   getFindings
    
-   batchUpdateFindings
    
-   getFindingHistory
    
-   describeHub
    
-   listEnabledProductsForImport
    
-   getFindingAggregator
    





 | batchImportFindings | SecurityHubOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the Security Hub client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **securityHubClient** (advanced) | **Autowired** To use an existing configured AWS Security Hub client. |  | SecurityHubClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Security Hub client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Security Hub client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Security Hub client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Security Hub client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Security Hub client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Security Hub client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Security Hub. | false | boolean |

## Endpoint Options

The AWS Security Hub endpoint is configured using URI syntax:

aws-security-hub:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (18 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   batchImportFindings
    
-   getFindings
    
-   batchUpdateFindings
    
-   getFindingHistory
    
-   describeHub
    
-   listEnabledProductsForImport
    
-   getFindingAggregator
    





 | batchImportFindings | SecurityHubOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the Security Hub client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **securityHubClient** (advanced) | **Autowired** To use an existing configured AWS Security Hub client. |  | SecurityHubClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Security Hub client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Security Hub client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Security Hub client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Security Hub client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Security Hub client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Security Hub client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Security Hub. | false | boolean |

## Message Headers

The AWS Security Hub component supports 22 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsSecurityHubOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsSecurityHubFindings** (producer) Constant: [`FINDINGS`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#FINDINGS) | The list of findings to import. |  | List |
| **CamelAwsSecurityHubFindingIdentifiers** (producer) Constant: [`FINDING_IDENTIFIERS`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#FINDING_IDENTIFIERS) | The finding identifiers for batch update. |  | List |
| **CamelAwsSecurityHubFilters** (producer) Constant: [`FILTERS`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#FILTERS) | The filters to apply when retrieving findings. |  | AwsSecurityFindingFilters |
| **CamelAwsSecurityHubNote** (producer) Constant: [`NOTE`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#NOTE) | The note to add to findings during update. |  | NoteUpdate |
| **CamelAwsSecurityHubSeverity** (producer) Constant: [`SEVERITY`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#SEVERITY) | The severity to set on findings during update. |  | SeverityUpdate |
| **CamelAwsSecurityHubWorkflow** (producer) Constant: [`WORKFLOW`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#WORKFLOW) | The workflow status to set on findings. |  | WorkflowUpdate |
| **CamelAwsSecurityHubVerificationState** (producer) Constant: [`VERIFICATION_STATE`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#VERIFICATION_STATE) | The verification state to set on findings. |  | String |
| **CamelAwsSecurityHubConfidence** (producer) Constant: [`CONFIDENCE`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#CONFIDENCE) | The confidence level to set on findings. |  | Integer |
| **CamelAwsSecurityHubCriticality** (producer) Constant: [`CRITICALITY`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#CRITICALITY) | The criticality level to set on findings. |  | Integer |
| **CamelAwsSecurityHubUserDefinedFields** (producer) Constant: [`USER_DEFINED_FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#USER_DEFINED_FIELDS) | User-defined fields to add to findings. |  | Map |
| **CamelAwsSecurityHubRelatedFindings** (producer) Constant: [`RELATED_FINDINGS`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#RELATED_FINDINGS) | Related findings to associate. |  | List |
| **CamelAwsSecurityHubTypes** (producer) Constant: [`TYPES`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#TYPES) | The types to assign to findings. |  | List |
| **CamelAwsSecurityHubNextToken** (getFindings listEnabledProductsForImport getFindingHistory) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#NEXT_TOKEN) | The token for the next set of results. |  | String |
| **CamelAwsSecurityHubMaxResults** (getFindings) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#MAX_RESULTS) | The maximum number of results to return. |  | Integer |
| **CamelAwsSecurityHubFailedCount** (batchImportFindings) Constant: [`FAILED_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#FAILED_COUNT) | The count of findings that failed to import. |  | Integer |
| **CamelAwsSecurityHubSuccessCount** (batchImportFindings) Constant: [`SUCCESS_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#SUCCESS_COUNT) | The count of findings that were successfully imported. |  | Integer |
| **CamelAwsSecurityHubUnprocessedFindings** (batchUpdateFindings) Constant: [`UNPROCESSED_FINDINGS`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#UNPROCESSED_FINDINGS) | The list of findings that were not updated. |  | List |
| **CamelAwsSecurityHubProcessedFindings** (batchUpdateFindings) Constant: [`PROCESSED_FINDINGS`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#PROCESSED_FINDINGS) | The list of findings that were updated successfully. |  | List |
| **CamelAwsSecurityHubFindingId** (getFindingHistory) Constant: [`FINDING_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#FINDING_ID) | The finding ID to get history for. |  | String |
| **CamelAwsSecurityHubProductArn** (getFindingHistory) Constant: [`PRODUCT_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#PRODUCT_ARN) | The product ARN for the finding. |  | String |
| **CamelAwsSecurityHubFindingAggregatorArn** (getFindingAggregator) Constant: [`FINDING_AGGREGATOR_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws-security-hub/latest/org/apache/camel/component/aws/securityhub/SecurityHubConstants.html#FINDING_AGGREGATOR_ARN) | The ARN of the finding aggregator to retrieve. |  | String |

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

### AWS Security Hub Producer operations

Camel-AWS Security Hub component provides the following operation on the producer side:

-   batchImportFindings
    
-   getFindings
    
-   batchUpdateFindings
    
-   getFindingHistory
    
-   describeHub
    
-   listEnabledProductsForImport
    

#### BatchImportFindings

Import security findings into Security Hub. This is the primary way to send findings from custom integrations.

```java
from("direct:importFindings")
    .process(exchange -> {
        AwsSecurityFinding finding = AwsSecurityFinding.builder()
            .schemaVersion("2018-10-08")
            .id("my-finding-id")
            .productArn("arn:aws:securityhub:us-east-1:123456789012:product/123456789012/default")
            .generatorId("my-generator")
            .awsAccountId("123456789012")
            .types("Software and Configuration Checks/Vulnerabilities/CVE")
            .createdAt("2024-01-15T00:00:00.000Z")
            .updatedAt("2024-01-15T00:00:00.000Z")
            .severity(Severity.builder().label(SeverityLabel.HIGH).build())
            .title("Critical vulnerability found")
            .description("A critical vulnerability was detected")
            .resources(Resource.builder()
                .type("AwsEc2Instance")
                .id("arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0")
                .build())
            .build();
        exchange.getIn().setBody(List.of(finding));
    })
    .to("aws-security-hub://findings?operation=batchImportFindings")
    .to("mock:result");
```

#### GetFindings

Retrieve security findings from Security Hub with optional filtering.

```java
from("direct:getFindings")
    .process(exchange -> {
        AwsSecurityFindingFilters filters = AwsSecurityFindingFilters.builder()
            .severityLabel(StringFilter.builder()
                .comparison(StringFilterComparison.EQUALS)
                .value("CRITICAL")
                .build())
            .build();
        exchange.getIn().setHeader(SecurityHubConstants.FILTERS, filters);
        exchange.getIn().setHeader(SecurityHubConstants.MAX_RESULTS, 10);
    })
    .to("aws-security-hub://findings?operation=getFindings")
    .to("mock:result");
```

#### BatchUpdateFindings

Update security findings with notes, severity changes, workflow status, etc.

```java
from("direct:updateFindings")
    .process(exchange -> {
        List<AwsSecurityFindingIdentifier> identifiers = List.of(
            AwsSecurityFindingIdentifier.builder()
                .id("my-finding-id")
                .productArn("arn:aws:securityhub:us-east-1:123456789012:product/123456789012/default")
                .build()
        );
        exchange.getIn().setHeader(SecurityHubConstants.FINDING_IDENTIFIERS, identifiers);

        NoteUpdate note = NoteUpdate.builder()
            .text("Reviewed and confirmed as false positive")
            .updatedBy("security-team")
            .build();
        exchange.getIn().setHeader(SecurityHubConstants.NOTE, note);

        WorkflowUpdate workflow = WorkflowUpdate.builder()
            .status(WorkflowStatus.RESOLVED)
            .build();
        exchange.getIn().setHeader(SecurityHubConstants.WORKFLOW, workflow);
    })
    .to("aws-security-hub://findings?operation=batchUpdateFindings")
    .to("mock:result");
```

#### DescribeHub

Get information about the Security Hub configuration in your account.

```java
from("direct:describeHub")
    .to("aws-security-hub://hub?operation=describeHub")
    .to("mock:result");
```

### OCSF Integration

AWS Security Hub uses the [Open Cybersecurity Schema Framework (OCSF)](https://schema.ocsf.io/) for findings. You can use the Camel OCSF DataFormat to work with security events in a vendor-neutral format, then convert them for import into Security Hub.

```java
from("direct:ocsfToSecurityHub")
    .unmarshal().ocsf(DetectionFinding.class)
    .process(exchange -> {
        DetectionFinding ocsf = exchange.getIn().getBody(DetectionFinding.class);
        // Convert OCSF finding to AWS Security Finding format
        AwsSecurityFinding finding = convertToAwsFinding(ocsf);
        exchange.getIn().setBody(List.of(finding));
    })
    .to("aws-security-hub://findings?operation=batchImportFindings");
```

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws-security-hub</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.
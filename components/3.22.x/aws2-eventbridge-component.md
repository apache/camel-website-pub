# AWS Eventbridge

**Since Camel 3.6**

**Only producer is supported**

The AWS2 Eventbridge component supports assumeRole operation. [AWS Eventbridge](https://aws.amazon.com/eventbridge/).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Eventbridge. More information is available at [Amazon Eventbridge](https://aws.amazon.com/eventbridge/).

> **Note**
> To create a rule that triggers on an action by an AWS service that does not emit events, you can base the rule on API calls made by that service. The API calls are recorded by AWS CloudTrail, so you’ll need to have CloudTrail enabled. For more information [Services Supported by CloudTrail Event History](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.md).

## URI Format

aws2-eventbridge://label\[?options\]

You can append query options to the URI in the following format, ?options=value&option2=value&…​

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The AWS Eventbridge component supports 17 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | EventbridgeConfiguration |
| **eventbridgeClient** (producer) | **Autowired** To use a existing configured AWS Eventbridge as client. |  | EventBridgeClient |
| **eventPatternFile** (producer) | EventPattern File. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   putRule
    
-   putTargets
    
-   removeTargets
    
-   deleteRule
    
-   enableRule
    
-   disableRule
    
-   describeRule
    
-   listRules
    
-   listTargetsByRule
    
-   listRuleNamesByTarget
    
-   putEvent
    





 | putRule | EventbridgeOperations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the Eventbridge client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the Eventbridge client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the Eventbridge client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which Eventbridge client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Eventbridge client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS Eventbridge endpoint is configured using URI syntax:

aws2-eventbridge://eventbusNameOrArn

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **eventbusNameOrArn** (producer) | **Required** Event bus name or ARN. |  | String |

### Query Parameters (15 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **eventbridgeClient** (producer) | **Autowired** To use a existing configured AWS Eventbridge as client. |  | EventBridgeClient |
| **eventPatternFile** (producer) | EventPattern File. |  | String |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   putRule
    
-   putTargets
    
-   removeTargets
    
-   deleteRule
    
-   enableRule
    
-   disableRule
    
-   describeRule
    
-   listRules
    
-   listTargetsByRule
    
-   listRuleNamesByTarget
    
-   putEvent
    





 | putRule | EventbridgeOperations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the Eventbridge client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the Eventbridge client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the Eventbridge client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which Eventbridge client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Eventbridge client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

### Static credentials vs Default Credential Provider

You have the possibility of avoiding the usage of explicit static credentials, by specifying the useDefaultCredentialsProvider option and set it to true.

-   Java system properties - aws.accessKeyId and aws.secretKey
    
-   Environment variables - AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable AWS\_CONTAINER\_CREDENTIALS\_RELATIVE\_URI is set.
    
-   Amazon EC2 Instance profile credentials.
    

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

## Message Headers

The AWS Eventbridge component supports 10 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsEventbridgeOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsEventbridgeRuleName** (producer) Constant: [`RULE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#RULE_NAME) | The name of the rule. |  | String |
| **CamelAwsEventbridgeRuleNamePrefix** (producer) Constant: [`RULE_NAME_PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#RULE_NAME_PREFIX) | The prefix matching the rule name. |  | String |
| **CamelAwsEventbridgeEventPattern** (producer) Constant: [`EVENT_PATTERN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#EVENT_PATTERN) | The event pattern. |  | String |
| **CamelAwsEventbridgeTargets** (producer) Constant: [`TARGETS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#TARGETS) | The targets to update or add to the rule. |  | Collection |
| **CamelAwsEventbridgeTargetsIds** (producer) Constant: [`TARGETS_IDS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#TARGETS_IDS) | The IDs of the targets to remove from the rule. |  | Collection |
| **CamelAwsEventbridgeTargetArn** (producer) Constant: [`TARGET_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#TARGET_ARN) | The Amazon Resource Name (ARN) of the target resource. |  | String |
| **CamelAwsEventbridgeResourcesArn** (producer) Constant: [`EVENT_RESOURCES_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#EVENT_RESOURCES_ARN) | Comma separated list of Amazon Resource Names (ARN) of the resources related to Event. |  | String |
| **CamelAwsEventbridgeSource** (producer) Constant: [`EVENT_SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#EVENT_SOURCE) | The source related to Event. |  | String |
| **CamelAwsEventbridgeDetailType** (producer) Constant: [`EVENT_DETAIL_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#EVENT_DETAIL_TYPE) | The detail type related to Event. |  | String |

### AWS2-Eventbridge Producer operations

Camel-AWS2-Eventbridge component provides the following operation on the producer side:

-   putRule
    
-   putTargets
    
-   removeTargets
    
-   deleteRule
    
-   enableRule
    
-   disableRule
    
-   listRules
    
-   describeRule
    
-   listTargetsByRule
    
-   listRuleNamesByTarget
    
-   putEvent
    
-   PutRule: this operation create a rule related to an eventbus
    

```java
  from("direct:putRule").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=putRule&eventPatternFile=file:src/test/resources/eventpattern.json")
  .to("mock:result");
```

This operation will create a rule named firstrule and it will use a json file for defining the EventPattern.

-   PutTargets: this operation will add a target to the rule
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
          Target target = Target.builder().id("sqs-queue").arn("arn:aws:sqs:eu-west-1:780410022472:camel-connector-test")
                .build();
          List<Target> targets = new ArrayList<Target>();
          targets.add(target);
          exchange.getIn().setHeader(EventbridgeConstants.TARGETS, targets);
      }
  })
  .to("aws2-eventbridge://test?operation=putTargets")
  .to("mock:result");
```

This operation will add the target sqs-queue with the arn reported to the targets of the firstrule rule.

-   RemoveTargets: this operation will remove a collection of target from the rule
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
          List<String> ids = new ArrayList<String>();
          targets.add("sqs-queue");
          exchange.getIn().setHeader(EventbridgeConstants.TARGETS_IDS, targets);
      }
  })
  .to("aws2-eventbridge://test?operation=removeTargets")
  .to("mock:result");
```

This operation will remove the target sqs-queue from the firstrule rule.

-   DeleteRule: this operation will delete a rule related to an eventbus
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=deleteRule")
  .to("mock:result");
```

This operation will remove the firstrule rule from the test eventbus.

-   EnableRule: this operation will enable a rule related to an eventbus
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=enableRule")
  .to("mock:result");
```

This operation will enable the firstrule rule from the test eventbus.

-   DisableRule: this operation will disable a rule related to an eventbus
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=disableRule")
  .to("mock:result");
```

This operation will disable the firstrule rule from the test eventbus.

-   ListRules: this operation will list all the rules related to an eventbus with prefix first
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME_PREFIX, "first");
      }
  })
  .to("aws2-eventbridge://test?operation=listRules")
  .to("mock:result");
```

This operation will list all the rules with prefix first from the test eventbus.

-   DescribeRule: this operation will describe a specified rule related to an eventbus
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=describeRule")
  .to("mock:result");
```

This operation will describe the firstrule rule from the test eventbus.

-   ListTargetsByRule: this operation will return a list of targets associated with a rule
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=listTargetsByRule")
  .to("mock:result");
```

this operation will return a list of targets associated with the firstrule rule.

-   ListRuleNamesByTarget: this operation will return a list of rule associated with a target
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.TARGET_ARN, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=listRuleNamesByTarget")
  .to("mock:result");
```

this operation will return a list of rule associated with a target.

-   PutEvent: this operation will send an event to the Servicebus
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
                exchange.getIn().setHeader(EventbridgeConstants.EVENT_RESOURCES_ARN, "arn:aws:sqs:eu-west-1:780410022472:camel-connector-test");
                exchange.getIn().setHeader(EventbridgeConstants.EVENT_SOURCE, "com.pippo");
                exchange.getIn().setHeader(EventbridgeConstants.EVENT_DETAIL_TYPE, "peppe");
                exchange.getIn().setBody("Test Event");
      }
  })
  .to("aws2-eventbridge://test?operation=putEvent")
  .to("mock:result");
```

this operation will return a list of entries with related ID sent to servicebus.

## Updating the rule

To update a rule you’ll need to perform the putRule operation again. There are no explicit update rule operation in the Java SDK.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-eventbridge</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-eventbridge with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-eventbridge-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 18 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-eventbridge.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-eventbridge.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-eventbridge.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.eventbridge.EventbridgeConfiguration type. |  | EventbridgeConfiguration |
| **camel.component.aws2-eventbridge.enabled** | Whether to enable auto configuration of the aws2-eventbridge component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-eventbridge.event-pattern-file** | EventPattern File. |  | String |
| **camel.component.aws2-eventbridge.eventbridge-client** | To use a existing configured AWS Eventbridge as client. The option is a software.amazon.awssdk.services.eventbridge.EventBridgeClient type. |  | EventBridgeClient |
| **camel.component.aws2-eventbridge.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-eventbridge.operation** | The operation to perform. |  | EventbridgeOperations |
| **camel.component.aws2-eventbridge.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-eventbridge.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-eventbridge.proxy-host** | To define a proxy host when instantiating the Eventbridge client. |  | String |
| **camel.component.aws2-eventbridge.proxy-port** | To define a proxy port when instantiating the Eventbridge client. |  | Integer |
| **camel.component.aws2-eventbridge.proxy-protocol** | To define a proxy protocol when instantiating the Eventbridge client. |  | Protocol |
| **camel.component.aws2-eventbridge.region** | The region in which Eventbridge client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-eventbridge.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-eventbridge.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-eventbridge.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-eventbridge.use-default-credentials-provider** | Set whether the Eventbridge client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
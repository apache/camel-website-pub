# ![aws redshift sink](_images/kamelets/aws-redshift-sink.svg) AWS Redshift Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to an AWS Redshift Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

## Configuration Options

The following table summarizes the configuration options available for the `aws-redshift-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the AWS Redshift Database. | string |  |  |
| **password** | Password | **Required** The password to access a secured AWS Redshift Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the AWS Redshift Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The server name for the data source. | string |  | localhost |
| **username** | Username | **Required** The username to access a secured AWS Redshift Database. | string |  |  |
| **serverPort** | Server Port | The server port for the AWS RedShi data source. | string | 5439 |  |

## Dependencies

At runtime, the `aws-redshift-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:com.amazon.redshift:redshift-jdbc42:2.2.8
    
-   mvn:org.apache.commons:commons-dbcp2:2.14.0
    

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
            uri: "kamelet:aws-redshift-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Redshift Sink Kamelet Description

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

### Expected Data format for sink

The Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters. For example, here is a query:

```sql
'INSERT INTO accounts (username,city) VALUES (:#username,:#city)'
```

Here is example input for the example query:

```json
'{ "username":"oscerd", "city":"Rome"}'
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-redshift-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-redshift-sink.kamelet.yaml)
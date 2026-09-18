# ![jira source](_images/kamelets/jira-source.svg) Jira Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive notifications about new issues from Jira.

## Configuration Options

The following table summarizes the configuration options available for the `jira-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **jiraUrl** | Jira URL | **Required** The URL of your instance of Jira. | string |  | http://my\_jira.com:8081 |
| **jql** | JQL | A query to filter issues. | string |  | project=MyProject |
| **password** | Password | The password to access Jira. | string |  |  |
| **personal-token** | Personal Token | Personal Token. | string |  |  |
| **username** | Username | The username to access Jira. | string |  |  |

## Dependencies

At runtime, the `jira-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:jira
    
-   camel:kamelet
    
-   mvn:com.fasterxml.jackson.datatype:jackson-datatype-joda:2.12.5
    

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
      uri: "kamelet:jira-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Jira Source Kamelet Description

### Authentication methods

This Kamelet uses basic authentication (username and password) to connect to JIRA. You need to provide:

-   Username and password for JIRA authentication
    
-   JIRA instance URL
    

### Output format

The Kamelet receives notifications about new issues from JIRA and produces the issue data in JSON format.

### Configuration

The Kamelet requires the following parameters:

-   `jiraUrl`: The URL of your instance of JIRA
    
-   `username`: The username to access JIRA
    
-   `password`: The password to access JIRA
    
-   `jql`: The JQL query to filter issues
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: jira-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: jira-source
    properties:
      jiraUrl: "http://my_jira.com:8081"
      username: "{{username}}"
      password: "{{password}}"
      jql: "project = TEST"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-source.kamelet.yaml)
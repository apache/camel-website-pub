# ![jira add comment sink](_images/kamelets/jira-add-comment-sink.svg) Jira Add Comment Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Add a new comment to an existing issue in Jira.

## Configuration Options

The following table summarizes the configuration options available for the `jira-add-comment-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **jiraUrl** | Jira URL | **Required** The URL of your instance of Jira. | string |  | http://my\_jira.com:8081 |
| **password** | Password | The password to access Jira. | string |  |  |
| **personal-token** | Personal Token | Personal Token. | string |  |  |
| **username** | Username | The username to access Jira. | string |  |  |

## Dependencies

At runtime, the `jira-add-comment-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:jira-add-comment-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Jira Add Comment Sink Kamelet Description

### JIRA Operations

This Kamelet adds comments to existing JIRA issues.

### Input Format

Expects JSON-formatted data containing the comment information.

### Authentication

Supports multiple authentication methods: - **Username and Password**: Basic authentication - **Personal Token**: API token authentication

### Required Configuration

-   **JIRA URL**: The URL of your JIRA instance
    

### Optional Headers

-   `ce-issueKey`: Specify the JIRA issue key to add the comment to
    

### Usage

The Kamelet sends the comment data to the specified JIRA issue, enabling automated comment addition to issues based on events or data processing.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-add-comment-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-add-comment-sink.kamelet.yaml)
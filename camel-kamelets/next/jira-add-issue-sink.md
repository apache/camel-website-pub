# ![jira add issue sink](_images/kamelets/jira-add-issue-sink.svg) Jira Add Issue Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Add a new issue to Jira.

## Configuration Options

The following table summarizes the configuration options available for the `jira-add-issue-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **jiraUrl** | Jira URL | **Required** The URL of your instance of Jira. | string |  | http://my\_jira.com:8081 |
| **password** | Password | The password to access Jira. | string |  |  |
| **personal-token** | Personal Token | Personal Token. | string |  |  |
| **username** | Username | The username to access Jira. | string |  |  |

## Dependencies

At runtime, the `jira-add-issue-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:jira-add-issue-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Jira Add Issue Sink Kamelet Description

### JIRA Operations

This Kamelet creates new issues in JIRA.

### Input Format

Expects JSON-formatted data containing the issue information.

### Authentication

Supports multiple authentication methods: - **Username and Password**: Basic authentication - **Personal Token**: API token authentication

### Required Configuration

-   **JIRA URL**: The URL of your JIRA instance
    

### Issue Configuration Headers

The Kamelet supports various headers to configure issue details: - `ce-projectKey`: JIRA project key - `ce-issueTypeName`: Type of issue to create - `ce-issueSummary`: Issue summary/title - `ce-issueAssignee`: Assignee for the issue - `ce-issuePriorityName`: Priority level - `ce-issueComponents`: Issue components - `ce-issueDescription`: Detailed description

### Usage

The Kamelet creates new JIRA issues with the specified details, enabling automated issue creation based on events or data processing workflows.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-add-issue-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-add-issue-sink.kamelet.yaml)
# ![jira update issue sink](_images/kamelets/jira-update-issue-sink.svg) Jira Update Issue Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Update fields of an existing issue in Jira.

## Configuration Options

The following table summarizes the configuration options available for the `jira-update-issue-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **jiraUrl** | Jira URL | **Required** The URL of your instance of Jira. | string |  | http://my\_jira.com:8081 |
| **password** | Password | The password to access Jira. | string |  |  |
| **personal-token** | Personal Token | Personal Token. | string |  |  |
| **username** | Username | The username to access Jira. | string |  |  |

## Dependencies

At runtime, the `jira-update-issue-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:jira-update-issue-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Jira Update Issue Sink Kamelet Description

### JIRA Operations

This Kamelet updates fields of existing JIRA issues.

### Input Format

Expects JSON-formatted data containing the updated issue information.

### Authentication

Supports multiple authentication methods: - **Username and Password**: Basic authentication - **Personal Token**: API token authentication

### Required Configuration

-   **JIRA URL**: The URL of your JIRA instance
    

### Issue Update Headers

The Kamelet supports various headers to update issue fields: - `ce-issueKey`: The JIRA issue key to update - `ce-issueTypeName`: Update issue type - `ce-issueSummary`: Update issue summary/title - `ce-issueAssignee`: Update assignee - `ce-issuePriorityName`: Update priority level - `ce-issueComponents`: Update issue components - `ce-issueDescription`: Update detailed description

### Usage

The Kamelet modifies existing JIRA issues with new field values, enabling automated issue updates based on external data or processing results.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-update-issue-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-update-issue-sink.kamelet.yaml)
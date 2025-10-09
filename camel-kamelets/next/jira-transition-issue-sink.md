# ![jira transition issue sink](_images/kamelets/jira-transition-issue-sink.svg) Jira Transition Issue Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sets a new status (transition to) of an existing issue in Jira.

## Configuration Options

The following table summarizes the configuration options available for the `jira-transition-issue-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **jiraUrl** | Jira URL | **Required** The URL of your instance of Jira. | string |  | http://my\_jira.com:8081 |
| **password** | Password | The password to access Jira. | string |  |  |
| **personal-token** | Personal Token | Personal Token. | string |  |  |
| **username** | Username | The username to access Jira. | string |  |  |

## Dependencies

At runtime, the `jira-transition-issue-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:jira-transition-issue-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Jira Transition Issue Sink Kamelet Description

### JIRA Operations

This Kamelet transitions JIRA issues to new statuses (e.g., from "In Progress" to "Done").

### Input Format

Expects JSON-formatted data containing the transition information.

### Authentication

Supports multiple authentication methods: - **Username and Password**: Basic authentication - **Personal Token**: API token authentication

### Required Configuration

-   **JIRA URL**: The URL of your JIRA instance
    

### Transition Configuration Headers

The Kamelet supports headers to specify transition details: - `ce-issueKey`: The JIRA issue key to transition - `ce-issueTransitionId`: The transition ID to execute

### Usage

The Kamelet changes the status of existing JIRA issues by executing workflow transitions, enabling automated issue state management based on external events or processing results.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-transition-issue-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-transition-issue-sink.kamelet.yaml)
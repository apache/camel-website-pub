# ![jira update issue sink](_images/kamelets/jira-update-issue-sink.svg) Jira Update Issue Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Changes the fields of an existing Jira issue, such as its summary, description, assignee or priority, for each message.

Use it to keep a ticket in step with another system, for example to assign an issue to the person on call or to raise its priority when an alert repeats. To change the status use `jira-transition-issue-sink`, and to create issues `jira-add-issue-sink`.

Input: the body becomes the new description of the issue, as text, and replaces the old one. When the body is empty, the `ce-issueDescription` header gives the description instead. The `ce-issueKey` header (the key of the issue, such as `SHOP-42`) is required. The other fields come from optional headers, and a field without a header is left as it is: `ce-issueSummary` (the title), `ce-issueTypeName` (such as `Bug`), `ce-issueAssignee`, `ce-issuePriorityName` (such as `High`) and `ce-issueComponents` (a comma-separated list, which replaces the components).

Output: the message is unchanged.

Good to know: a message with a body always replaces the description, even when it also has the `ce-issueDescription` header. An issue type or a priority whose name Jira does not know is ignored. A message without `ce-issueKey` fails. Log in either with `username` and `password`, or with `personal-token`.

## Configuration Options

The following table summarizes the configuration options available for the `jira-update-issue-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **jiraUrl** | Jira URL | **Required** The address of your Jira, as you open it in a browser, without a path. | string |  | https://mycompany.atlassian.net |
| **password** | Password | The password of `username`. For Jira Cloud, use an API token of the account here, not its password; create one at id.atlassian.com, under Security, API tokens. | string |  |  |
| **personal-token** | Personal Token | A personal access token, for Jira Server and Jira Data Center; create one in Jira under your profile, Personal Access Tokens. Use it instead of `username` and `password`. | string |  |  |
| **username** | Username | The user to log in as, together with `password`. For Jira Cloud, this is the email address of the account. When it is set, `personal-token` is not used. | string |  |  |

## Dependencies

At runtime, the `jira-update-issue-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:jira
    
-   camel:kamelet
    
-   mvn:tools.jackson.datatype:jackson-datatype-joda:3.2.4
    

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

The body becomes the new description of the issue, as text. It replaces the description on every message.

### Issue Update Headers

The Kamelet reads these headers. Only `ce-issueKey` is required; a field without a header is left as it is.

-   `ce-issueKey`: the key of the issue to update, such as `SHOP-42` (required)
    
-   `ce-issueTypeName`: the name of the new issue type, such as `Bug`
    
-   `ce-issueSummary`: the new summary (title)
    
-   `ce-issueAssignee`: the user name of the new assignee
    
-   `ce-issuePriorityName`: the name of the new priority, such as `High`
    
-   `ce-issueComponents`: a comma-separated list of component names, which replaces the components of the issue
    

An issue type or a priority whose name Jira does not know is ignored. The description comes from the body; the `ce-issueDescription` header gives it only when the body is empty.

### Authentication

Use one of the two ways to log in:

-   **Jira Cloud**: set `username` to the email address of the account, and `password` to an API token of that account.
    
-   **Jira Server and Jira Data Center**: set `personal-token` to a personal access token, and leave `username` and `password` empty.
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "The checkout page fails for orders above 1000 EUR. Seen again today."
        repeatCount: 1
      steps:
        - setHeader:
            name: ce-issueKey
            constant: SHOP-42
        - setHeader:
            name: ce-issuePriorityName
            constant: High
        - to:
            uri: "kamelet:jira-update-issue-sink"
            parameters:
              jiraUrl: "https://mycompany.atlassian.net"
              username: "me@mycompany.com"
              password: "{{jira.apiToken}}"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-update-issue-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-update-issue-sink.kamelet.yaml)
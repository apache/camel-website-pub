# ![jira add issue sink](_images/kamelets/jira-add-issue-sink.svg) Jira Add Issue Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Creates a new issue, such as a bug or a task, in a Jira project for each message.

Use it to open a ticket automatically when something happens, for example when a monitoring alert fires, a form is submitted or an order fails.

Input: the body is the description of the issue, as text. The other fields come from headers. `ce-projectKey` (the key of the project, such as `SHOP`), `ce-issueTypeName` (such as `Bug` or `Task`) and `ce-issueSummary` (the title) are required. `ce-issueAssignee`, `ce-issuePriorityName` (such as `High`) and `ce-issueComponents` (a comma-separated list) are optional. Set them before this sink, for example with `insert-header-action`.

Output: when it is used inside a route, the body afterwards is the issue that was created.

Good to know: a message without a project key, an issue type or a summary fails. Log in either with `username` and `password`, or with `personal-token`.

## Configuration Options

The following table summarizes the configuration options available for the `jira-add-issue-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **jiraUrl** | Jira URL | **Required** The address of your Jira, as you open it in a browser, without a path. | string |  | https://mycompany.atlassian.net |
| **password** | Password | The password of `username`. For Jira Cloud, use an API token of the account here, not its password. | string |  |  |
| **personal-token** | Personal Token | A personal access token, for Jira Server and Jira Data Center. Use it instead of `username` and `password`. | string |  |  |
| **username** | Username | The user to log in as, together with `password`. For Jira Cloud, this is the email address of the account. | string |  |  |

## Dependencies

At runtime, the `jira-add-issue-sink` Kamelet relies upon the presence of the following dependencies:

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

### Authentication

Use one of the two ways to log in:

-   **Jira Cloud**: set `username` to the email address of the account, and `password` to an API token of that account.
    
-   **Jira Server and Jira Data Center**: set `personal-token` to a personal access token, and leave `username` and `password` empty.
    

### Usage example

The route below creates a bug in the `SHOP` project for every message. The body becomes the description of the issue, and the headers give the other fields.

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 60000
        repeatCount: 1
        message: "The checkout page returns an error for orders above 1000 EUR."
      steps:
        - setHeader:
            name: ce-projectKey
            constant: SHOP
        - setHeader:
            name: ce-issueTypeName
            constant: Bug
        - setHeader:
            name: ce-issueSummary
            constant: Checkout fails for large orders
        - to:
            uri: "kamelet:jira-add-issue-sink"
            parameters:
              jiraUrl: "https://mycompany.atlassian.net"
              username: "me@mycompany.com"
              password: "{{jira.apiToken}}"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-add-issue-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-add-issue-sink.kamelet.yaml)
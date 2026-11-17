# ![jira transition issue sink](_images/kamelets/jira-transition-issue-sink.svg) Jira Transition Issue Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Moves an existing Jira issue to another status, such as from `In Progress` to `Done`, by running a transition of its workflow for each message.

Use it to keep tickets in step with what happens elsewhere, for example to close an issue when its fix is deployed or to reopen it when a test fails again. To change other fields use `jira-update-issue-sink`, and to only add a comment `jira-add-comment-sink`.

Input: the `ce-issueKey` header (the key of the issue, such as `SHOP-42`) and the `ce-issueTransitionId` header (the ID number of the transition, such as `31`, not the name of the status) are required. The body, as text, is added to the issue as a comment after the transition.

Output: the message is unchanged.

Good to know: a message without one of the two headers fails, and so does a transition that the workflow does not allow from the current status of the issue. Jira lists the transitions possible for an issue, with their IDs, at `<jiraUrl>/rest/api/2/issue/<key>/transitions`. Log in either with `username` and `password`, or with `personal-token`.

## Configuration Options

The following table summarizes the configuration options available for the `jira-transition-issue-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **jiraUrl** | Jira URL | **Required** The address of your Jira, as you open it in a browser, without a path. | string |  | https://mycompany.atlassian.net |
| **password** | Password | The password of `username`. For Jira Cloud, use an API token of the account here, not its password; create one at id.atlassian.com, under Security, API tokens. | string |  |  |
| **personal-token** | Personal Token | A personal access token, for Jira Server and Jira Data Center; create one in Jira under your profile, Personal Access Tokens. Use it instead of `username` and `password`. | string |  |  |
| **username** | Username | The user to log in as, together with `password`. For Jira Cloud, this is the email address of the account. When it is set, `personal-token` is not used. | string |  |  |

## Dependencies

At runtime, the `jira-transition-issue-sink` Kamelet relies upon the presence of the following dependencies:

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

This Kamelet transitions JIRA issues to new statuses (e.g., from "In Progress" to "Done"), by running a transition of the workflow of the issue.

### Input Format

Two headers are required:

-   `ce-issueKey`: the key of the issue to transition, such as `SHOP-42`.
    
-   `ce-issueTransitionId`: the ID number of the transition to run, such as `31`. It is not the name of the status.
    

The body, as text, is added to the issue as a comment after the transition.

### Finding the Transition ID

A transition is a step of the workflow, from one status to another, and each has an ID number. Jira lists the transitions that are possible for an issue in its current status, with their IDs, at `<jiraUrl>/rest/api/2/issue/<key>/transitions`. A Jira administrator can also see them in the text view of the workflow. A transition that is not possible from the current status of the issue fails.

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
        message: "Closed automatically: the fix is deployed."
        repeatCount: 1
      steps:
        - setHeader:
            name: ce-issueKey
            constant: SHOP-42
        - setHeader:
            name: ce-issueTransitionId
            constant: "31"
        - to:
            uri: "kamelet:jira-transition-issue-sink"
            parameters:
              jiraUrl: "https://mycompany.atlassian.net"
              username: "me@mycompany.com"
              password: "{{jira.apiToken}}"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-transition-issue-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-transition-issue-sink.kamelet.yaml)
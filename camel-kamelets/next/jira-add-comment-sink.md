# ![jira add comment sink](_images/kamelets/jira-add-comment-sink.svg) Jira Add Comment Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Adds the text of each message as a new comment to an existing issue in Jira.

Use it to record on a ticket what happened elsewhere, for example a deployment, the result of a build or a reply of a customer. To create issues use `jira-add-issue-sink`, to change their fields `jira-update-issue-sink`, and to change their status `jira-transition-issue-sink`.

Input: the body is the text of the comment, as text. The `ce-issueKey` header, the key of the issue such as `SHOP-42`, is required. Set it before this sink, for example with `insert-header-action`.

Output: the message is unchanged.

Good to know: a message without `ce-issueKey`, or for an issue that does not exist or that the user cannot see, fails. The comment is written in the name of the account the Kamelet logs in with. Log in either with `username` and `password`, or with `personal-token`. Headers that start with `CamelJira` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `jira-add-comment-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **jiraUrl** | Jira URL | **Required** The address of your Jira, as you open it in a browser, without a path. | string |  | https://mycompany.atlassian.net |
| **password** | Password | The password of `username`. For Jira Cloud, use an API token of the account here, not its password; create one at id.atlassian.com, under Security, API tokens. | string |  |  |
| **personal-token** | Personal Token | A personal access token, for Jira Server and Jira Data Center; create one in Jira under your profile, Personal Access Tokens. Use it instead of `username` and `password`. | string |  |  |
| **username** | Username | The user to log in as, together with `password`. For Jira Cloud, this is the email address of the account. When it is set, `personal-token` is not used. | string |  |  |

## Dependencies

At runtime, the `jira-add-comment-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:jira-add-comment-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Jira Add Comment Sink Kamelet Description

### JIRA Operations

This Kamelet adds a comment to an existing JIRA issue for each message.

### Input Format

The body is the text of the comment, as text. The `ce-issueKey` header names the issue, such as `SHOP-42`, and is required: a message without it fails.

### Authentication

Use one of the two ways to log in:

-   **Jira Cloud**: set `username` to the email address of the account, and `password` to an API token of that account.
    
-   **Jira Server and Jira Data Center**: set `personal-token` to a personal access token, and leave `username` and `password` empty.
    

The comment is written in the name of the account the Kamelet logs in with.

### Usage example

The route below adds a comment to the issue `SHOP-42`.

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "Version 2.3.1 with the fix is deployed to production."
        repeatCount: 1
      steps:
        - setHeader:
            name: ce-issueKey
            constant: SHOP-42
        - to:
            uri: "kamelet:jira-add-comment-sink"
            parameters:
              jiraUrl: "https://mycompany.atlassian.net"
              username: "me@mycompany.com"
              password: "{{jira.apiToken}}"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-add-comment-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-add-comment-sink.kamelet.yaml)
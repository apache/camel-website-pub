# ![jira source](_images/kamelets/jira-source.svg) Jira Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each new Jira issue that matches a JQL query, such as every new bug of a project, by asking Jira at a regular interval.

Use it to react when a ticket is opened, for example to tell a team chat about a new bug or to copy new issues into another tracker. To log in with OAuth 1.0a instead of a password or a token, use `jira-oauth-source`.

Output: the body is the issue as JSON text in bytes, with fields such as `key`, `summary`, `description`, `status`, `issueType`, `project`, `reporter`, `assignee` and `priority`. The `Content-Type` header is `application/json`.

Good to know: only the issues created after the Kamelet starts are sent; the issues that already exist are not, and neither are changes to an issue. It checks every 6 seconds. `jql` must be set, or the Kamelet does not start. Log in either with `username` and `password`, or with `personal-token`.

## Configuration Options

The following table summarizes the configuration options available for the `jira-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **jiraUrl** | Jira URL | **Required** The address of your Jira, as you open it in a browser, without a path. | string |  | https://mycompany.atlassian.net |
| **jql** | JQL | **Required** The JQL query that selects the issues to send, as in the advanced issue search of Jira, without `ORDER BY`. It must be set, or the Kamelet does not start. | string |  | project = SHOP AND issuetype = Bug |
| **password** | Password | The password of `username`. For Jira Cloud, use an API token of the account here, not its password; create one at id.atlassian.com, under Security, API tokens. | string |  |  |
| **personal-token** | Personal Token | A personal access token, for Jira Server and Jira Data Center; create one in Jira under your profile, Personal Access Tokens. Use it instead of `username` and `password`. | string |  |  |
| **username** | Username | The user to log in as, together with `password`. For Jira Cloud, this is the email address of the account. When it is set, `personal-token` is not used. | string |  |  |

## Dependencies

At runtime, the `jira-source` Kamelet relies upon the presence of the following dependencies:

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

Use one of the two ways to log in:

-   **Jira Cloud**: set `username` to the email address of the account, and `password` to an API token of that account.
    
-   **Jira Server and Jira Data Center**: set `personal-token` to a personal access token, and leave `username` and `password` empty.
    

To log in with OAuth 1.0a, use `jira-oauth-source` instead.

### Output format

The Kamelet sends each new issue that matches the JQL query as one message, with the issue as JSON text. Only the issues created after the Kamelet starts are sent. It checks for new issues every 6 seconds.

### Configuration

The Kamelet requires the following parameters:

-   `jiraUrl`: The address of your Jira, such as `[https://mycompany.atlassian.net](https://mycompany.atlassian.net)`
    
-   `jql`: The JQL query that selects the issues, without `ORDER BY`. The Kamelet does not start without it.
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:jira-source"
      parameters:
        jiraUrl: "https://mycompany.atlassian.net"
        username: "me@mycompany.com"
        password: "{{jira.apiToken}}"
        jql: "project = SHOP AND issuetype = Bug"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jira-source.kamelet.yaml)
# ![github event source](_images/kamelets/github-event-source.svg) GitHub Event Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the activity of a GitHub repository, such as pushes, issues, pull requests and stars, one message per event, by asking the GitHub API for new events.

Use it to follow everything that happens in a repository in one flow, for example to log it or to count it. To receive only commits, pull requests, comments on pull requests or tags, use `github-commit-source`, `github-pullrequest-source`, `github-pullrequest-comment-source` or `github-tag-source`.

Output: the body is the type of the event as JSON text, that is a quoted JSON string such as `"PUSH"`, `"PULL_REQUEST"` or `"ISSUES"`. The details of the event are only in the `CamelGitHubEventPayload` header, as a Java object.

Good to know: when it starts, it first sends the recent events that GitHub still lists for the repository, not only the new ones. It works with github.com, not with GitHub Enterprise Server. It asks GitHub for new events once a minute by default (`delay`), and every request counts against the API rate limit of the token.

## Configuration Options

The following table summarizes the configuration options available for the `github-event-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **oauthToken** | OAuth Token | **Required** A GitHub personal access token, created on GitHub under Settings, Developer settings, Personal access tokens. It needs read access to the repository. | string |  |  |
| **repoName** | Repository Name | **Required** The name of the repository, such as `camel` in `[https://github.com/apache/camel](https://github.com/apache/camel)`. | string |  | camel |
| **repoOwner** | Repository Owner | **Required** The user or organization that owns the repository, such as `apache` in `[https://github.com/apache/camel](https://github.com/apache/camel)`. | string |  | apache |
| **delay** | Delay | How long to wait between two polls of GitHub, in milliseconds. For example, 60000 is one minute. | integer | 60000 |  |

## Dependencies

At runtime, the `github-event-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:github2
    
-   camel:kamelet
    

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
      uri: "kamelet:github-event-source"
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

## GitHub Event Source Kamelet Description

### Authentication methods

This Kamelet uses OAuth token-based authentication to connect to GitHub. You need to provide:

-   A valid OAuth token with appropriate repository permissions
    
-   The repository name and owner information
    

### Output format

The Kamelet produces one message per repository event, such as a push, an issue or a pull request. The body is the type of the event as JSON text, that is a quoted JSON string such as `"PUSH"`; the details of the event are in the `CamelGitHubEventPayload` header, as a Java object.

### Configuration

The Kamelet requires the following parameters:

-   `repoName`: The GitHub repository name
    
-   `repoOwner`: The repository owner (user or organization)
    
-   `oauthToken`: OAuth token for authentication
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: github-event-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: github-event-source
    properties:
      repoName: "my-repository"
      repoOwner: "my-organization"
      oauthToken: "{{oauth-token}}"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/github-event-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/github-event-source.kamelet.yaml)
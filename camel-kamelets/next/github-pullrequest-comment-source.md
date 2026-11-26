# ![github pullrequest comment source](_images/kamelets/github-pullrequest-comment-source.svg) GitHub Pull Request Comments Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each new comment written on the open pull requests of a GitHub repository, one message per comment, by asking the GitHub API for new comments.

Use it to react to the discussion on pull requests, for example to answer a command written in a comment, such as `/retest`, or to forward the comments to a chat channel. To receive the pull requests themselves, use `github-pullrequest-source`.

Output: the body is the comment as JSON text in bytes, an object with the fields of the GitHub API that say what it is: `id`, `body` (the text of the comment), `html_url` (its web address), `user.login` (its author), `author_association` (the role of the author in the repository, such as `OWNER` or `CONTRIBUTOR`), `created_at` and `updated_at`. The `CamelGitHubPullRequest` header gives the number of the pull request it was written on. The `Content-Type` header is `application/json`.

Good to know: only the comments written after the start are sent, and only on pull requests that are still open. These are the comments of the conversation of a pull request, not the review comments on lines of code. It works with github.com, not with GitHub Enterprise Server. Once a minute by default (`delay`), it asks GitHub for the open pull requests and for the comments of each of them, and every request counts against the API rate limit of the token.

## Configuration Options

The following table summarizes the configuration options available for the `github-pullrequest-comment-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **oauthToken** | OAuth Token | **Required** A GitHub personal access token, created on GitHub under Settings, Developer settings, Personal access tokens. It needs read access to the repository and its pull requests. | string |  |  |
| **repoName** | Repository Name | **Required** The name of the repository, such as `camel` in `[https://github.com/apache/camel](https://github.com/apache/camel)`. | string |  | camel |
| **repoOwner** | Repository Owner | **Required** The user or organization that owns the repository, such as `apache` in `[https://github.com/apache/camel](https://github.com/apache/camel)`. | string |  | apache |
| **delay** | Delay | How long to wait between two polls of GitHub, in milliseconds. For example, 60000 is one minute. | integer | 60000 |  |

## Dependencies

At runtime, the `github-pullrequest-comment-source` Kamelet relies upon the presence of the following dependencies:

-   camel:github2
    
-   camel:jq
    
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
      uri: "kamelet:github-pullrequest-comment-source"
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

## GitHub Pull Request Comments Source Kamelet Description

### Authentication methods

This Kamelet uses OAuth token-based authentication to connect to GitHub. You need to provide:

-   A valid OAuth token with appropriate repository permissions
    
-   The repository name and owner information
    

### Output format

The Kamelet produces pull request comment data in JSON format containing comment information from GitHub pull requests in the specified repository.

### Configuration

The Kamelet requires the following parameters:

-   `repoName`: The GitHub repository name
    
-   `repoOwner`: The repository owner (user or organization)
    
-   `oauthToken`: OAuth token for authentication
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:github-pullrequest-comment-source"
      parameters:
        repoName: "my-repository"
        repoOwner: "my-organization"
        oauthToken: "{{oauth-token}}"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/github-pullrequest-comment-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/github-pullrequest-comment-source.kamelet.yaml)
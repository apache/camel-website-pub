# ![github pullrequest source](_images/kamelets/github-pullrequest-source.svg) GitHub Pull Request Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each new pull request opened in a GitHub repository, one message per pull request, by asking the GitHub API for new open pull requests.

Use it to react when someone proposes a change, for example to announce the pull request in a chat channel, open a review ticket or start a check. To receive the comments on pull requests, use `github-pullrequest-comment-source`.

Output: the body is the pull request as JSON text, an object with the fields of the GitHub API that say what it is: `number`, `title`, `body` (its description), `state`, `draft`, `html_url` (its web address), `user.login` (its author), `head` and `base` (the branch it comes from and the branch it goes to, each with `ref`, `sha` and `label`), `labels` (each with its `name`), `created_at` and `updated_at`. The `CamelGitHubPullRequest` header gives its number, and `CamelGitHubPullRequestHeadCommitSha` the SHA of its latest commit.

Good to know: only the pull requests opened after the start are sent, once each; updates, merges and closes are not. The body holds only what GitHub gives in its list of pull requests, so no more requests are made per pull request; the size of the change, such as its additions or commits, and whether it can be merged are not in it. It works with github.com, not with GitHub Enterprise Server. It asks GitHub for new pull requests once a minute by default (`delay`), and every request counts against the API rate limit of the token.

## Configuration Options

The following table summarizes the configuration options available for the `github-pullrequest-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **oauthToken** | OAuth Token | **Required** A GitHub personal access token, created on GitHub under Settings, Developer settings, Personal access tokens. It needs read access to the repository and its pull requests. | string |  |  |
| **repoName** | Repository Name | **Required** The name of the repository, such as `camel` in `[https://github.com/apache/camel](https://github.com/apache/camel)`. | string |  | camel |
| **repoOwner** | Repository Owner | **Required** The user or organization that owns the repository, such as `apache` in `[https://github.com/apache/camel](https://github.com/apache/camel)`. | string |  | apache |
| **delay** | Delay | How long to wait between two polls of GitHub, in milliseconds. For example, 60000 is one minute. | integer | 60000 |  |

## Dependencies

At runtime, the `github-pullrequest-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:github-pullrequest-source"
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

## GitHub Pull Request Source Kamelet Description

### Authentication methods

This Kamelet uses OAuth token-based authentication to connect to GitHub. You need to provide:

-   A valid OAuth token with appropriate repository permissions
    
-   The repository name and owner information
    

### Output format

The Kamelet produces pull request data in JSON format containing pull request information from the specified GitHub repository.

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
  name: github-pullrequest-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: github-pullrequest-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/github-pullrequest-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/github-pullrequest-source.kamelet.yaml)
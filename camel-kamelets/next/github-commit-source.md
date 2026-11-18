# ![github commit source](_images/kamelets/github-commit-source.svg) GitHub Commit Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each new commit on a branch of a GitHub repository, one message per commit, oldest first, by asking the GitHub API for new commits.

Use it to start a flow when code is pushed, for example to post the commit message to a chat channel or to trigger a build or a deployment.

Output: the body is the commit message as JSON text, that is a quoted JSON string such as `"Fix the login page"`. The `CamelGitHubCommitSha` header gives the SHA of the commit, `CamelGitHubCommitUrl` its web address, and `CamelGitHubCommitAuthor` and `CamelGitHubCommitCommitter` the names of its author and committer.

Good to know: with the default `startingSha` of `last`, only the commits made after the start are sent. It works with github.com, not with GitHub Enterprise Server. It asks GitHub for new commits once a minute by default (`delay`), and every request counts against the API rate limit of the token.

## Configuration Options

The following table summarizes the configuration options available for the `github-commit-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **branch** | Branch | **Required** The name of the branch to watch for new commits. | string |  | main |
| **oauthToken** | OAuth Token | **Required** A GitHub personal access token, created on GitHub under Settings, Developer settings, Personal access tokens. It needs read access to the repository. | string |  |  |
| **repoName** | Repository Name | **Required** The name of the repository, such as `camel` in `[https://github.com/apache/camel](https://github.com/apache/camel)`. | string |  | camel |
| **repoOwner** | Repository Owner | **Required** The user or organization that owns the repository, such as `apache` in `[https://github.com/apache/camel](https://github.com/apache/camel)`. | string |  | apache |
| **startingSha** | Starting SHA | **Required** Where to start. `last` sends only the commits made after the start, `beginning` also sends the commits already on the branch, and the SHA of a commit sends the commits made after that one. | string | last | 8aed4eb7f8fa1877d215a331a2a682edc4e26932 |
| **delay** | Delay | How long to wait between two polls of GitHub, in milliseconds. For example, 60000 is one minute. | integer | 60000 |  |

## Dependencies

At runtime, the `github-commit-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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
      uri: "kamelet:github-commit-source"
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

## GitHub Commit Source Kamelet Description

### Authentication methods

This Kamelet uses OAuth token-based authentication to connect to GitHub. You need to provide:

-   A valid OAuth token with appropriate repository permissions
    
-   The repository name and owner information
    

### Output format

The Kamelet produces one message per new commit on the branch. The body is the commit message as JSON text, that is a quoted JSON string, and the headers `CamelGitHubCommitSha`, `CamelGitHubCommitUrl`, `CamelGitHubCommitAuthor` and `CamelGitHubCommitCommitter` give the details of the commit.

### Configuration

The Kamelet requires the following parameters:

-   `repoName`: The GitHub repository name
    
-   `repoOwner`: The repository owner (user or organization)
    
-   `oauthToken`: OAuth token for authentication
    
-   `startingSha`: SHA from which to start consuming (beginning, last, or specific SHA)
    
-   `branch`: The branch to consume commits from
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: github-commit-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: github-commit-source
    properties:
      repoName: "my-repository"
      repoOwner: "my-organization"
      oauthToken: "{{oauth-token}}"
      startingSha: "last"
      branch: "main"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/github-commit-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/github-commit-source.kamelet.yaml)
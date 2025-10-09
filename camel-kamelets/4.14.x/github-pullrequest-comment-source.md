# ![github pullrequest comment source](_images/kamelets/github-pullrequest-comment-source.svg) GitHub Pull Request Comments Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive pull request Comments From GitHub.

## Configuration Options

The following table summarizes the configuration options available for the `github-pullrequest-comment-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **oauthToken** | OAuth Token | **Required** OAuth token. | string |  |  |
| **repoName** | Repository Name | **Required** The GitHub Repository name. | string |  |  |
| **repoOwner** | Repository Owner | **Required** The repository owner. | string |  |  |

## Dependencies

At runtime, the `github-pullrequest-comment-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:github
    
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
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: github-pullrequest-comment-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: github-pullrequest-comment-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/github-pullrequest-comment-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/github-pullrequest-comment-source.kamelet.yaml)
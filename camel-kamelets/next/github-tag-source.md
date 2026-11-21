# ![github tag source](_images/kamelets/github-tag-source.svg) GitHub Tag Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each new tag created in a GitHub repository, one message per tag, by asking the GitHub API for the tags of the repository.

Use it to react to a new version, for example to announce a release, update a changelog or start a deployment. To receive every commit instead, use `github-commit-source`.

Output: the body is the tag as JSON text in bytes, an object with its `name`, such as `v1.0.0`, and `commit.sha`, the SHA of the commit it points to. The `Content-Type` header is `application/json`.

Good to know: only the tags created after the start are sent; the tags that exist when it starts are skipped. GitHub lists a tag without its date or the message of an annotated tag, so they are not in the body. It works with github.com, not with GitHub Enterprise Server. It asks GitHub for the tags once a minute by default (`delay`), and every request counts against the API rate limit of the token.

## Configuration Options

The following table summarizes the configuration options available for the `github-tag-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **oauthToken** | OAuth Token | **Required** A GitHub personal access token, created on GitHub under Settings, Developer settings, Personal access tokens. It needs read access to the repository. | string |  |  |
| **repoName** | Repository Name | **Required** The name of the repository, such as `camel` in `[https://github.com/apache/camel](https://github.com/apache/camel)`. | string |  | camel |
| **repoOwner** | Repository Owner | **Required** The user or organization that owns the repository, such as `apache` in `[https://github.com/apache/camel](https://github.com/apache/camel)`. | string |  | apache |
| **delay** | Delay | How long to wait between two polls of GitHub, in milliseconds. For example, 60000 is one minute. | integer | 60000 |  |

## Dependencies

At runtime, the `github-tag-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:github-tag-source"
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

## GitHub Tag Source Kamelet Description

### Authentication methods

This Kamelet uses OAuth token-based authentication to connect to GitHub. You need to provide:

-   A valid OAuth token with appropriate repository permissions
    
-   The repository name and owner information
    

### Output format

The Kamelet produces tag data in JSON format containing tag information from the specified GitHub repository.

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
  name: github-tag-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: github-tag-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/github-tag-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/github-tag-source.kamelet.yaml)
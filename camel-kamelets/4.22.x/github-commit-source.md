# ![github commit source](_images/kamelets/github-commit-source.svg) GitHub Commit Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive commit From GitHub.

## Configuration Options

The following table summarizes the configuration options available for the `github-commit-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **branch** | Branch | **Required** The branch we want to consume commit from. | string |  |  |
| **oauthToken** | OAuth Token | **Required** OAuth token. | string |  |  |
| **repoName** | Repository Name | **Required** The GitHub Repository name. | string |  |  |
| **repoOwner** | Repository Owner | **Required** The repository owner. | string |  |  |
| **startingSha** | Starting SHA | **Required** The SHA from which we want to consume, possible values beginning, last or a specific SHA. | string | last |  |

## Dependencies

At runtime, the `github-commit-source` Kamelet relies upon the presence of the following dependencies:

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

The Kamelet produces commit data in JSON format containing commit information from the specified GitHub repository and branch.

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
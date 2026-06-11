# ![github event source](_images/kamelets/github-event-source.svg) GitHub Event Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive Events From a GitHub Repository.

## Configuration Options

The following table summarizes the configuration options available for the `github-event-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **oauthToken** | OAuth Token | **Required** OAuth token. | string |  |  |
| **repoName** | Repository Name | **Required** The GitHub Repository name. | string |  |  |
| **repoOwner** | Repository Owner | **Required** The repository owner. | string |  |  |

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

The Kamelet produces event data in JSON format containing various GitHub repository events such as pushes, issues, pull requests, and other repository activities.

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
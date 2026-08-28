# ![github tag source](_images/kamelets/github-tag-source.svg) GitHub Tag Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive Tags From a GitHub Repository.

## Configuration Options

The following table summarizes the configuration options available for the `github-tag-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **oauthToken** | OAuth Token | **Required** OAuth token. | string |  |  |
| **repoName** | Repository Name | **Required** The GitHub Repository name. | string |  |  |
| **repoOwner** | Repository Owner | **Required** The repository owner. | string |  |  |

## Dependencies

At runtime, the `github-tag-source` Kamelet relies upon the presence of the following dependencies:

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
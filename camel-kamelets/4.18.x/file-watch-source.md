# ![file watch source](_images/kamelets/file-watch-source.svg) File Watch Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive events related to a file or folder. It may require a volume mounting on Kubernetes.

## Configuration Options

The following table summarizes the configuration options available for the `file-watch-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **events** | Events | **Required** The type of events to consume. | string | CREATE,MODIFY,DELETE |  |
| **filePath** | Path to Watch | **Required** Path of file or folder to watch. | string |  |  |

## Dependencies

At runtime, the `file-watch-source` Kamelet relies upon the presence of the following dependencies:

-   camel:file-watch
    
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
      uri: "kamelet:file-watch-source"
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

## File Watch Source Kamelet Description

### Configuration

The File Watch Source Kamelet monitors files or directories for changes and emits events when specific filesystem events occur. It requires the following configuration:

-   **File Path**: The path to the file or directory to monitor (required)
    
-   **Events**: The types of filesystem events to watch for (default: "CREATE,MODIFY,DELETE")
    

### Event Types

The kamelet can monitor for the following types of filesystem events:

-   **CREATE**: Triggered when a new file or directory is created
    
-   **MODIFY**: Triggered when an existing file or directory is modified
    
-   **DELETE**: Triggered when a file or directory is deleted
    

You can specify multiple events by separating them with commas.

### Output Format

The kamelet outputs filesystem event information including details about the type of event and the affected file or directory path.

### Volume Mounting

When deployed on Kubernetes, this kamelet may require volume mounting to access the filesystem paths you want to monitor. Ensure the appropriate volumes are mounted to the pod running the integration.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:file-watch-source"
      parameters:
        filePath: "/tmp/watched-directory"
        events: "CREATE,MODIFY,DELETE"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Monitor Specific Events

```yaml
- route:
    from:
      uri: "kamelet:file-watch-source"
      parameters:
        filePath: "/var/log/application.log"
        events: "MODIFY"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This example only monitors for modifications to a specific log file.

### Monitor Multiple Event Types

```yaml
- route:
    from:
      uri: "kamelet:file-watch-source"
      parameters:
        filePath: "/home/user/documents"
        events: "CREATE,DELETE"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This example monitors for file creation and deletion events in the documents directory.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/file-watch-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/file-watch-source.kamelet.yaml)
# ![file watch source](_images/kamelets/file-watch-source.svg) File Watch Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends a message each time a file in a local directory is created, changed or deleted, with the kind of change and the path of the file.

Use it to react to files that another program writes into a directory on the same machine, for example to start processing when a new export appears, or to keep track of the changes in a folder. To read files from a remote server instead, use `ftp-source`, `sftp-source` or `aws-s3-source`.

Output: the body is the file that changed, which the next step can read as text or bytes; a deleted file or a directory has no content to read. The `CamelFileEventType` header is `CREATE`, `MODIFY` or `DELETE`, `CamelFileName` is the path of the file relative to the watched directory, and `CamelFileAbsolutePath` is its full path.

Good to know: it watches the subdirectories too, new ones included. It never changes or deletes the files. Only changes made while it runs are sent, not the files that are already there when it starts. The path must be a directory, not a single file; it is created when it does not exist. On Kubernetes, mount the directory into the pod as a volume.

## Configuration Options

The following table summarizes the configuration options available for the `file-watch-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **events** | Events | **Required** The kinds of change to send, as a comma-separated list of `CREATE`, `MODIFY` and `DELETE`. For example, `CREATE` sends only the new files. | string | CREATE,MODIFY,DELETE | CREATE |
| **filePath** | Directory to Watch | **Required** The full path of the local directory to watch. It must be a directory, not a single file: to follow one file, watch its directory. Changes in its subdirectories are sent too. | string |  | /data/incoming |

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

-   **File Path**: The path of the directory to monitor (required). It must be a directory, not a single file; it is created when it does not exist
    
-   **Events**: The types of filesystem events to watch for (default: "CREATE,MODIFY,DELETE")
    

### Event Types

The kamelet can monitor for the following types of filesystem events:

-   **CREATE**: Triggered when a new file or directory is created
    
-   **MODIFY**: Triggered when an existing file or directory is modified
    
-   **DELETE**: Triggered when a file or directory is deleted
    

You can specify multiple events by separating them with commas.

### Output Format

The body of each message is the file that changed. The `CamelFileEventType` header holds the kind of event (`CREATE`, `MODIFY` or `DELETE`), `CamelFileName` the path relative to the watched directory, and `CamelFileAbsolutePath` the full path. Subdirectories are watched too. A deleted file, or a directory, has no content to read.

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
        filePath: "/var/log/myapp"
        events: "MODIFY"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This example only monitors for modifications of the files in the `/var/log/myapp` directory. To follow a single file, watch its directory and filter on `CamelFileName`.

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
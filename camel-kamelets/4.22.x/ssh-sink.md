# ![ssh sink](_images/kamelets/ssh-sink.svg) SSH Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send command through SSH session.

## Configuration Options

The following table summarizes the configuration options available for the `ssh-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The SSH Host. | string |  |  |
| **connectionPort** | Connection Port | **Required** The SSH Port. | string | 22 |  |
| **password** | Password | **Required** The SSH password to use. | string |  |  |
| **username** | Username | **Required** The SSH username to use. | string |  |  |

## Dependencies

At runtime, the `ssh-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:ssh
    
-   camel:gson
    
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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:ssh-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## SSH Sink Kamelet Description

### Secure Shell Integration

This Kamelet provides integration with SSH (Secure Shell) for executing remote commands and operations on remote systems over encrypted connections.

### Remote Command Execution

Enables execution of commands on remote systems through SSH connections, providing secure remote administration and automation capabilities.

### Authentication Methods

Supports multiple SSH authentication mechanisms:

-   Username and password authentication
    
-   Public key authentication
    
-   Certificate-based authentication
    
-   Multi-factor authentication support
    

### Security Features

SSH provides comprehensive security features:

-   Strong encryption for all communications
    
-   Host key verification
    
-   User authentication and authorization
    
-   Session integrity and confidentiality
    

### Remote Administration

Common use cases include:

-   System administration and maintenance
    
-   Automated deployment and configuration
    
-   Remote monitoring and diagnostics
    
-   File operations and transfers
    
-   Service management and control
    

### Cross-Platform Support

Works across different operating systems and platforms, providing consistent secure remote access capabilities for heterogeneous environments.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ssh-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ssh-sink.kamelet.yaml)
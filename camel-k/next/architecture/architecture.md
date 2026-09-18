# Architecture

## High Level Architecture

> **Note**
> The following diagram reflects the Camel K architecture as of version 1.4.0

![Overview](../_images/architecture/camel-k-high-level.svg)

## Concepts

The main **Camel K** platform concepts are:

1.  The [Operator](operator.md) which is the intelligence that coordinates all the moving parts;
    
2.  The [Runtime](runtime.md) which provides the functionality to run the integration;
    
3.  The [Traits](traits.md) which configure the integration and the runtime.
# How do I edit the website?

There are two ways to edit the website:

-   Directly on the GitHub website
    
-   In local repositories
    

> **Note**
> All contributions are licensed under the [Apache Software License version 2.0](http://www.apache.org/licenses/LICENSE-2.0)

## Directly on the GitHub website

The website pages can be edited on the GitHub website. It’s a very quick process and ideal for fixing typos or updating information.

Steps to edit a file:

1.  Go to the page you want to edit.
    
2.  Look for a link called "Edit this Page" and click on it.
    
3.  Edit the file.
    
4.  Preview your changes.
    
5.  Provide a title and description for your pull request.
    
6.  Click on the "Propose file change" button.
    

> **Note**
> Check the top of the file for a comment such as "Copied from …​" or "Generated content". Do not use this process for such content. Also, much of the documentation is generated from other sources, including the java code and various configuration files. For such documentation, you will need to locate the original source and propose a change to it.

## In local repositories

To edit files locally, it’s important to understand how the website is generated and where the files are located. The configuration for the Antora and Hugo site generators is located in its [own repository](https://github.com/apache/camel-website). The documentation is located in the main [Apache Camel](https://github.com/apache/camel) repository and sub-project repositories, such as [Camel Spring Boot](https://github.com/apache/camel-spring-boot) and [Camel Quarkus](https://github.com/apache/camel-quarkus).

See [Improving the documentation](../improving-the-documentation.md) for instructions on how to work on the documentation.

> **Note**
> It’s a good idea to spend some time and learn how [Antora](https://antora.org) and [Hugo](https://gohugo.io/) work.
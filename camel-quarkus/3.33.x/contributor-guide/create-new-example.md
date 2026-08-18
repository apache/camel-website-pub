# Create a new example project

This guide outlines how to contribute a new example project to [camel-quarkus-examples](https://github.com/apache/camel-quarkus-examples).

1.  You should know [how to build](index.html#how-to-build).
    
2.  Make sure that nobody else works on the same example project already by searching through the [GitHub issues](https://github.com/apache/camel-quarkus/issues) or search the [examples label](https://github.com/apache/camel-quarkus/labels/example).
    
3.  Let others know that you work on the given example by either creating a [new issue](https://github.com/apache/camel-quarkus/issues/new) or asking to assign an existing one to you.
    
4.  Clone [camel-quarkus-examples](https://github.com/apache/camel-quarkus-examples) and check out the `camel-quarkus-main` branch.
    
5.  Scaffold a new example project using the `cq-maven-plugin`. For example, to add a new project named `yaml-to-log`:
    
    ```shell
    cd camel-quarkus-examples
    mvn org.l2x6.cq:cq-maven-plugin:create-example -Dcq.artifactIdBase="yaml-to-log" -Dcq.exampleName="YAML To Log" -Dcq.exampleDescription="Shows how to use a YAML route with the log EIP"
    ```
    
    Where:
    
    -   `cq.artifactIdBase` is the Maven `artifactId` to use on the project. It’s also used as the directory name for the generated project.
        
    -   `cq.exampleName` is a short descriptive name of the project. If you choose not to provide this, it’ll be determined from the value of `cq.artifactIdBase`.
        
    -   `cq.exampleDescription` is a longer description of the project.
        
    
6.  If the plugin execution completes successfully, change into the new project directory. You can test the project build with `mvn clean test`.
    
    You may now add your own routes, tests and README documentation. There are some `TODO` comments that show where to do this.
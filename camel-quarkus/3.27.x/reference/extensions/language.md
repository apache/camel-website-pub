# Language

JVM since1.1.0 Native since2.2.0

Execute scripts in any of the languages supported by Camel.

## What’s inside

-   [Language component](../../../../components/4.14.x/language-component.md), URI syntax: `language:languageName:resourceUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-language)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-language</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Required Dependencies

The Language extension only handles the passing of an Exchange to a script for execution. The extension implementing the language must be added as a dependency. The following list of languages are implemented in [Core](core.md):

-   Constant
    
-   ExchangeProperty
    
-   File
    
-   Header
    
-   Ref
    
-   Simple
    
-   Tokenize
    

To use any other language, you must add the corresponding dependency. Consult the [Languages Guide](../languages.md) for details.

### Native Mode

When loading scripts from the classpath in native mode, the path to the script file must be specified in the `quarkus.native.resources.includes` property of the `application.properties` file. For example:

```properties
quarkus.native.resources.includes=script.txt
```

## allowContextMapAll option in native mode

The `allowContextMapAll` option is not supported in native mode as it requires reflective access to security sensitive camel core classes such as `CamelContext` & `Exchange`. This is considered a security risk and thus access to the feature is not provided by default.
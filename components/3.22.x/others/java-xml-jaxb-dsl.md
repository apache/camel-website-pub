# Jaxb XML Dsl

**Since Camel 3.9**

The `xml-jaxb-dsl` is the original Camel XML DSL that are loaded via JAXB that is heavy and with overhead.

The JAXB parser is generic and can be used for parsing any XML. However, the `xml-io-dsl` is a source code generated parser that is Camel specific and can only parse Camel `.xml` route files (not classic Spring `<beans>` XML files).

If you are using Camel XML DSL then its recommended using `xml-io-dsl` instead of `xml-jaxb-dsl`. You can use this in all of Camel’s runtime such as Spring Boot, Quarkus, Camel Main, and Camel K etc.

If you use classic Spring `<beans>` XML files, or OSGi `<blueprint>` then you must use the `camel-jaxb-dsl`, which comes out of the box when using `camel-spring-xml` or `camel-blueprint`.

## See Also

See [DSL](../../../manual/dsl.md)
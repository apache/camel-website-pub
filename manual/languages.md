# Languages

To support flexible and powerful [Enterprise Integration Patterns](../components/4.22.x/eips/enterprise-integration-patterns.md), Camel supports various Languages to create an [Expression](expression.md) or [Predicate](predicate.md) within the [Routes](routes.md) and [DSL](dsl.md)..

## Supported languages

There are more than 25 different [Languages](../components/4.22.x/languages/index.md) such as scripted programming languages like Groovy, and template based languages like Velocity and Freemarker, and XML/JSon languages, and industry specifics such as Finance and Health Care, and many others.

Most of these languages are also supported used as [Annotation Based Expression Language](parameter-binding-annotations.md) in Java beans.

## Component-provided languages and tooling

A language can use the existing generic `LanguageExpression` without adding a dedicated expression model to Camel core. Register its implementation with `@Language(value = "myLanguage", modelName = "language")` and provide class-level `@Metadata` with `title`, `description`, `label`, and `firstVersion`. The package plugin generates its discovery entry and catalog metadata using the generic model. Existing languages retain their named core models by default.

Use `language("myLanguage", "expression")` in Java, `<language language="myLanguage">` in XML, or the generic `language:` expression in YAML. This registration does not add a native XML element, YAML key or Java builder method for the language. Configure language settings separately through Camel Main’s `camel.language.myLanguage.*` binding or its Language SPI.

The catalog entry describes the generic expression model, not the implementation’s global configuration properties. Downstream generators that derive configuration classes from language model options need separate support for those implementation settings.
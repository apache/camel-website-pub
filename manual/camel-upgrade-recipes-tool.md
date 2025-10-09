# Apache Camel Upgrade Recipes Project

This document provides instructions on how to use the automatic update tool to assist in the migration process.

## Introduction

To help with migration process, Camel Upgrade Recipes project based on OpenRewrite was developed.

> **Note**
> The project is not designed to provide fully automated migration but rather to assist with manual migrations, making them more efficient and less error-prone.

Refer to the [release notes](https://github.com/apache/camel-upgrade-recipes/blob/main/release_notes.adoc) of the Camel Upgrade Recipes Project to see the specific migrations covered by the upgrade tool.

## Running the Upgrade Tool

The migration tool is easy to run. To upgrade to the latest version of Camel, you can either execute the following script:

```bash
$ mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.recipeArtifactCoordinates=org.apache.camel.upgrade:camel-upgrade-recipes:LATEST -Drewrite.activeRecipes=org.apache.camel.upgrade.CamelMigrationRecipe
```

or use camel-jbang [update](camel-jbang.html#_update) action:

```bash
$ camel update run $VERSION
```
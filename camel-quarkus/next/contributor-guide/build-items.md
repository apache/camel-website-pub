# Camel Quarkus build items

Quarkus extensions pass information to each other at build time through build items produced and consumed by `@BuildStep` methods. This page lists the build items declared by the Camel Quarkus deployment modules. The build items provided by Quarkus itself are listed on the [Quarkus build items](https://quarkus.io/guides/all-builditems) page.

## Core

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.core.deployment.main.spi.CamelMainBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/main/spi/CamelMainBuildItem.java)
Holds the `CamelMain` `RuntimeValue`.

 | `RuntimeValue<CamelMain> main` |
| [`org.apache.camel.quarkus.core.deployment.main.spi.CamelMainListenerBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/main/spi/CamelMainListenerBuildItem.java)

A `MultiBuildItem` holding ``MainListener`s to add to `CamelMain``.

 | `RuntimeValue<MainListener> listener` |
| [`org.apache.camel.quarkus.core.deployment.spi.AnnouncedSyntheticBeanBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/AnnouncedSyntheticBeanBuildItem.java)

Announces a bean that another extension registers synthetically. `BeanDiscoveryFinishedBuildItem` lists class-based beans only, so a build step that counts beans of a type through it misses the synthetic ones; the extension knowing about such a bean produces one item per bean, naming the type it counts as and, for a bean qualified by a name, that name. A consumer looking for the default bean of a type must skip the named announcements: a named bean does not carry the `@Default` qualifier.

 | `DotName beanType`

`String name`

 |
| [`org.apache.camel.quarkus.core.deployment.spi.BuildTimeCamelCatalogBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/BuildTimeCamelCatalogBuildItem.java)

_No Javadoc found_

 | `BuildTimeCamelCatalog catalog` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelBeanBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelBeanBuildItem.java)

A `MultiBuildItem` holding beans to add to `org.apache.camel.spi.Registry` during `ExecutionTime#STATIC_INIT` phase.

You can use the sibling `CamelRuntimeBeanBuildItem` to register beans in the `ExecutionTime#RUNTIME_INIT` phase - i.e. those ones that cannot be produced during `ExecutionTime#STATIC_INIT` phase.

Note that the field type should refer to the most specialized class to avoid the issue described in [https://issues.apache.org/jira/browse/CAMEL-13948](https://issues.apache.org/jira/browse/CAMEL-13948).

 | `String name`

`String type`

`RuntimeValue<?> value`

 |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelBeanQualifierResolverBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelBeanQualifierResolverBuildItem.java)

Holds a `CamelBeanQualifierResolver` for a specified bean type.

 | `RuntimeValue<CamelBeanQualifierResolver> runtimeValue`

`Class<?> beanType`

`String beanName`

 |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelBootClockBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelBootClockBuildItem.java)

_No Javadoc found_

 | `RuntimeValue<Clock> bootClockRuntimeValue` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelBootstrapCompletedBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelBootstrapCompletedBuildItem.java)

A build item that does not carry any data but it is used to signal that all the bootstrap steps have been completed.

 | None |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelComponentNameResolverBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelComponentNameResolverBuildItem.java)

Holds the `ComponentNameResolver` `RuntimeValue`.

 | `RuntimeValue<ComponentNameResolver> value` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelContextBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelContextBuildItem.java)

Holds the `CamelContext` `RuntimeValue`.

 | `RuntimeValue<CamelContext> value` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelContextCustomizerBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelContextCustomizerBuildItem.java)

A `MultiBuildItem` holding the `CamelContextCustomizer` `RuntimeValue` and could be used to customize the camel context before produce the `CamelContextBuildItem`

 | `RuntimeValue<CamelContextCustomizer> value` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelFactoryFinderResolverBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelFactoryFinderResolverBuildItem.java)

A `SimpleBuildItem` holding a `FactoryFinderResolver` `RuntimeValue`.

 | `RuntimeValue<FactoryFinderResolver> factoryFinderResolver` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelModelJAXBContextFactoryBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelModelJAXBContextFactoryBuildItem.java)

Holds the `ModelJAXBContextFactory` instance.

 | `RuntimeValue<ModelJAXBContextFactory> value` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelModelReifierFactoryBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelModelReifierFactoryBuildItem.java)

A `SimpleBuildItem` holding a `ModelReifierFactory` `RuntimeValue`.

 | `RuntimeValue<ModelReifierFactory> modelReifierFactory` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelModelToXMLDumperBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelModelToXMLDumperBuildItem.java)

_No Javadoc found_

 | `RuntimeValue<ModelToXMLDumper> value` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelModelToYAMLDumperBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelModelToYAMLDumperBuildItem.java)

_No Javadoc found_

 | `RuntimeValue<ModelToYAMLDumper> value` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelPackageScanClassBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelPackageScanClassBuildItem.java)

A `MultiBuildItem` holding the names of a types that will be scanned by the Camel PackageScanClassResolver.

 | `Set<String> classNames` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelPackageScanClassResolverBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelPackageScanClassResolverBuildItem.java)

Holds the `PackageScanClassResolver` `RuntimeValue`.

 | `RuntimeValue<PackageScanClassResolver> value` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelRegistryBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelRegistryBuildItem.java)

Holds the `Registry` `RuntimeValue`. It is made available after the beans from ``CamelBeanBuildItem`s were registered in the underlying `Registry``.

 | `RuntimeValue<Registry> value` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelRouteResourceBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelRouteResourceBuildItem.java)

Holds a `Resource` relating to discovered Camel DSL route definition files defined by route inclusion patterns configuration.

 | `String location`

`String sourcePath`

`boolean isHotReloadable`

 |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelRoutesBuilderClassBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelRoutesBuilderClassBuildItem.java)

A `MultiBuildItem` holding class names of all `RoutesBuilder` implementations.

The class names are gathered from Jandex by `camel-quarkus-core`. Extensions are free to add \`CamelRoutesBuilderClassBuildItem\`s programmatically.

 | `DotName dotName` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelRuntimeBeanBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelRuntimeBeanBuildItem.java)

A `MultiBuildItem` holding beans to add to `org.apache.camel.spi.Registry` during `ExecutionTime#RUNTIME_INIT` phase.

You should use the sibling `CamelBeanBuildItem` for all beans that can be produced during `ExecutionTime#STATIC_INIT` phase.

Note that the field type should refer to the most specialized class to avoid the issue described in [https://issues.apache.org/jira/browse/CAMEL-13948](https://issues.apache.org/jira/browse/CAMEL-13948).

 | `String name`

`String type`

`RuntimeValue<?> value`

 |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelRuntimeBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelRuntimeBuildItem.java)

_No Javadoc found_

 | `RuntimeValue<CamelRuntime> runtime`

`boolean autoStartup`

 |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelRuntimeTaskBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelRuntimeTaskBuildItem.java)

Marker used as synchronization item for Build Steps to ensure all the Build Steps that need to record `ExecutionTime#RUNTIME_INIT`.

As example some beans can be bound to the `org.apache.camel.spi.Registry` at `ExecutionTime#STATIC_INIT` but others can only be bound at `ExecutionTime#RUNTIME_INIT` and to be sure that the binding happens before the `org.apache.camel.quarkus.core.CamelRuntime` is assembled and started a CamelRuntimeTaskBuildItem is produced and the Build Steps producing `CamelRuntimeBuildItem` depends on it.

The initial barrier required two symmetric Build Items:

-   CamelRegistryBuildItem
    
-   CamelRuntimeRegistryBuildItem
    

Where the second Build Item was useless except for synchronization purpose and has been replaced to this generic CamelRuntimeTaskBuildItem.

 | `String name` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelSerializationBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelSerializationBuildItem.java)

Signal that the basic classes listed in `org.apache.camel.quarkus.core.deployment.CamelSerializationProcessor.BASE_SERIALIZATION_CLASSES`, together with any additional classes passed to this build item, should be registered for serialization.

Registrations requested via this build item can be vetoed by the user with `quarkus.camel.native.reflection.serialization-enabled=false`. Extensions that need the base set of classes must therefore route their serialization registrations through this build item, instead of producing `ReflectiveClassBuildItem.serializationClass(..)` directly.

 | `List<String> classNames` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelServiceBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelServiceBuildItem.java)

A `MultiBuildItem` holding information about a service defined in a property file somewhere under `META-INF/services/org/apache/camel`.

 | `Path path`

`String name`

`String type`

 |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelServiceFilterBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelServiceFilterBuildItem.java)

_No Javadoc found_

 | `CamelServiceFilter predicate` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelServicePatternBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelServicePatternBuildItem.java)

A `MultiBuildItem` holding a collection of path patterns to select files under `META-INF/services/org/apache/camel` which define discoverable Camel services.

 | `CamelServiceDestination destination`

`boolean include`

`List<String> patterns`

 |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelTypeConverterLoaderBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelTypeConverterLoaderBuildItem.java)

Holds the `TypeConverterLoader` `RuntimeValue`.

 | `RuntimeValue<TypeConverterLoader> value` |
| [`org.apache.camel.quarkus.core.deployment.spi.CamelTypeConverterRegistryBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CamelTypeConverterRegistryBuildItem.java)

Holds the `org.apache.camel.spi.TypeConverterRegistry` `RuntimeValue`.

 | `RuntimeValue<TypeConverterRegistry> value` |
| [`org.apache.camel.quarkus.core.deployment.spi.CompiledCSimpleExpressionBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/CompiledCSimpleExpressionBuildItem.java)

A `MultiBuildItem` bearing info about a compiled CSimple language expression.

 | `String sourceCode`

`String className`

`boolean predicate`

 |
| [`org.apache.camel.quarkus.core.deployment.spi.ContainerBeansBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/ContainerBeansBuildItem.java)

Hold a set of beans known to the ArC container.

 | `Set<CamelBeanInfo> beans`

`Set<DotName> classes`

 |
| [`org.apache.camel.quarkus.core.deployment.spi.RoutesBuilderClassExcludeBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/RoutesBuilderClassExcludeBuildItem.java)

A `MultiBuildItem` holding patterns whose matching classes will be excluded from the set of classes from which routes will be instantiated. This is a programmatic way of doing the same thing as can be done via `RoutesDiscoveryConfig#excludePatterns`.

 | `String pattern` |
| [`org.apache.camel.quarkus.core.deployment.spi.RuntimeCamelContextCustomizerBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/spi/RuntimeCamelContextCustomizerBuildItem.java)

A `MultiBuildItem` holding the `CamelContextCustomizer` `RuntimeValue` and could be used to customize the camel context before starting it.

 | `RuntimeValue<CamelContextCustomizer> value` |

## BeanIO

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.component.beanio.deployment.BeanioPropertiesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/beanio/deployment/src/main/java/org/apache/camel/quarkus/component/beanio/deployment/BeanioPropertiesBuildItem.java)
_No Javadoc found_

 | `Properties properties` |

## CSimple

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.component.csimple.deployment.CSimpleExpressionSourceBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/csimple/deployment/src/main/java/org/apache/camel/quarkus/component/csimple/deployment/CSimpleExpressionSourceBuildItem.java)
A `MultiBuildItem` bearing info about a CSimple language expression that needs to get compiled.

 | `String sourceCode`

`String classNameBase`

`boolean predicate`

 |

## DataSonnet

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.component.datasonnet.deployment.DatasonnetLibrariesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/datasonnet/deployment/src/main/java/org/apache/camel/quarkus/component/datasonnet/deployment/DatasonnetLibrariesBuildItem.java)
_No Javadoc found_

 | `Map<String,String> libraries` |

## FHIR

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.component.fhir.deployment.AbstractPropertiesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/fhir/deployment/src/main/java/org/apache/camel/quarkus/component/fhir/deployment/AbstractPropertiesBuildItem.java)
_No Javadoc found_

 | `Map<String,String> properties` |
| [`org.apache.camel.quarkus.component.fhir.deployment.dstu2.Dstu2PropertiesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/fhir/deployment/src/main/java/org/apache/camel/quarkus/component/fhir/deployment/dstu2/Dstu2PropertiesBuildItem.java)

_No Javadoc found_

 | None |
| [`org.apache.camel.quarkus.component.fhir.deployment.dstu2Hl7Org.Dstu2Hl7OrgPropertiesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/fhir/deployment/src/main/java/org/apache/camel/quarkus/component/fhir/deployment/dstu2Hl7Org/Dstu2Hl7OrgPropertiesBuildItem.java)

_No Javadoc found_

 | None |
| [`org.apache.camel.quarkus.component.fhir.deployment.dstu2_1.Dstu2_1PropertiesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/fhir/deployment/src/main/java/org/apache/camel/quarkus/component/fhir/deployment/dstu2_1/Dstu2_1PropertiesBuildItem.java)

_No Javadoc found_

 | None |
| [`org.apache.camel.quarkus.component.fhir.deployment.dstu3.Dstu3PropertiesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/fhir/deployment/src/main/java/org/apache/camel/quarkus/component/fhir/deployment/dstu3/Dstu3PropertiesBuildItem.java)

_No Javadoc found_

 | None |
| [`org.apache.camel.quarkus.component.fhir.deployment.r4.R4PropertiesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/fhir/deployment/src/main/java/org/apache/camel/quarkus/component/fhir/deployment/r4/R4PropertiesBuildItem.java)

_No Javadoc found_

 | None |
| [`org.apache.camel.quarkus.component.fhir.deployment.r5.R5PropertiesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/fhir/deployment/src/main/java/org/apache/camel/quarkus/component/fhir/deployment/r5/R5PropertiesBuildItem.java)

_No Javadoc found_

 | None |

## Groovy

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.component.groovy.deployment.GroovyExpressionSourceBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/groovy/deployment/src/main/java/org/apache/camel/quarkus/component/groovy/deployment/GroovyExpressionSourceBuildItem.java)
A `MultiBuildItem` bearing info about a Groovy language expression that needs to get compiled.

 | `String sourceCode`

`String originalCode`

`String className`

 |

## Java jOOR DSL

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.dsl.java.joor.deployment.JavaJoorGeneratedClassBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/java-joor-dsl/deployment/src/main/java/org/apache/camel/quarkus/dsl/java/joor/deployment/JavaJoorGeneratedClassBuildItem.java)
_No Javadoc found_

 | `String name`

`String location`

`byte[] classData`

 |

## jOOR

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.component.joor.deployment.JoorExpressionSourceBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/joor/deployment/src/main/java/org/apache/camel/quarkus/component/joor/deployment/JoorExpressionSourceBuildItem.java)
A `MultiBuildItem` bearing info about a jOOR language expression that needs to get compiled.

 | `String sourceCode`

`String className`

`String id`

`boolean script`

 |

## LangChain4j Embedding Store

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.component.langchain4j.embeddingstore.deployment.DefaultRetrievalAugmentorBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/langchain4j-embeddingstore/deployment/src/main/java/org/apache/camel/quarkus/component/langchain4j/embeddingstore/deployment/DefaultRetrievalAugmentorBuildItem.java)
Produced when the auto-detected default `RetrievalAugmentor` is registered, so that its `@Default` store and model can be verified once the synthetic beans exist.

 | None |

## MapStruct

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.component.mapstruct.deployment.ConversionMethodInfoRuntimeValuesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/mapstruct/deployment/src/main/java/org/apache/camel/quarkus/component/mapstruct/deployment/ConversionMethodInfoRuntimeValuesBuildItem.java)
Holds info about generated TypeConverter ConversionMethod.

 | `Set<RuntimeValue<ConversionMethodInfo>> conversionMethodInfoRuntimeValues` |
| [`org.apache.camel.quarkus.component.mapstruct.deployment.MapStructMapperPackagesBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/mapstruct/deployment/src/main/java/org/apache/camel/quarkus/component/mapstruct/deployment/MapStructMapperPackagesBuildItem.java)

Holds the set of discovered MapStruct Mapper packages.

 | `Set<String> mapperPackages` |

## Platform HTTP

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.component.platform.http.deployment.PlatformHttpEngineBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/platform-http/deployment/src/main/java/org/apache/camel/quarkus/component/platform/http/deployment/PlatformHttpEngineBuildItem.java)
Holds the `PlatformHttpEngine` `RuntimeValue`.

 | `RuntimeValue<PlatformHttpEngine> instance` |

## Support Bouncy Castle

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.support.bouncycastle.deployment.BouncyCastleAdditionalProviderBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-support/bouncycastle/deployment/src/main/java/org/apache/camel/quarkus/support/bouncycastle/deployment/BouncyCastleAdditionalProviderBuildItem.java)
In case that non-default BC provider has to be registered, use this buildItem. (provider available for registration is `BCPQC`)

 | `String proivderName` |
| [`org.apache.camel.quarkus.support.bouncycastle.deployment.CipherTransformationBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-support/bouncycastle/deployment/src/main/java/org/apache/camel/quarkus/support/bouncycastle/deployment/CipherTransformationBuildItem.java)

A `MultiBuildItem` holding cipher transformations to be explicitly registered as security services. Extensions should provide all cipher transformations that are reachable at runtime. Those cipher transformations will be explicitly instantiated at bootstrap so that graal can proceed with security services automatic registration.

 | `List<String> cipherTransformations` |

## Support DSL

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.support.dsl.deployment.DslGeneratedClassBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-support/dsl/deployment/src/main/java/org/apache/camel/quarkus/support/dsl/deployment/DslGeneratedClassBuildItem.java)
_No Javadoc found_

 | `String name`

`String location`

`boolean instantiateWithCamelContext`

 |

## Support Language

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.support.language.deployment.ExpressionBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-support/language/deployment/src/main/java/org/apache/camel/quarkus/support/language/deployment/ExpressionBuildItem.java)
`ExpressionBuildItem` represents an expression in a given language that has been extracted from the route definitions.

 | `String language`

`String expression`

`String loadedExpression`

`boolean predicate`

`Object[] properties`

 |
| [`org.apache.camel.quarkus.support.language.deployment.ExpressionExtractionResultBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-support/language/deployment/src/main/java/org/apache/camel/quarkus/support/language/deployment/ExpressionExtractionResultBuildItem.java)

`ExpressionBuildItem` represents the result of the expression extraction process.

 | `boolean success` |
| [`org.apache.camel.quarkus.support.language.deployment.ScriptBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions-support/language/deployment/src/main/java/org/apache/camel/quarkus/support/language/deployment/ScriptBuildItem.java)

`ScriptBuildItem` represents a script and its binding context in a given language that has been extracted from the route definitions.

 | `String language`

`String content`

`String loadedContent`

`Map<String,Object> bindings`

 |

## XSLT

 
| Class name | Attributes |
| --- | --- |
| [`org.apache.camel.quarkus.component.xslt.deployment.UriResolverEntryBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/xslt/deployment/src/main/java/org/apache/camel/quarkus/component/xslt/deployment/UriResolverEntryBuildItem.java)
Holds a pair of XSLT template URI and the unqualified translet name to use when creating a `RuntimeUriResolver`.

 | `String templateUri`

`String transletClassName`

 |
| [`org.apache.camel.quarkus.component.xslt.deployment.XsltGeneratedClassBuildItem`](https://github.com/apache/camel-quarkus/blob/main/extensions/xslt/deployment/src/main/java/org/apache/camel/quarkus/component/xslt/deployment/XsltGeneratedClassBuildItem.java)

A `MultiBuildItem` holding names of the XSLT translets (and possibly also names of their ancillary classes) generated at build time.

 | `String className` |
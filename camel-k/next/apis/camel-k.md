# Camel K API

## camel.apache.org/v1

Package v1 contains API Schema definitions for the camel v1 API group

## Resource Types

### Build

Build is the Schema for the builds API.

 
| Field | Description |
| --- | --- |
| `apiVersion`  
string | `camel.apache.org/v1` |
| `kind`  
string | `Build` |
| `metadata`  
**[Kubernetes meta/v1.ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectmeta-v1-meta)** | Refer to the Kubernetes API documentation for the fields of the `metadata` field. |
| `spec`  
**[BuildSpec](#_camel_apache_org_v1_BuildSpec)** | 
 |
| `status`  
**[BuildStatus](#_camel_apache_org_v1_BuildStatus)** | 

 |

### CamelCatalog

CamelCatalog represents the languages, components, data formats and capabilities enabled on a given runtime provider. The catalog may be statically generated.

 
| Field | Description |
| --- | --- |
| `apiVersion`  
string | `camel.apache.org/v1` |
| `kind`  
string | `CamelCatalog` |
| `metadata`  
**[Kubernetes meta/v1.ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectmeta-v1-meta)** | Refer to the Kubernetes API documentation for the fields of the `metadata` field. |
| `status`  
**[CamelCatalogStatus](#_camel_apache_org_v1_CamelCatalogStatus)** | the actual state of the catalog |
| `spec`  
**[CamelCatalogSpec](#_camel_apache_org_v1_CamelCatalogSpec)** | the desired state of the catalog |

### Integration

Integration is the Schema for the integrations API.

 
| Field | Description |
| --- | --- |
| `apiVersion`  
string | `camel.apache.org/v1` |
| `kind`  
string | `Integration` |
| `metadata`  
**[Kubernetes meta/v1.ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectmeta-v1-meta)** | Refer to the Kubernetes API documentation for the fields of the `metadata` field. |
| `spec`  
**[IntegrationSpec](#_camel_apache_org_v1_IntegrationSpec)** | the desired Integration specification |
| `status`  
**[IntegrationStatus](#_camel_apache_org_v1_IntegrationStatus)** | the status of the Integration |

### IntegrationKit

IntegrationKit defines a container image and additional configuration needed to run an `Integration`. An `IntegrationKit` is a generic image generally built from the requirements of an `Integration`, but agnostic to it, in order to be reused by any other `Integration` which has the same required set of capabilities. An `IntegrationKit` may be used for other kits as a base container layer, when the `incremental` build option is enabled.

 
| Field | Description |
| --- | --- |
| `apiVersion`  
string | `camel.apache.org/v1` |
| `kind`  
string | `IntegrationKit` |
| `metadata`  
**[Kubernetes meta/v1.ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectmeta-v1-meta)** | Refer to the Kubernetes API documentation for the fields of the `metadata` field. |
| `spec`  
**[IntegrationKitSpec](#_camel_apache_org_v1_IntegrationKitSpec)** | the desired configuration |
| `status`  
**[IntegrationKitStatus](#_camel_apache_org_v1_IntegrationKitStatus)** | the actual status |

### IntegrationPlatform

IntegrationPlatform is the resource used to drive the Camel K operator behavior. It defines the behavior of all Custom Resources (`IntegrationKit`, `Integration`, `Kamelet`) in the given namespace. When the Camel K operator is installed in `global` mode, you will need to specify an `IntegrationPlatform` in each namespace where you want the Camel K operator to be executed.

Deprecated: see documentation to switch to environment variable based configuration.

 
| Field | Description |
| --- | --- |
| `apiVersion`  
string | `camel.apache.org/v1` |
| `kind`  
string | `IntegrationPlatform` |
| `metadata`  
**[Kubernetes meta/v1.ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectmeta-v1-meta)** | Refer to the Kubernetes API documentation for the fields of the `metadata` field. |
| `spec`  
**[IntegrationPlatformSpec](#_camel_apache_org_v1_IntegrationPlatformSpec)** | 
 |
| `status`  
**[IntegrationPlatformStatus](#_camel_apache_org_v1_IntegrationPlatformStatus)** | 

 |

### IntegrationProfile

IntegrationProfile is the resource used to apply user defined settings to the Camel K operator behavior. It defines the behavior of all Custom Resources (`IntegrationKit`, `Integration`, `Kamelet`) in the given namespace.

 
| Field | Description |
| --- | --- |
| `apiVersion`  
string | `camel.apache.org/v1` |
| `kind`  
string | `IntegrationProfile` |
| `metadata`  
**[Kubernetes meta/v1.ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectmeta-v1-meta)** | Refer to the Kubernetes API documentation for the fields of the `metadata` field. |
| `spec`  
**[IntegrationProfileSpec](#_camel_apache_org_v1_IntegrationProfileSpec)** | 
 |
| `status`  
**[IntegrationProfileStatus](#_camel_apache_org_v1_IntegrationProfileStatus)** | Deprecated: no longer in use. |

### Kamelet

Kamelet is the Schema for the kamelets API.

 
| Field | Description |
| --- | --- |
| `apiVersion`  
string | `camel.apache.org/v1` |
| `kind`  
string | `Kamelet` |
| `metadata`  
**[Kubernetes meta/v1.ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectmeta-v1-meta)** | Refer to the Kubernetes API documentation for the fields of the `metadata` field. |
| `spec`  
**[KameletSpec](#_camel_apache_org_v1_KameletSpec)** | the desired specification |
| `status`  
**[KameletStatus](#_camel_apache_org_v1_KameletStatus)** | the actual status of the resource Deprecated no longer in use |

### Pipe

Pipe is the Schema for the Pipe API.

 
| Field | Description |
| --- | --- |
| `apiVersion`  
string | `camel.apache.org/v1` |
| `kind`  
string | `Pipe` |
| `metadata`  
**[Kubernetes meta/v1.ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectmeta-v1-meta)** | Refer to the Kubernetes API documentation for the fields of the `metadata` field. |
| `spec`  
**[PipeSpec](#_camel_apache_org_v1_PipeSpec)** | the specification of a Pipe |
| `status`  
**[PipeStatus](#_camel_apache_org_v1_PipeStatus)** | the status of a Pipe |

## Internal Types

### AddonTrait

**Appears on:**

-   [IntegrationKitTraits](#_camel_apache_org_v1_IntegrationKitTraits)
    
-   [Traits](#_camel_apache_org_v1_Traits)
    

AddonTrait represents the configuration of an addon trait.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.)
Generic raw message, typically a map containing the keys (trait parameters) and the values (either single text or array)

 |

### Args

**Appears on:**

-   [Container](#_camel_apache_org_v1_Container)
    

Args — .

 
| Field | Description |
| --- | --- |
| `arg`  
string | 
 |

### Artifact

**Appears on:**

-   [BuildStatus](#_camel_apache_org_v1_BuildStatus)
    
-   [IntegrationKitStatus](#_camel_apache_org_v1_IntegrationKitStatus)
    

Artifact represents a materialized artifact (a jar dependency or in general a file used by the build).

 
| Field | Description |
| --- | --- |
| `id`  
string | the identification (GAV for maven dependencies or file name for other file types) |
| `location`  
string | where it is located in the builder `Pod` |
| `target`  
string | the expected location in the runtime |
| `checksum`  
string | a checksum (SHA1) of the content |

### BaseTask

**Appears on:**

-   [BuildahTask](#_camel_apache_org_v1_BuildahTask)
    
-   [BuilderTask](#_camel_apache_org_v1_BuilderTask)
    
-   [JibTask](#_camel_apache_org_v1_JibTask)
    
-   [KanikoTask](#_camel_apache_org_v1_KanikoTask)
    
-   [S2iTask](#_camel_apache_org_v1_S2iTask)
    
-   [SpectrumTask](#_camel_apache_org_v1_SpectrumTask)
    
-   [UserTask](#_camel_apache_org_v1_UserTask)
    

BaseTask is a base for the struct hierarchy.

 
| Field | Description |
| --- | --- |
| `name`  
string | name of the task |
| `configuration`  
**[BuildConfiguration](#_camel_apache_org_v1_BuildConfiguration)** | The configuration that should be used to perform the Build. |

### BeanProperties

BeanProperties represent an unstructured object properties to be set on a bean.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.) |

### BuildCondition

**Appears on:**

-   [BuildStatus](#_camel_apache_org_v1_BuildStatus)
    

BuildCondition describes the state of a resource at a certain point.

 
| Field | Description |
| --- | --- |
| `type`  
**[BuildConditionType](#_camel_apache_org_v1_BuildConditionType)** | Type of integration condition. |
| `status`  
**[Kubernetes core/v1.ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#conditionstatus-v1-core)** | Status of the condition, one of True, False, Unknown. |
| `lastUpdateTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | The last time this condition was updated. |
| `lastTransitionTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | Last time the condition transitioned from one status to another. |
| `reason`  
string | The reason for the condition’s last transition. |
| `message`  
string | A human-readable message indicating details about the transition. |

### BuildConditionType(`string` alias)

**Appears on:**

-   [BuildCondition](#_camel_apache_org_v1_BuildCondition)
    

BuildConditionType — .

### BuildConfiguration

**Appears on:**

-   [BaseTask](#_camel_apache_org_v1_BaseTask)
    
-   [BuildSpec](#_camel_apache_org_v1_BuildSpec)
    
-   [IntegrationPlatformBuildSpec](#_camel_apache_org_v1_IntegrationPlatformBuildSpec)
    

BuildConfiguration represent the configuration required to build the runtime.

 
| Field | Description |
| --- | --- |
| `toolImage`  
string | The container image to be used to run the build. |
| `operatorNamespace`  
string | The namespace where to run the builder Pod (must be the same of the operator in charge of this Build reconciliation).
Deprecated: no longer in use.

 |
| `strategy`  
**[BuildStrategy](#_camel_apache_org_v1_BuildStrategy)** | the strategy to adopt |
| `orderStrategy`  
**[BuildOrderStrategy](#_camel_apache_org_v1_BuildOrderStrategy)** | the build order strategy to adopt |
| `requestCPU`  
string | The minimum amount of CPU required. Only used for `pod` strategy |
| `requestMemory`  
string | The minimum amount of memory required. Only used for `pod` strategy |
| `limitCPU`  
string | The maximum amount of CPU required. Only used for `pod` strategy |
| `limitMemory`  
string | The maximum amount of memory required. Only used for `pod` strategy |
| `nodeSelector`  
map\[string\]string | The node selector for the builder pod. Only used for `pod` strategy |
| `annotations`  
map\[string\]string | Annotation to use for the builder pod. Only used for `pod` strategy |
| `platforms`  
\[\]string | The list of platforms used in order to build a container image. |

### BuildOrderStrategy(`string` alias)

**Appears on:**

-   [BuildConfiguration](#_camel_apache_org_v1_BuildConfiguration)
    

BuildOrderStrategy specifies how builds are reconciled and queued.

### BuildPhase(`string` alias)

**Appears on:**

-   [BuildStatus](#_camel_apache_org_v1_BuildStatus)
    

BuildPhase — .

### BuildSpec

**Appears on:**

-   [Build](#_camel_apache_org_v1_Build)
    

BuildSpec defines the list of tasks to be execute for a Build. From Camel K version 2, it would be more appropriate to think it as pipeline.

 
| Field | Description |
| --- | --- |
| `tasks`  
**[\[\]Task](#_camel_apache_org_v1_Task)** | The sequence of tasks (pipeline) to be performed. |
| `configuration`  
**[BuildConfiguration](#_camel_apache_org_v1_BuildConfiguration)** | The configuration that should be used to perform the Build.
Deprecated: no longer in use in Camel K 2 - maintained for backward compatibility

 |
| `toolImage`  
string | The container image to be used to run the build.

Deprecated: no longer in use in Camel K 2 - maintained for backward compatibility

 |
| `operatorNamespace`  
string | The namespace where to run the builder Pod (must be the same of the operator in charge of this Build reconciliation).

Deprecated: no longer in use in Camel K 2 - maintained for backward compatibility

 |
| `timeout`  
**[Kubernetes meta/v1.Duration](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#duration-v1-meta)** | Timeout defines the Build maximum execution duration. The Build deadline is set to the Build start time plus the Timeout duration. If the Build deadline is exceeded, the Build context is canceled, and its phase set to BuildPhaseFailed. |
| `maxRunningBuilds`  
int32 | the maximum amount of parallel running builds started by this operator instance.

Deprecated: no longer in use in Camel K 2 - maintained for backward compatibility

 |

### BuildStatus

**Appears on:**

-   [Build](#_camel_apache_org_v1_Build)
    

BuildStatus defines the observed state of Build.

 
| Field | Description |
| --- | --- |
| `observedGeneration`  
int64 | ObservedGeneration is the most recent generation observed for this Build. |
| `phase`  
**[BuildPhase](#_camel_apache_org_v1_BuildPhase)** | describes the phase |
| `image`  
string | the image name built |
| `digest`  
string | the digest from image |
| `rootImage`  
string | root image (the first image from which the incremental image has started) |
| `baseImage`  
string | the base image used for this build |
| `artifacts`  
**[\[\]Artifact](#_camel_apache_org_v1_Artifact)** | a list of artifacts contained in the build |
| `error`  
string | the error description (if any) |
| `failure`  
**[Failure](#_camel_apache_org_v1_Failure)** | the reason of the failure (if any) |
| `startedAt`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | the time when it started |
| `conditions`  
**[\[\]BuildCondition](#_camel_apache_org_v1_BuildCondition)** | a list of conditions occurred during the build |
| `duration`  
string | how long it took for the build Change to Duration / ISO 8601 when CRD uses OpenAPI spec v3 [https://github.com/OAI/OpenAPI-Specification/issues/845](https://github.com/OAI/OpenAPI-Specification/issues/845) |

### BuildStrategy(`string` alias)

**Appears on:**

-   [BuildConfiguration](#_camel_apache_org_v1_BuildConfiguration)
    

BuildStrategy specifies how the Build should be executed. It will trigger a Maven process (either as an Operator routine or Kubernetes Pod execution) that will take care of producing the expected Camel/Camel-Quarkus runtime.

### BuildahTask

**Appears on:**

-   [Task](#_camel_apache_org_v1_Task)
    

BuildahTask is used to configure Buildah.

Deprecated: no longer in use.

 
| Field | Description |
| --- | --- |
| `BaseTask`  
**[BaseTask](#_camel_apache_org_v1_BaseTask)** | (Members of `BaseTask` are embedded into this type.) |
| `PublishTask`  
**[PublishTask](#_camel_apache_org_v1_PublishTask)** | (Members of `PublishTask` are embedded into this type.) |
| `platform`  
string | The platform of build image |
| `verbose`  
bool | log more information |
| `executorImage`  
string | docker image to use |

### BuilderTask

**Appears on:**

-   [Task](#_camel_apache_org_v1_Task)
    

BuilderTask is the generic task in charge of building the application image.

 
| Field | Description |
| --- | --- |
| `BaseTask`  
**[BaseTask](#_camel_apache_org_v1_BaseTask)** | (Members of `BaseTask` are embedded into this type.) |
| `baseImage`  
string | the base image layer |
| `runtime`  
**[RuntimeSpec](#_camel_apache_org_v1_RuntimeSpec)** | the configuration required for the runtime application |
| `dependencies`  
\[\]string | the list of dependencies to use for this build |
| `steps`  
\[\]string | the list of steps to execute (see pkg/builder/) |
| `maven`  
**[MavenBuildSpec](#_camel_apache_org_v1_MavenBuildSpec)** | the configuration required by Maven for the application build phase |
| `buildDir`  
string | workspace directory to use |
| `sources`  
**[\[\]SourceSpec](#_camel_apache_org_v1_SourceSpec)** | the sources to add at build time |
| `git`  
**[GitConfigSpec](#_camel_apache_org_v1_GitConfigSpec)** | the configuration of the project to build on Git |

### CamelArtifact

**Appears on:**

-   [CamelCatalogSpec](#_camel_apache_org_v1_CamelCatalogSpec)
    

CamelArtifact represent the configuration for a feature offered by Camel.

 
| Field | Description |
| --- | --- |
| `CamelArtifactDependency`  
**[CamelArtifactDependency](#_camel_apache_org_v1_CamelArtifactDependency)** | (Members of `CamelArtifactDependency` are embedded into this type.)
Base Camel Artifact dependency

 |
| `schemes`  
**[\[\]CamelScheme](#_camel_apache_org_v1_CamelScheme)** | accepted URI schemes |
| `languages`  
\[\]string | accepted languages |
| `dataformats`  
\[\]string | accepted data formats |
| `dependencies`  
**[\[\]CamelArtifactDependency](#_camel_apache_org_v1_CamelArtifactDependency)** | required dependencies |
| `javaTypes`  
\[\]string | the Java types used by the artifact feature (ie, component, data format, …​) |

### CamelArtifactDependency

**Appears on:**

-   [CamelArtifact](#_camel_apache_org_v1_CamelArtifact)
    
-   [CamelSchemeScope](#_camel_apache_org_v1_CamelSchemeScope)
    

CamelArtifactDependency represent a maven’s dependency.

 
| Field | Description |
| --- | --- |
| `MavenArtifact`  
**[MavenArtifact](#_camel_apache_org_v1_MavenArtifact)** | (Members of `MavenArtifact` are embedded into this type.)
the maven dependency

 |
| `exclusions`  
**[\[\]CamelArtifactExclusion](#_camel_apache_org_v1_CamelArtifactExclusion)** | provide a list of artifacts to exclude for this dependency |

### CamelArtifactExclusion

**Appears on:**

-   [CamelArtifactDependency](#_camel_apache_org_v1_CamelArtifactDependency)
    

CamelArtifactExclusion represents an exclusion clause.

 
| Field | Description |
| --- | --- |
| `groupId`  
string | Maven Group |
| `artifactId`  
string | Maven Artifact |

### CamelCatalogCondition

**Appears on:**

-   [CamelCatalogStatus](#_camel_apache_org_v1_CamelCatalogStatus)
    

CamelCatalogCondition describes the state of a resource at a certain point.

 
| Field | Description |
| --- | --- |
| `type`  
**[CamelCatalogConditionType](#_camel_apache_org_v1_CamelCatalogConditionType)** | Type of CamelCatalog condition. |
| `status`  
**[Kubernetes core/v1.ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#conditionstatus-v1-core)** | Status of the condition, one of True, False, Unknown. |
| `lastUpdateTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | The last time this condition was updated. |
| `lastTransitionTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | Last time the condition transitioned from one status to another. |
| `reason`  
string | The reason for the condition’s last transition. |
| `message`  
string | A human-readable message indicating details about the transition. |

### CamelCatalogConditionType(`string` alias)

**Appears on:**

-   [CamelCatalogCondition](#_camel_apache_org_v1_CamelCatalogCondition)
    

CamelCatalogConditionType --.

### CamelCatalogPhase(`string` alias)

**Appears on:**

-   [CamelCatalogStatus](#_camel_apache_org_v1_CamelCatalogStatus)
    

CamelCatalogPhase — .

### CamelCatalogSpec

**Appears on:**

-   [CamelCatalog](#_camel_apache_org_v1_CamelCatalog)
    

CamelCatalogSpec specify what features a Camel runtime provides.

 
| Field | Description |
| --- | --- |
| `runtime`  
**[RuntimeSpec](#_camel_apache_org_v1_RuntimeSpec)** | the runtime targeted for the catalog |
| `artifacts`  
**[map\[string\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.CamelArtifact](#_camel_apache_org_v1_CamelArtifact)** | artifacts required by this catalog |
| `loaders`  
**[map\[string\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.CamelLoader](#_camel_apache_org_v1_CamelLoader)** | loaders required by this catalog |

### CamelCatalogStatus

**Appears on:**

-   [CamelCatalog](#_camel_apache_org_v1_CamelCatalog)
    

CamelCatalogStatus defines the observed state of CamelCatalog.

 
| Field | Description |
| --- | --- |
| `observedGeneration`  
int64 | ObservedGeneration is the most recent generation observed for this Catalog. |
| `phase`  
**[CamelCatalogPhase](#_camel_apache_org_v1_CamelCatalogPhase)** | the actual phase |
| `conditions`  
**[\[\]CamelCatalogCondition](#_camel_apache_org_v1_CamelCatalogCondition)** | a list of events happened for the CamelCatalog |
| `image`  
string | the container image available for building an application with this catalog |

### CamelLoader

**Appears on:**

-   [CamelCatalogSpec](#_camel_apache_org_v1_CamelCatalogSpec)
    

CamelLoader represents the configuration required to load a DSL.

 
| Field | Description |
| --- | --- |
| `MavenArtifact`  
**[MavenArtifact](#_camel_apache_org_v1_MavenArtifact)** | (Members of `MavenArtifact` are embedded into this type.)
the base Maven artifact required

 |
| `languages`  
\[\]string | a list of DSLs supported |
| `dependencies`  
**[\[\]MavenArtifact](#_camel_apache_org_v1_MavenArtifact)** | a list of additional dependencies required beside the base one |
| `metadata`  
map\[string\]string | the metadata of the loader |

### CamelProperty

**Appears on:**

-   [Capability](#_camel_apache_org_v1_Capability)
    

CamelProperty represents a Camel property that may end up in an application.properties file.

 
| Field | Description |
| --- | --- |
| `key`  
string | 
 |
| `value`  
string | 

 |

### CamelScheme

**Appears on:**

-   [CamelArtifact](#_camel_apache_org_v1_CamelArtifact)
    

CamelScheme represents the scheme used to identify a component in a URI (ie, timer in a timer:xyz endpoint URI).

 
| Field | Description |
| --- | --- |
| `id`  
string | the ID (ie, timer in a timer:xyz URI) |
| `passive`  
bool | is a passive scheme |
| `http`  
bool | is a HTTP based scheme |
| `consumer`  
**[CamelSchemeScope](#_camel_apache_org_v1_CamelSchemeScope)** | required scope for consumer |
| `producer`  
**[CamelSchemeScope](#_camel_apache_org_v1_CamelSchemeScope)** | required scope for producers |

### CamelSchemeScope

**Appears on:**

-   [CamelScheme](#_camel_apache_org_v1_CamelScheme)
    

CamelSchemeScope contains scoped information about a scheme.

 
| Field | Description |
| --- | --- |
| `dependencies`  
**[\[\]CamelArtifactDependency](#_camel_apache_org_v1_CamelArtifactDependency)** | list of dependencies needed for this scope |

### Capability

**Appears on:**

-   [RuntimeSpec](#_camel_apache_org_v1_RuntimeSpec)
    

Capability is a particular feature which requires a well known set of dependencies and other properties which are specified in the runtime catalog.

 
| Field | Description |
| --- | --- |
| `dependencies`  
**[\[\]MavenArtifact](#_camel_apache_org_v1_MavenArtifact)** | List of required Maven dependencies |
| `runtimeProperties`  
**[\[\]CamelProperty](#_camel_apache_org_v1_CamelProperty)** | Set of required Camel runtime properties |
| `buildTimeProperties`  
**[\[\]CamelProperty](#_camel_apache_org_v1_CamelProperty)** | Set of required Camel build time properties |
| `metadata`  
map\[string\]string | Set of generic metadata |

### Catalog

**Appears on:**

-   [IntegrationKitStatus](#_camel_apache_org_v1_IntegrationKitStatus)
    
-   [IntegrationStatus](#_camel_apache_org_v1_IntegrationStatus)
    

Catalog represents the Camel Catalog runtime specification.

 
| Field | Description |
| --- | --- |
| `version`  
string | 
 |
| `provider`  
**[RuntimeProvider](#_camel_apache_org_v1_RuntimeProvider)** | 

 |

### Configurable

Configurable --.

### ConfigurationSpec

**Appears on:**

-   [IntegrationKitSpec](#_camel_apache_org_v1_IntegrationKitSpec)
    
-   [IntegrationPlatformSpec](#_camel_apache_org_v1_IntegrationPlatformSpec)
    
-   [IntegrationSpec](#_camel_apache_org_v1_IntegrationSpec)
    
-   [IntegrationStatus](#_camel_apache_org_v1_IntegrationStatus)
    

ConfigurationSpec represents a generic configuration specification.

 
| Field | Description |
| --- | --- |
| `type`  
string | represents the type of configuration, ie: property, configmap, secret, …​ |
| `value`  
string | the value to assign to the configuration (syntax may vary depending on the `Type`) |

### Container

**Appears on:**

-   [PluginConfiguration](#_camel_apache_org_v1_PluginConfiguration)
    

Container — .

 
| Field | Description |
| --- | --- |
| `entrypoint`  
string | 
 |
| `args`  
**[Args](#_camel_apache_org_v1_Args)** | 

 |

### DataSpec

**Appears on:**

-   [SourceSpec](#_camel_apache_org_v1_SourceSpec)
    

DataSpec represents the way the source is materialized in the running `Pod`.

 
| Field | Description |
| --- | --- |
| `name`  
string | the name of the specification |
| `path`  
string | the path where the file is stored |
| `content`  
string | the source code (plain text) |
| `rawContent`  
\[\]byte | the source code (binary) |
| `contentRef`  
string | the confimap reference holding the source content |
| `contentKey`  
string | the confimap key holding the source content |
| `contentType`  
string | the content type (tipically text or binary) |
| `compression`  
bool | if the content is compressed (base64 encrypted) |

### DataTypeReference

**Appears on:**

-   [Endpoint](#_camel_apache_org_v1_Endpoint)
    

DataTypeReference references to the specification of a data type by its scheme and format name.

 
| Field | Description |
| --- | --- |
| `scheme`  
string | the data type component scheme |
| `format`  
string | the data type format name |

### DataTypeSpec

**Appears on:**

-   [DataTypesSpec](#_camel_apache_org_v1_DataTypesSpec)
    

DataTypeSpec represents the specification for a data type.

 
| Field | Description |
| --- | --- |
| `scheme`  
string | the data type component scheme |
| `format`  
string | the data type format name |
| `description`  
string | optional description |
| `mediaType`  
string | media type as expected for HTTP media types (ie, application/json) |
| `dependencies`  
\[\]string | the list of Camel or Maven dependencies required by the data type |
| `headers`  
**[map\[string\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.HeaderSpec](#_camel_apache_org_v1_HeaderSpec)** | one to many header specifications |
| `schema`  
**[JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)** | the expected schema for the data type |

### DataTypesSpec

**Appears on:**

-   [KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)
    

DataTypesSpec represents the specification for a set of data types.

 
| Field | Description |
| --- | --- |
| `default`  
string | the default data type for this Kamelet |
| `types`  
**[map\[string\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.DataTypeSpec](#_camel_apache_org_v1_DataTypeSpec)** | one to many data type specifications |
| `headers`  
**[map\[string\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.HeaderSpec](#_camel_apache_org_v1_HeaderSpec)** | one to many header specifications |

### Endpoint

**Appears on:**

-   [ErrorHandlerSink](#_camel_apache_org_v1_ErrorHandlerSink)
    
-   [PipeSpec](#_camel_apache_org_v1_PipeSpec)
    

Endpoint represents a source/sink external entity (could be any Kubernetes resource or Camel URI).

 
| Field | Description |
| --- | --- |
| `ref`  
**[Kubernetes core/v1.ObjectReference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectreference-v1-core)** | Ref can be used to declare a Kubernetes resource as source/sink endpoint |
| `uri`  
string | URI can be used to specify the (Camel) endpoint explicitly |
| `properties`  
**[EndpointProperties](#_camel_apache_org_v1_EndpointProperties)** | Properties are a key value representation of endpoint properties |
| `dataTypes`  
**[map\[github.com/apache/camel-k/v2/pkg/apis/camel/v1.TypeSlot\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.DataTypeReference](#_camel_apache_org_v1_DataTypeReference)** | DataTypes defines the data type of the data produced/consumed by the endpoint and references a given data type specification. |

### EndpointProperties

**Appears on:**

-   [Endpoint](#_camel_apache_org_v1_Endpoint)
    

EndpointProperties is a key/value struct represented as JSON raw to allow numeric/boolean values.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.) |

### EndpointType(`string` alias)

EndpointType represents the type (ie, source or sink).

### ErrorHandler

ErrorHandler is a generic interface that represent any type of error handler specification.

### ErrorHandlerLog

**Appears on:**

-   [ErrorHandlerSink](#_camel_apache_org_v1_ErrorHandlerSink)
    

ErrorHandlerLog represent a default (log) error handler type.

 
| Field | Description |
| --- | --- |
| `ErrorHandlerNone`  
**[ErrorHandlerNone](#_camel_apache_org_v1_ErrorHandlerNone)** | 
 |
| `parameters`  
**[ErrorHandlerParameters](#_camel_apache_org_v1_ErrorHandlerParameters)** | 

 |

### ErrorHandlerNone

**Appears on:**

-   [ErrorHandlerLog](#_camel_apache_org_v1_ErrorHandlerLog)
    

ErrorHandlerNone --.

 
| Field | Description |
| --- | --- |

### ErrorHandlerParameters

**Appears on:**

-   [ErrorHandlerLog](#_camel_apache_org_v1_ErrorHandlerLog)
    

ErrorHandlerParameters represent an unstructured object for error handler parameters.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.) |

### ErrorHandlerSink

ErrorHandlerSink represents a sink error handler type which behave like a dead letter channel.

 
| Field | Description |
| --- | --- |
| `ErrorHandlerLog`  
**[ErrorHandlerLog](#_camel_apache_org_v1_ErrorHandlerLog)** | 
 |
| `endpoint`  
**[Endpoint](#_camel_apache_org_v1_Endpoint)** | 

 |

### ErrorHandlerSpec

**Appears on:**

-   [PipeSpec](#_camel_apache_org_v1_PipeSpec)
    

ErrorHandlerSpec represents an unstructured object for an error handler.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.) |

### ErrorHandlerType(`string` alias)

ErrorHandlerType a type of error handler (ie, sink).

### EventTypeSpec

**Appears on:**

-   [KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)
    

EventTypeSpec represents a specification for an event type. Deprecated: In favor of using DataTypeSpec.

 
| Field | Description |
| --- | --- |
| `mediaType`  
string | media type as expected for HTTP media types (ie, application/json) |
| `schema`  
**[JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)** | the expected schema for the event |

### ExternalDocumentation

**Appears on:**

-   [JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)
    

ExternalDocumentation allows referencing an external resource for extended documentation.

 
| Field | Description |
| --- | --- |
| `description`  
string | 
 |
| `url`  
string | 

 |

### ExtraDirectories

**Appears on:**

-   [PluginConfiguration](#_camel_apache_org_v1_PluginConfiguration)
    

ExtraDirectories — .

 
| Field | Description |
| --- | --- |
| `paths>path`  
**[\[\]Path](#_camel_apache_org_v1_Path)** | 
 |
| `permissions>permission`  
**[\[\]Permission](#_camel_apache_org_v1_Permission)** | 

 |

### Failure

**Appears on:**

-   [BuildStatus](#_camel_apache_org_v1_BuildStatus)
    
-   [IntegrationKitStatus](#_camel_apache_org_v1_IntegrationKitStatus)
    

Failure represent a message specifying the reason and the time of an event failure.

 
| Field | Description |
| --- | --- |
| `reason`  
string | a short text specifying the reason |
| `time`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | the time when the failure has happened |
| `recovery`  
**[FailureRecovery](#_camel_apache_org_v1_FailureRecovery)** | the recovery attempted for this failure |

### FailureRecovery

**Appears on:**

-   [Failure](#_camel_apache_org_v1_Failure)
    

FailureRecovery defines the attempts to recover a failure.

 
| Field | Description |
| --- | --- |
| `attempt`  
int | attempt number |
| `attemptMax`  
int | maximum number of attempts |
| `attemptTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | **(Optional)**
time of the attempt execution

 |

### Filter

**Appears on:**

-   [PluginExtensionConfiguration](#_camel_apache_org_v1_PluginExtensionConfiguration)
    

Filter — .

 
| Field | Description |
| --- | --- |
| `glob`  
string | 
 |
| `toLayer`  
string | 

 |

### Flow

**Appears on:**

-   [IntegrationSpec](#_camel_apache_org_v1_IntegrationSpec)
    

Flow is an unstructured object representing a Camel Flow in YAML/JSON DSL.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.) |

### GitConfigSpec

**Appears on:**

-   [BuilderTask](#_camel_apache_org_v1_BuilderTask)
    
-   [IntegrationSpec](#_camel_apache_org_v1_IntegrationSpec)
    

GitConfigSpec defines the Git configuration of a project.

 
| Field | Description |
| --- | --- |
| `url`  
string | the URL of the project |
| `secret`  
string | the Kubernetes secret where token is stored |
| `branch`  
string | the git branch to check out |
| `tag`  
string | the git tag to check out |
| `commit`  
string | the git commit (full SHA) to check out |
| `path`  
string | the path you want to use for your project. If provided, it must be an existing directory on the Git repository. |

### HeaderSpec

**Appears on:**

-   [DataTypeSpec](#_camel_apache_org_v1_DataTypeSpec)
    
-   [DataTypesSpec](#_camel_apache_org_v1_DataTypesSpec)
    

HeaderSpec represents the specification for a header used in the Kamelet.

 
| Field | Description |
| --- | --- |
| `type`  
string | 
 |
| `title`  
string | 

 |
| `description`  
string | 

 |
| `required`  
bool | 

 |
| `default`  
string | 

 |

### HealthCheck

 
| Field | Description |
| --- | --- |
| `status`  
**[HealthCheckStatus](#_camel_apache_org_v1_HealthCheckStatus)** | 
 |
| `checks`  
**[\[\]HealthCheckResponse](#_camel_apache_org_v1_HealthCheckResponse)** | 

 |

### HealthCheckResponse

**Appears on:**

-   [HealthCheck](#_camel_apache_org_v1_HealthCheck)
    
-   [PodCondition](#_camel_apache_org_v1_PodCondition)
    

 
| Field | Description |
| --- | --- |
| `name`  
string | 
 |
| `status`  
**[HealthCheckStatus](#_camel_apache_org_v1_HealthCheckStatus)** | 

 |
| `data`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | 

 |

### HealthCheckStatus(`string` alias)

**Appears on:**

-   [HealthCheck](#_camel_apache_org_v1_HealthCheck)
    
-   [HealthCheckResponse](#_camel_apache_org_v1_HealthCheckResponse)
    

### IntegrationCondition

**Appears on:**

-   [IntegrationStatus](#_camel_apache_org_v1_IntegrationStatus)
    

IntegrationCondition describes the state of a resource at a certain point.

 
| Field | Description |
| --- | --- |
| `type`  
**[IntegrationConditionType](#_camel_apache_org_v1_IntegrationConditionType)** | Type of integration condition. |
| `status`  
**[Kubernetes core/v1.ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#conditionstatus-v1-core)** | Status of the condition, one of True, False, Unknown. |
| `lastUpdateTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | The last time this condition was updated. |
| `lastTransitionTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | Last time the condition transitioned from one status to another. |
| `firstTruthyTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | First time the condition status transitioned to True. |
| `reason`  
string | The reason for the condition’s last transition. |
| `message`  
string | A human-readable message indicating details about the transition. |
| `pods`  
**[\[\]PodCondition](#_camel_apache_org_v1_PodCondition)** | DeprecatedPods collect health and conditions information from the owned PODs
Deprecated: may be removed in future releases.

 |

### IntegrationConditionType(`string` alias)

**Appears on:**

-   [IntegrationCondition](#_camel_apache_org_v1_IntegrationCondition)
    

IntegrationConditionType --.

### IntegrationKitCondition

**Appears on:**

-   [IntegrationKitStatus](#_camel_apache_org_v1_IntegrationKitStatus)
    

IntegrationKitCondition describes the state of a resource at a certain point.

 
| Field | Description |
| --- | --- |
| `type`  
**[IntegrationKitConditionType](#_camel_apache_org_v1_IntegrationKitConditionType)** | Type of integration condition. |
| `status`  
**[Kubernetes core/v1.ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#conditionstatus-v1-core)** | Status of the condition, one of True, False, Unknown. |
| `lastUpdateTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | The last time this condition was updated. |
| `lastTransitionTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | Last time the condition transitioned from one status to another. |
| `reason`  
string | The reason for the condition’s last transition. |
| `message`  
string | A human-readable message indicating details about the transition. |

### IntegrationKitConditionType(`string` alias)

**Appears on:**

-   [IntegrationKitCondition](#_camel_apache_org_v1_IntegrationKitCondition)
    

IntegrationKitConditionType --.

### IntegrationKitPhase(`string` alias)

**Appears on:**

-   [IntegrationKitStatus](#_camel_apache_org_v1_IntegrationKitStatus)
    

IntegrationKitPhase --.

### IntegrationKitSpec

**Appears on:**

-   [IntegrationKit](#_camel_apache_org_v1_IntegrationKit)
    

IntegrationKitSpec defines a container image and additional configurations required to kick off an `Integration` with certain features.

 
| Field | Description |
| --- | --- |
| `image`  
string | the container image as identified in the container registry |
| `dependencies`  
\[\]string | a list of Camel dependencies used by this kit |
| `profile`  
**[TraitProfile](#_camel_apache_org_v1_TraitProfile)** | the profile which is expected by this kit
Deprecated: may be removed in future releases.

 |
| `traits`  
**[IntegrationKitTraits](#_camel_apache_org_v1_IntegrationKitTraits)** | traits that the kit will execute |
| `configuration`  
**[\[\]ConfigurationSpec](#_camel_apache_org_v1_ConfigurationSpec)** | Deprecated:

Use camel trait (camel.properties) to manage properties Use mount trait (mount.configs) to manage configs Use mount trait (mount.resources) to manage resources Use mount trait (mount.volumes) to manage volumes configuration used by the kit

 |
| `repositories`  
\[\]string | Maven repositories that can be used by the kit |
| `sources`  
**[\[\]SourceSpec](#_camel_apache_org_v1_SourceSpec)** | the sources to add at build time |
| `capabilities`  
\[\]string | features offered by the IntegrationKit |

### IntegrationKitStatus

**Appears on:**

-   [IntegrationKit](#_camel_apache_org_v1_IntegrationKit)
    

IntegrationKitStatus defines the observed state of IntegrationKit.

 
| Field | Description |
| --- | --- |
| `observedGeneration`  
int64 | ObservedGeneration is the most recent generation observed for this IntegrationKit. |
| `phase`  
**[IntegrationKitPhase](#_camel_apache_org_v1_IntegrationKitPhase)** | phase of the kit |
| `rootImage`  
string | root image used by the kit (the first image from which the incremental image has started, typically a JDK/JRE base image) |
| `baseImage`  
string | base image used by the kit (could be another IntegrationKit) |
| `image`  
string | actual image name of the kit |
| `digest`  
string | actual image digest of the kit |
| `artifacts`  
**[\[\]Artifact](#_camel_apache_org_v1_Artifact)** | list of artifacts used by the kit |
| `failure`  
**[Failure](#_camel_apache_org_v1_Failure)** | failure reason (if any) |
| `runtimeVersion`  
string | the runtime version for which this kit was configured |
| `runtimeProvider`  
**[RuntimeProvider](#_camel_apache_org_v1_RuntimeProvider)** | the runtime provider for which this kit was configured |
| `catalog`  
**[Catalog](#_camel_apache_org_v1_Catalog)** | the catalog used to build/operate the IntegrationKit. |
| `platform`  
string | the platform for which this kit was configured |
| `version`  
string | the Camel K operator version for which this kit was configured |
| `conditions`  
**[\[\]IntegrationKitCondition](#_camel_apache_org_v1_IntegrationKitCondition)** | a list of conditions which happened for the events related the kit |

### IntegrationKitTraits

**Appears on:**

-   [IntegrationKitSpec](#_camel_apache_org_v1_IntegrationKitSpec)
    

IntegrationKitTraits defines traits assigned to an `IntegrationKit`.

 
| Field | Description |
| --- | --- |
| `builder`  
**[BuilderTrait](#_camel_apache_org_v1_trait_BuilderTrait)** | The builder trait is internally used to determine the best strategy to build and configure IntegrationKits. |
| `camel`  
**[CamelTrait](#_camel_apache_org_v1_trait_CamelTrait)** | The Camel trait sets up Camel configuration. |
| `quarkus`  
**[QuarkusTrait](#_camel_apache_org_v1_trait_QuarkusTrait)** | The Quarkus trait configures the Quarkus runtime. It’s enabled by default. NOTE: Compiling to a native executable, requires at least 4GiB of memory, so the Pod running the native build must have enough memory available. |
| `registry`  
**[RegistryTrait](#_camel_apache_org_v1_trait_RegistryTrait)** | The Registry trait sets up Maven to use the Image registry as a Maven repository (support removed since version 2.5.0).
Deprecated: use jvm trait or read documentation.

 |
| `addons`  
**[map\[string\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.AddonTrait](#_camel_apache_org_v1_AddonTrait)** | Deprecated: no longer in use. |

### IntegrationPhase(`string` alias)

**Appears on:**

-   [IntegrationStatus](#_camel_apache_org_v1_IntegrationStatus)
    

IntegrationPhase --.

### IntegrationPlatformBuildPublishStrategy(`string` alias)

**Appears on:**

-   [IntegrationPlatformBuildSpec](#_camel_apache_org_v1_IntegrationPlatformBuildSpec)
    

IntegrationPlatformBuildPublishStrategy defines the strategy used to package and publish an Integration base image.

### IntegrationPlatformBuildSpec

**Appears on:**

-   [IntegrationPlatformSpec](#_camel_apache_org_v1_IntegrationPlatformSpec)
    

IntegrationPlatformBuildSpec contains platform related build information. This configuration can be used to tune the behavior of the Integration/IntegrationKit image builds. You can define the build strategy, the image registry to use and the Maven configuration to adopt.

 
| Field | Description |
| --- | --- |
| `buildConfiguration`  
**[BuildConfiguration](#_camel_apache_org_v1_BuildConfiguration)** | the configuration required to build an Integration container image |
| `publishStrategy`  
**[IntegrationPlatformBuildPublishStrategy](#_camel_apache_org_v1_IntegrationPlatformBuildPublishStrategy)** | the strategy to adopt for publishing an Integration container image |
| `runtimeVersion`  
string | the Camel K Runtime dependency version |
| `runtimeProvider`  
**[RuntimeProvider](#_camel_apache_org_v1_RuntimeProvider)** | the runtime used. Likely Camel Quarkus (we used to have main runtime which has been discontinued since version 1.5) |
| `runtimeCoreVersion`  
string | the Camel core version used by this IntegrationPlatform |
| `baseImage`  
string | a base image that can be used as base layer for all images. It can be useful if you want to provide some custom base image with further utility software |
| `registry`  
**[RegistrySpec](#_camel_apache_org_v1_RegistrySpec)** | the image registry used to push/pull Integration images |
| `buildCatalogToolTimeout`  
**[Kubernetes meta/v1.Duration](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#duration-v1-meta)** | the timeout (in seconds) to use when creating the build tools container image.
Deprecated: no longer in use

 |
| `timeout`  
**[Kubernetes meta/v1.Duration](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#duration-v1-meta)** | how much time to wait before time out the pipeline process |
| `maven`  
**[MavenSpec](#_camel_apache_org_v1_MavenSpec)** | Maven configuration used to build the Camel/Camel-Quarkus applications |
| `PublishStrategyOptions`  
map\[string\]string | Deprecated: no longer in use |
| `maxRunningBuilds`  
int32 | the maximum amount of parallel running pipelines started by this operator instance |

### IntegrationPlatformCluster(`string` alias)

**Appears on:**

-   [IntegrationPlatformSpec](#_camel_apache_org_v1_IntegrationPlatformSpec)
    

IntegrationPlatformCluster is the kind of orchestration cluster the platform is installed into.

Deprecated: no longer in use.

### IntegrationPlatformCondition

**Appears on:**

-   [IntegrationPlatformStatus](#_camel_apache_org_v1_IntegrationPlatformStatus)
    

IntegrationPlatformCondition describes the state of a resource at a certain point.

 
| Field | Description |
| --- | --- |
| `type`  
**[IntegrationPlatformConditionType](#_camel_apache_org_v1_IntegrationPlatformConditionType)** | Type of integration condition. |
| `status`  
**[Kubernetes core/v1.ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#conditionstatus-v1-core)** | Status of the condition, one of True, False, Unknown. |
| `lastUpdateTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | The last time this condition was updated. |
| `lastTransitionTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | Last time the condition transitioned from one status to another. |
| `reason`  
string | The reason for the condition’s last transition. |
| `message`  
string | A human-readable message indicating details about the transition. |

### IntegrationPlatformConditionType(`string` alias)

**Appears on:**

-   [IntegrationPlatformCondition](#_camel_apache_org_v1_IntegrationPlatformCondition)
    

IntegrationPlatformConditionType defines the type of condition.

### IntegrationPlatformKameletSpec

**Appears on:**

-   [IntegrationPlatformSpec](#_camel_apache_org_v1_IntegrationPlatformSpec)
    

IntegrationPlatformKameletSpec define the behavior for all the Kamelets controller by the IntegrationPlatform.

Deprecated: to be removed in future versions.

 
| Field | Description |
| --- | --- |
| `repositories`  
**[\[\]KameletRepositorySpec](#_camel_apache_org_v1_KameletRepositorySpec)** | remote repository used to retrieve Kamelet catalog |

### IntegrationPlatformPhase(`string` alias)

**Appears on:**

-   [IntegrationPlatformStatus](#_camel_apache_org_v1_IntegrationPlatformStatus)
    

IntegrationPlatformPhase is the phase of an IntegrationPlatform.

### IntegrationPlatformSpec

**Appears on:**

-   [IntegrationPlatform](#_camel_apache_org_v1_IntegrationPlatform)
    
-   [IntegrationPlatformStatus](#_camel_apache_org_v1_IntegrationPlatformStatus)
    

IntegrationPlatformSpec defines the desired state of IntegrationPlatform.

 
| Field | Description |
| --- | --- |
| `cluster`  
**[IntegrationPlatformCluster](#_camel_apache_org_v1_IntegrationPlatformCluster)** | what kind of cluster you’re running (ie, plain Kubernetes or OpenShift) |
| `profile`  
**[TraitProfile](#_camel_apache_org_v1_TraitProfile)** | the profile you wish to use. It will apply certain traits which are required by the specific profile chosen. It usually relates the Cluster with the optional definition of special profiles (ie, Knative)
Deprecated: may be removed in future releases.

 |
| `build`  
**[IntegrationPlatformBuildSpec](#_camel_apache_org_v1_IntegrationPlatformBuildSpec)** | specify how to build the Integration/IntegrationKits |
| `traits`  
**[Traits](#_camel_apache_org_v1_Traits)** | list of traits to be executed for all the Integration/IntegrationKits built from this IntegrationPlatform |
| `configuration`  
**[\[\]ConfigurationSpec](#_camel_apache_org_v1_ConfigurationSpec)** | Deprecated:

Use camel trait (camel.properties) to manage properties Use mount trait (mount.configs) to manage configs Use mount trait (mount.resources) to manage resources Use mount trait (mount.volumes) to manage volumes list of configuration properties to be attached to all the Integration/IntegrationKits built from this IntegrationPlatform

 |
| `kamelet`  
**[IntegrationPlatformKameletSpec](#_camel_apache_org_v1_IntegrationPlatformKameletSpec)** | configuration to be executed to all Kamelets controlled by this IntegrationPlatform |

### IntegrationPlatformStatus

**Appears on:**

-   [IntegrationPlatform](#_camel_apache_org_v1_IntegrationPlatform)
    

IntegrationPlatformStatus defines the observed state of IntegrationPlatform.

 
| Field | Description |
| --- | --- |
| `IntegrationPlatformSpec`  
**[IntegrationPlatformSpec](#_camel_apache_org_v1_IntegrationPlatformSpec)** | (Members of `IntegrationPlatformSpec` are embedded into this type.) |
| `observedGeneration`  
int64 | ObservedGeneration is the most recent generation observed for this IntegrationPlatform. |
| `phase`  
**[IntegrationPlatformPhase](#_camel_apache_org_v1_IntegrationPlatformPhase)** | defines in what phase the IntegrationPlatform is found |
| `conditions`  
**[\[\]IntegrationPlatformCondition](#_camel_apache_org_v1_IntegrationPlatformCondition)** | which are the conditions met (particularly useful when in ERROR phase) |
| `version`  
string | the Camel K operator version controlling this IntegrationPlatform |
| `info`  
map\[string\]string | generic information related to the build of Camel K operator software |

### IntegrationProfileBuildSpec

**Appears on:**

-   [IntegrationProfileSpec](#_camel_apache_org_v1_IntegrationProfileSpec)
    

IntegrationProfileBuildSpec contains profile related build information. This configuration can be used to tune the behavior of the Integration/IntegrationKit image builds.

 
| Field | Description |
| --- | --- |
| `runtimeVersion`  
string | the Camel K Runtime dependency version |
| `runtimeProvider`  
**[RuntimeProvider](#_camel_apache_org_v1_RuntimeProvider)** | the runtime used. Likely Camel Quarkus (we used to have main runtime which has been discontinued since version 1.5) |
| `baseImage`  
string | a base image that can be used as base layer for all images. It can be useful if you want to provide some custom base image with further utility software |
| `registry`  
**[RegistrySpec](#_camel_apache_org_v1_RegistrySpec)** | the image registry used to push/pull Integration images |
| `timeout`  
**[Kubernetes meta/v1.Duration](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#duration-v1-meta)** | how much time to wait before time out the pipeline process |
| `maven`  
**[MavenSpec](#_camel_apache_org_v1_MavenSpec)** | Maven configuration used to build the Camel/Camel-Quarkus applications |

### IntegrationProfileCondition

**Appears on:**

-   [IntegrationProfileStatus](#_camel_apache_org_v1_IntegrationProfileStatus)
    

IntegrationProfileCondition describes the state of a resource at a certain point.

 
| Field | Description |
| --- | --- |
| `type`  
**[IntegrationProfileConditionType](#_camel_apache_org_v1_IntegrationProfileConditionType)** | Type of integration condition. |
| `status`  
**[Kubernetes core/v1.ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#conditionstatus-v1-core)** | Status of the condition, one of True, False, Unknown. |
| `lastUpdateTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | The last time this condition was updated. |
| `lastTransitionTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | Last time the condition transitioned from one status to another. |
| `reason`  
string | The reason for the condition’s last transition. |
| `message`  
string | A human-readable message indicating details about the transition. |

### IntegrationProfileConditionType(`string` alias)

**Appears on:**

-   [IntegrationProfileCondition](#_camel_apache_org_v1_IntegrationProfileCondition)
    

IntegrationProfileConditionType defines the type of condition.

### IntegrationProfileKameletSpec

**Appears on:**

-   [IntegrationProfileSpec](#_camel_apache_org_v1_IntegrationProfileSpec)
    

IntegrationProfileKameletSpec define the behavior for all the Kamelets controller by the IntegrationProfile.

Deprecated: to be removed in future versions.

 
| Field | Description |
| --- | --- |
| `repositories`  
**[\[\]KameletRepositorySpec](#_camel_apache_org_v1_KameletRepositorySpec)** | remote repository used to retrieve Kamelet catalog |

### IntegrationProfilePhase(`string` alias)

**Appears on:**

-   [IntegrationProfileStatus](#_camel_apache_org_v1_IntegrationProfileStatus)
    

IntegrationProfilePhase is the phase of an IntegrationProfile.

### IntegrationProfileSpec

**Appears on:**

-   [IntegrationProfile](#_camel_apache_org_v1_IntegrationProfile)
    
-   [IntegrationProfileStatus](#_camel_apache_org_v1_IntegrationProfileStatus)
    

IntegrationProfileSpec applies user defined settings to the IntegrationProfile.

 
| Field | Description |
| --- | --- |
| `build`  
**[IntegrationProfileBuildSpec](#_camel_apache_org_v1_IntegrationProfileBuildSpec)** | specify how to build the Integration/IntegrationKits |
| `traits`  
**[Traits](#_camel_apache_org_v1_Traits)** | list of traits to be executed for all the Integration/IntegrationKits built from this IntegrationProfile |
| `dependencies`  
\[\]string | a list of dependencies needed by the application |
| `kamelet`  
**[IntegrationProfileKameletSpec](#_camel_apache_org_v1_IntegrationProfileKameletSpec)** | configuration to be executed to all Kamelets controlled by this IntegrationProfile
Deprecated: to be removed in future versions.

 |

### IntegrationProfileStatus

**Appears on:**

-   [IntegrationProfile](#_camel_apache_org_v1_IntegrationProfile)
    

IntegrationProfileStatus defines the observed state of IntegrationProfile.

 
| Field | Description |
| --- | --- |
| `IntegrationProfileSpec`  
**[IntegrationProfileSpec](#_camel_apache_org_v1_IntegrationProfileSpec)** | (Members of `IntegrationProfileSpec` are embedded into this type.) |
| `observedGeneration`  
int64 | ObservedGeneration is the most recent generation observed for this IntegrationProfile. |
| `phase`  
**[IntegrationProfilePhase](#_camel_apache_org_v1_IntegrationProfilePhase)** | defines in what phase the IntegrationProfile is found |
| `conditions`  
**[\[\]IntegrationProfileCondition](#_camel_apache_org_v1_IntegrationProfileCondition)** | which are the conditions met (particularly useful when in ERROR phase) |

### IntegrationSpec

**Appears on:**

-   [Integration](#_camel_apache_org_v1_Integration)
    
-   [PipeSpec](#_camel_apache_org_v1_PipeSpec)
    

IntegrationSpec specifies the configuration of an Integration. The Integration will be watched by the operator which will be in charge to run the related application, according to the configuration specified.

 
| Field | Description |
| --- | --- |
| `replicas`  
int32 | the number of `Pods` needed for the running Integration |
| `sources`  
**[\[\]SourceSpec](#_camel_apache_org_v1_SourceSpec)** | the sources which contain the Camel routes to run |
| `git`  
**[GitConfigSpec](#_camel_apache_org_v1_GitConfigSpec)** | the configuration of the project to build on Git |
| `flows`  
**[\[\]Flow](#_camel_apache_org_v1_Flow)** | a source in YAML DSL language which contain the routes to run |
| `integrationKit`  
**[Kubernetes core/v1.ObjectReference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectreference-v1-core)** | the reference of the `IntegrationKit` which is used for this Integration |
| `dependencies`  
\[\]string | the list of Camel or Maven dependencies required by the Integration |
| `profile`  
**[TraitProfile](#_camel_apache_org_v1_TraitProfile)** | the profile needed to run this Integration
Deprecated: may be removed in future releases.

 |
| `traits`  
**[Traits](#_camel_apache_org_v1_Traits)** | the traits needed to run this Integration |
| `template`  
**[PodSpecTemplate](#_camel_apache_org_v1_PodSpecTemplate)** | Pod template customization. |
| `configuration`  
**[\[\]ConfigurationSpec](#_camel_apache_org_v1_ConfigurationSpec)** | Deprecated:

Use camel trait (camel.properties) to manage properties Use mount trait (mount.configs) to manage configs Use mount trait (mount.resources) to manage resources Use mount trait (mount.volumes) to manage volumes

 |
| `repositories`  
\[\]string | additional Maven repositories to be used |
| `serviceAccountName`  
string | custom SA to use for the Integration |

### IntegrationStatus

**Appears on:**

-   [Integration](#_camel_apache_org_v1_Integration)
    

IntegrationStatus defines the observed state of Integration.

 
| Field | Description |
| --- | --- |
| `observedGeneration`  
int64 | ObservedGeneration is the most recent generation observed for this Integration. |
| `phase`  
**[IntegrationPhase](#_camel_apache_org_v1_IntegrationPhase)** | the actual phase |
| `digest`  
string | the digest calculated for this Integration |
| `image`  
string | the container image used |
| `jar`  
string | the Java jar dependency to execute (if available) |
| `dependencies`  
\[\]string | a list of dependencies needed by the application |
| `profile`  
**[TraitProfile](#_camel_apache_org_v1_TraitProfile)** | the profile needed to run this Integration
Deprecated: may be removed in future releases.

 |
| `traits`  
**[Traits](#_camel_apache_org_v1_Traits)** | the traits executed for the Integration |
| `integrationKit`  
**[Kubernetes core/v1.ObjectReference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#objectreference-v1-core)** | the reference of the `IntegrationKit` which is used for this Integration |
| `platform`  
string | The IntegrationPlatform watching this Integration |
| `generatedSources`  
**[\[\]SourceSpec](#_camel_apache_org_v1_SourceSpec)** | a list of sources generated for this Integration |
| `runtimeVersion`  
string | the runtime version targeted for this Integration |
| `runtimeProvider`  
**[RuntimeProvider](#_camel_apache_org_v1_RuntimeProvider)** | the runtime provider targeted for this Integration |
| `catalog`  
**[Catalog](#_camel_apache_org_v1_Catalog)** | the catalog used to build/operate the Integration. |
| `configuration`  
**[\[\]ConfigurationSpec](#_camel_apache_org_v1_ConfigurationSpec)** | a list of configuration specification.

Deprecated: use properties instead.

 |
| `conditions`  
**[\[\]IntegrationCondition](#_camel_apache_org_v1_IntegrationCondition)** | a list of events happened for the Integration |
| `version`  
string | the operator version |
| `replicas`  
int32 | the number of replicas |
| `selector`  
string | label selector |
| `capabilities`  
\[\]string | features offered by the Integration |
| `lastInitTimestamp`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | the timestamp representing the last time when this integration was initialized. |
| `lastDeploymentTimestamp`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | the timestamp representing the last time when this integration was deployed. |
| `lastBuildTimestamp`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | the timestamp representing the last time when this integration was built. |

### JSON

**Appears on:**

-   [JSONSchemaProp](#_camel_apache_org_v1_JSONSchemaProp)
    
-   [JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)
    

JSON represents any valid JSON value. These types are supported: bool, int64, float64, string, \[\]interface{}, map\[string\]interface{} and nil.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.) |

### JSONSchemaProp

**Appears on:**

-   [JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)
    

 
| Field | Description |
| --- | --- |
| `id`  
string | 
 |
| `deprecated`  
bool | 

 |
| `description`  
string | 

 |
| `type`  
string | 

 |
| `format`  
string | 

format is an OpenAPI v3 format string. Unknown formats are ignored. The following formats are validated:

-   bsonobjectid: a bson object ID, i.e. a 24 characters hex string
    
-   uri: an URI as parsed by Golang net/url.ParseRequestURI
    
-   email: an email address as parsed by Golang net/mail.ParseAddress
    
-   hostname: a valid representation for an Internet host name, as defined by RFC 1034, section 3.1 \[RFC1034\].
    
-   ipv4: an IPv4 IP as parsed by Golang net.ParseIP
    
-   ipv6: an IPv6 IP as parsed by Golang net.ParseIP
    
-   cidr: a CIDR as parsed by Golang net.ParseCIDR
    
-   mac: a MAC address as parsed by Golang net.ParseMAC
    
-   uuid: an UUID that allows uppercase defined by the regex (?i)^\[0-9a-f\]{8}-?\[0-9a-f\]{4}-?\[0-9a-f\]{4}-?\[0-9a-f\]{4}-?\[0-9a-f\]{12}$
    
-   uuid3: an UUID3 that allows uppercase defined by the regex (?i)^\[0-9a-f\]{8}-?\[0-9a-f\]{4}-?3\[0-9a-f\]{3}-?\[0-9a-f\]{4}-?\[0-9a-f\]{12}$
    
-   uuid4: an UUID4 that allows uppercase defined by the regex (?i)^\[0-9a-f\]{8}-?\[0-9a-f\]{4}-?4\[0-9a-f\]{3}-?\[89ab\]\[0-9a-f\]{3}-?\[0-9a-f\]{12}$
    
-   uuid5: an UUID5 that allows uppercase defined by the regex (?i)^\[0-9a-f\]{8}-?\[0-9a-f\]{4}-?5\[0-9a-f\]{3}-?\[89ab\]\[0-9a-f\]{3}-?\[0-9a-f\]{12}$
    
-   isbn: an ISBN10 or ISBN13 number string like "0321751043" or "978-0321751041"
    
-   isbn10: an ISBN10 number string like "0321751043"
    
-   isbn13: an ISBN13 number string like "978-0321751041"
    
-   creditcard: a credit card number defined by the regex ^(?:4\[0-9\]{12}(?:\[0-9\]{3})?|5\[1-5\]\[0-9\]{14}|6(?:011|5\[0-9\]\[0-9\])\[0-9\]{12}|3\[47\]\[0-9\]{13}|3(?:0\[0-5\]|\[68\]\[0-9\])\[0-9\]{11}|(?:2131|1800|35\\\\d{3})\\\\d{11})$ with any non digit characters mixed in
    
-   ssn: a U.S. social security number following the regex ^\\\\d{3}\[- \]?\\\\d{2}\[- \]?\\\\d{4}$
    
-   hexcolor: an hexadecimal color code like "#FFFFFF" following the regex ^#?(\[0-9a-fA-F\]{3}|\[0-9a-fA-F\]{6})$
    
-   rgbcolor: an RGB color code like rgb like "rgb(255,255,255)"
    
-   byte: base64 encoded binary data
    
-   password: any kind of string
    
-   date: a date string like "2006-01-02" as defined by full-date in RFC3339
    
-   duration: a duration string like "22 ns" as parsed by Golang time.ParseDuration or compatible with Scala duration format
    
-   datetime: a date time string like "2014-12-15T19:30:20.000Z" as defined by date-time in RFC3339.
    





 |
| `title`  
string | 

 |
| `default`  
**[JSON](#_camel_apache_org_v1_JSON)** | default is a default value for undefined object fields. |
| `maximum`  
encoding/json.Number | 

 |
| `exclusiveMaximum`  
bool | 

 |
| `minimum`  
encoding/json.Number | 

 |
| `exclusiveMinimum`  
bool | 

 |
| `maxLength`  
int64 | 

 |
| `minLength`  
int64 | 

 |
| `pattern`  
string | 

 |
| `maxItems`  
int64 | 

 |
| `minItems`  
int64 | 

 |
| `uniqueItems`  
bool | 

 |
| `maxProperties`  
int64 | 

 |
| `minProperties`  
int64 | 

 |
| `multipleOf`  
encoding/json.Number | 

 |
| `enum`  
**[\[\]JSON](#_camel_apache_org_v1_JSON)** | 

 |
| `example`  
**[JSON](#_camel_apache_org_v1_JSON)** | 

 |
| `nullable`  
bool | 

 |
| `x-descriptors`  
\[\]string | XDescriptors is a list of extended properties that trigger a custom behavior in external systems |

### JSONSchemaProps

**Appears on:**

-   [DataTypeSpec](#_camel_apache_org_v1_DataTypeSpec)
    
-   [EventTypeSpec](#_camel_apache_org_v1_EventTypeSpec)
    
-   [KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)
    

JSONSchemaProps is a JSON-Schema following Specification Draft 4 ([http://json-schema.org/](http://json-schema.org/)).

 
| Field | Description |
| --- | --- |
| `id`  
string | 
 |
| `description`  
string | 

 |
| `title`  
string | 

 |
| `properties`  
**[map\[string\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.JSONSchemaProp](#_camel_apache_org_v1_JSONSchemaProp)** | 

 |
| `required`  
\[\]string | 

 |
| `example`  
**[JSON](#_camel_apache_org_v1_JSON)** | 

 |
| `externalDocs`  
**[ExternalDocumentation](#_camel_apache_org_v1_ExternalDocumentation)** | 

 |
| `$schema`  
**[JSONSchemaURL](#_camel_apache_org_v1_JSONSchemaURL)** | 

 |
| `type`  
string | 

 |

### JSONSchemaURL(`string` alias)

**Appears on:**

-   [JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)
    

JSONSchemaURL represents a schema url.

### JibTask

**Appears on:**

-   [Task](#_camel_apache_org_v1_Task)
    

JibTask is used to configure Jib.

 
| Field | Description |
| --- | --- |
| `BaseTask`  
**[BaseTask](#_camel_apache_org_v1_BaseTask)** | (Members of `BaseTask` are embedded into this type.) |
| `PublishTask`  
**[PublishTask](#_camel_apache_org_v1_PublishTask)** | (Members of `PublishTask` are embedded into this type.) |

### KameletCondition

**Appears on:**

-   [KameletStatus](#_camel_apache_org_v1_KameletStatus)
    

KameletCondition describes the state of a resource at a certain point.

 
| Field | Description |
| --- | --- |
| `type`  
**[KameletConditionType](#_camel_apache_org_v1_KameletConditionType)** | Type of kamelet condition. |
| `status`  
**[Kubernetes core/v1.ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#conditionstatus-v1-core)** | Status of the condition, one of True, False, Unknown. |
| `lastUpdateTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | The last time this condition was updated. |
| `lastTransitionTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | Last time the condition transitioned from one status to another. |
| `reason`  
string | The reason for the condition’s last transition. |
| `message`  
string | A human-readable message indicating details about the transition. |

### KameletConditionType(`string` alias)

**Appears on:**

-   [KameletCondition](#_camel_apache_org_v1_KameletCondition)
    

KameletConditionType --.

### KameletPhase(`string` alias)

**Appears on:**

-   [KameletStatus](#_camel_apache_org_v1_KameletStatus)
    

KameletPhase --.

### KameletProperty

**Appears on:**

-   [KameletStatus](#_camel_apache_org_v1_KameletStatus)
    

KameletProperty specify the behavior of a property in a Kamelet.

 
| Field | Description |
| --- | --- |
| `name`  
string | the name of the property |
| `default`  
string | the default value of the property (if any) |

### KameletRepositorySpec

**Appears on:**

-   [IntegrationPlatformKameletSpec](#_camel_apache_org_v1_IntegrationPlatformKameletSpec)
    
-   [IntegrationProfileKameletSpec](#_camel_apache_org_v1_IntegrationProfileKameletSpec)
    

KameletRepositorySpec defines the location of the Kamelet catalog to use.

 
| Field | Description |
| --- | --- |
| `uri`  
string | the remote repository in the format github:ORG/REPO/PATH\_TO\_KAMELETS\_FOLDER |

### KameletSpec

**Appears on:**

-   [Kamelet](#_camel_apache_org_v1_Kamelet)
    

KameletSpec specifies the configuration required to execute a Kamelet.

 
| Field | Description |
| --- | --- |
| `KameletSpecBase`  
**[KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)** | (Members of `KameletSpecBase` are embedded into this type.) |
| `versions`  
**[map\[string\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)** | the optional versions available for this Kamelet. This field may not be taken in account by Camel core and is meant to support any user defined versioning model on cluster only. If the user wants to use any given version, she must materialize a file with the given version spec as the `main` Kamelet spec on the runtime. |

### KameletSpecBase

**Appears on:**

-   [KameletSpec](#_camel_apache_org_v1_KameletSpec)
    

KameletSpecBase specifies the base configuration of a Kamelet.

 
| Field | Description |
| --- | --- |
| `definition`  
**[JSONSchemaProps](#_camel_apache_org_v1_JSONSchemaProps)** | defines the formal configuration of the Kamelet |
| `sources`  
**[\[\]SourceSpec](#_camel_apache_org_v1_SourceSpec)** | sources in any Camel DSL supported |
| `template`  
**[Template](#_camel_apache_org_v1_Template)** | the main source in YAML DSL |
| `types`  
**[map\[github.com/apache/camel-k/v2/pkg/apis/camel/v1.TypeSlot\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.EventTypeSpec](#_camel_apache_org_v1_EventTypeSpec)** | data specification types for the events consumed/produced by the Kamelet Deprecated: In favor of using DataTypes |
| `dataTypes`  
**[map\[github.com/apache/camel-k/v2/pkg/apis/camel/v1.TypeSlot\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.DataTypesSpec](#_camel_apache_org_v1_DataTypesSpec)** | data specification types for the events consumed/produced by the Kamelet |
| `dependencies`  
\[\]string | Camel dependencies needed by the Kamelet |

### KameletStatus

**Appears on:**

-   [Kamelet](#_camel_apache_org_v1_Kamelet)
    

KameletStatus defines the observed state of Kamelet.

 
| Field | Description |
| --- | --- |
| `observedGeneration`  
int64 | ObservedGeneration is the most recent generation observed for this Kamelet. |
| `phase`  
**[KameletPhase](#_camel_apache_org_v1_KameletPhase)** | Phase —  |
| `conditions`  
**[\[\]KameletCondition](#_camel_apache_org_v1_KameletCondition)** | Conditions —  |
| `properties`  
**[\[\]KameletProperty](#_camel_apache_org_v1_KameletProperty)** | Properties —  |

### KanikoTask

**Appears on:**

-   [Task](#_camel_apache_org_v1_Task)
    

KanikoTask is used to configure Kaniko.

Deprecated: no longer in use.

 
| Field | Description |
| --- | --- |
| `BaseTask`  
**[BaseTask](#_camel_apache_org_v1_BaseTask)** | (Members of `BaseTask` are embedded into this type.) |
| `PublishTask`  
**[PublishTask](#_camel_apache_org_v1_PublishTask)** | (Members of `PublishTask` are embedded into this type.) |
| `verbose`  
bool | log more information |
| `cache`  
**[KanikoTaskCache](#_camel_apache_org_v1_KanikoTaskCache)** | use a cache |
| `executorImage`  
string | docker image to use |

### KanikoTaskCache

**Appears on:**

-   [KanikoTask](#_camel_apache_org_v1_KanikoTask)
    

KanikoTaskCache is used to configure Kaniko cache.

Deprecated: no longer in use.

 
| Field | Description |
| --- | --- |
| `enabled`  
bool | true if a cache is enabled |
| `persistentVolumeClaim`  
string | the PVC used to store the cache |

### Language(`string` alias)

**Appears on:**

-   [SourceSpec](#_camel_apache_org_v1_SourceSpec)
    

Language represents a supported language (Camel DSL).

### MavenArtifact

**Appears on:**

-   [CamelArtifactDependency](#_camel_apache_org_v1_CamelArtifactDependency)
    
-   [CamelLoader](#_camel_apache_org_v1_CamelLoader)
    
-   [Capability](#_camel_apache_org_v1_Capability)
    
-   [MavenSpec](#_camel_apache_org_v1_MavenSpec)
    
-   [RuntimeSpec](#_camel_apache_org_v1_RuntimeSpec)
    

MavenArtifact defines a GAV (Group:Artifact:Type:Version:Classifier) Maven artifact.

 
| Field | Description |
| --- | --- |
| `groupId`  
string | Maven Group |
| `artifactId`  
string | Maven Artifact |
| `type`  
string | Maven Type |
| `version`  
string | Maven Version |
| `classifier`  
string | Maven Classifier |

### MavenBuildSpec

**Appears on:**

-   [BuilderTask](#_camel_apache_org_v1_BuilderTask)
    

MavenBuildSpec defines the Maven configuration plus additional repositories to use.

 
| Field | Description |
| --- | --- |
| `MavenSpec`  
**[MavenSpec](#_camel_apache_org_v1_MavenSpec)** | (Members of `MavenSpec` are embedded into this type.)
base Maven specification

 |
| `repositories`  
**[\[\]Repository](#_camel_apache_org_v1_Repository)** | additional repositories |
| `servers`  
**[\[\]Server](#_camel_apache_org_v1_Server)** | Servers (auth)

Deprecated: no longer in use.

 |

### MavenSpec

**Appears on:**

-   [IntegrationPlatformBuildSpec](#_camel_apache_org_v1_IntegrationPlatformBuildSpec)
    
-   [IntegrationProfileBuildSpec](#_camel_apache_org_v1_IntegrationProfileBuildSpec)
    
-   [MavenBuildSpec](#_camel_apache_org_v1_MavenBuildSpec)
    

MavenSpec --.

 
| Field | Description |
| --- | --- |
| `localRepository`  
string | The path of the local Maven repository. |
| `properties`  
map\[string\]string | The Maven properties. |
| `profiles`  
**[\[\]ValueSource](#_camel_apache_org_v1_ValueSource)** | Deprecated: no longer in use. |
| `settings`  
**[ValueSource](#_camel_apache_org_v1_ValueSource)** | A reference to the ConfigMap or Secret key that contains the Maven settings. |
| `settingsSecurity`  
**[ValueSource](#_camel_apache_org_v1_ValueSource)** | A reference to the ConfigMap or Secret key that contains the security of the Maven settings. |
| `caSecrets`  
**[\[\]Kubernetes core/v1.SecretKeySelector](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#secretkeyselector-v1-core)** | The Secrets name and key, containing the CA certificate(s) used to connect to remote Maven repositories. It can contain X.509 certificates, and PKCS#7 formatted certificate chains. A JKS formatted keystore is automatically created to store the CA certificate(s), and configured to be used as a trusted certificate(s) by the Maven commands. Note that the root CA certificates are also imported into the created keystore. |
| `extension`  
**[\[\]MavenArtifact](#_camel_apache_org_v1_MavenArtifact)** | Deprecated: no longer in use. |
| `cliOptions`  
\[\]string | The CLI options that are appended to the list of arguments for Maven commands, e.g., `-V,--no-transfer-progress,-Dstyle.color=never`. See [https://maven.apache.org/ref/3.9.14/maven-embedder/cli.html](https://maven.apache.org/ref/3.9.14/maven-embedder/cli.md). |

### Path

**Appears on:**

-   [ExtraDirectories](#_camel_apache_org_v1_ExtraDirectories)
    

Path — .

 
| Field | Description |
| --- | --- |
| `from`  
string | 
 |
| `into`  
string | 

 |
| `excludes>exclude`  
\[\]string | 

 |

### Permission

**Appears on:**

-   [ExtraDirectories](#_camel_apache_org_v1_ExtraDirectories)
    

Permission — .

 
| Field | Description |
| --- | --- |
| `file`  
string | 
 |
| `mode`  
string | 

 |

### PipeCondition

**Appears on:**

-   [PipeStatus](#_camel_apache_org_v1_PipeStatus)
    

PipeCondition describes the state of a resource at a certain point.

 
| Field | Description |
| --- | --- |
| `type`  
**[PipeConditionType](#_camel_apache_org_v1_PipeConditionType)** | Type of pipe condition. |
| `status`  
**[Kubernetes core/v1.ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#conditionstatus-v1-core)** | Status of the condition, one of True, False, Unknown. |
| `lastUpdateTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | The last time this condition was updated. |
| `lastTransitionTime`  
**[Kubernetes meta/v1.Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#time-v1-meta)** | Last time the condition transitioned from one status to another. |
| `reason`  
string | The reason for the condition’s last transition. |
| `message`  
string | A human readable message indicating details about the transition. |
| `pods`  
**[\[\]PodCondition](#_camel_apache_org_v1_PodCondition)** | DeprecatedPods collect health and conditions information from the owned PODs
Deprecated: may be removed in future releases.

 |

### PipeConditionType(`string` alias)

**Appears on:**

-   [PipeCondition](#_camel_apache_org_v1_PipeCondition)
    

PipeConditionType --.

### PipePhase(`string` alias)

**Appears on:**

-   [PipeStatus](#_camel_apache_org_v1_PipeStatus)
    

PipePhase --.

### PipeSpec

**Appears on:**

-   [Pipe](#_camel_apache_org_v1_Pipe)
    

PipeSpec defines the binding between a source and a sink. It can include custom parameters and additional intermediate steps and error handling.

 
| Field | Description |
| --- | --- |
| `integration`  
**[IntegrationSpec](#_camel_apache_org_v1_IntegrationSpec)** | Integration is an optional integration used to specify custom parameters Deprecated don’t use this. Use trait annotations if you need to change any cluster configuration. |
| `source`  
**[Endpoint](#_camel_apache_org_v1_Endpoint)** | Source is the starting point of the integration defined by this Pipe |
| `sink`  
**[Endpoint](#_camel_apache_org_v1_Endpoint)** | Sink is the destination of the integration defined by this Pipe |
| `errorHandler`  
**[ErrorHandlerSpec](#_camel_apache_org_v1_ErrorHandlerSpec)** | ErrorHandler is an optional handler called upon an error occurring in the integration |
| `traits`  
**[Traits](#_camel_apache_org_v1_Traits)** | the traits needed to customize the depending Integration |
| `steps`  
**[\[\]Endpoint](#_camel_apache_org_v1_Endpoint)** | Steps contains an optional list of intermediate steps that are executed between the Source and the Sink |
| `replicas`  
int32 | Replicas is the number of desired replicas for the Pipe |
| `serviceAccountName`  
string | Custom SA to use for the Pipe |
| `dependencies`  
\[\]string | the list of Camel or Maven dependencies required by the Pipe |

### PipeStatus

**Appears on:**

-   [Pipe](#_camel_apache_org_v1_Pipe)
    

PipeStatus specify the status of a Pipe.

 
| Field | Description |
| --- | --- |
| `observedGeneration`  
int64 | ObservedGeneration is the most recent generation observed for this Pipe. |
| `phase`  
**[PipePhase](#_camel_apache_org_v1_PipePhase)** | Phase —  |
| `conditions`  
**[\[\]PipeCondition](#_camel_apache_org_v1_PipeCondition)** | Conditions —  |
| `replicas`  
int32 | Replicas is the number of actual replicas of the pipe |
| `selector`  
string | Selector allows to identify pods belonging to the pipe |

### PluginConfiguration

PluginConfiguration see [Maven settings](https://maven.apache.org/settings.md).

 
| Field | Description |
| --- | --- |
| `container`  
**[Container](#_camel_apache_org_v1_Container)** | 
 |
| `allowInsecureRegistries`  
string | 

 |
| `extraDirectories`  
**[ExtraDirectories](#_camel_apache_org_v1_ExtraDirectories)** | 

 |
| `pluginExtensions`  
**[PluginExtensions](#_camel_apache_org_v1_PluginExtensions)** | 

 |

### PluginExtension

**Appears on:**

-   [PluginExtensions](#_camel_apache_org_v1_PluginExtensions)
    

PluginExtension — .

 
| Field | Description |
| --- | --- |
| `implementation`  
string | 
 |
| `configuration`  
**[PluginExtensionConfiguration](#_camel_apache_org_v1_PluginExtensionConfiguration)** | 

 |

### PluginExtensionConfiguration

**Appears on:**

-   [PluginExtension](#_camel_apache_org_v1_PluginExtension)
    

PluginExtensionConfiguration — .

 
| Field | Description |
| --- | --- |
| `filters>Filter`  
**[\[\]Filter](#_camel_apache_org_v1_Filter)** | 
 |
| `_implementation`  
string | 

 |

### PluginExtensions

**Appears on:**

-   [PluginConfiguration](#_camel_apache_org_v1_PluginConfiguration)
    

PluginExtensions — .

 
| Field | Description |
| --- | --- |
| `pluginExtension`  
**[PluginExtension](#_camel_apache_org_v1_PluginExtension)** | 
 |

### PluginProperties(`map[string]github.com/apache/camel-k/v2/pkg/apis/camel/v1.StringOrProperties` alias)

PluginProperties — .

### PodCondition

**Appears on:**

-   [IntegrationCondition](#_camel_apache_org_v1_IntegrationCondition)
    
-   [PipeCondition](#_camel_apache_org_v1_PipeCondition)
    

Deprecated: may be removed in future releases.

 
| Field | Description |
| --- | --- |
| `name`  
string | 
 |
| `condition`  
**[Kubernetes core/v1.PodCondition](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#podcondition-v1-core)** | 

 |
| `health`  
**[\[\]HealthCheckResponse](#_camel_apache_org_v1_HealthCheckResponse)** | 

 |

### PodSpec

**Appears on:**

-   [PodSpecTemplate](#_camel_apache_org_v1_PodSpecTemplate)
    

PodSpec defines a group of Kubernetes resources.

 
| Field | Description |
| --- | --- |
| `automountServiceAccountToken`  
bool | AutomountServiceAccountToken |
| `enableServiceLinks`  
bool | EnableServiceLinks indicates whether information about services should be injected into the Pod’s environment variables, matching the syntax of Docker links. Defaults to true. |
| `volumes`  
**[\[\]Kubernetes core/v1.Volume](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#volume-v1-core)** | Volumes |
| `initContainers`  
**[\[\]Kubernetes core/v1.Container](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#container-v1-core)** | InitContainers |
| `containers`  
**[\[\]Kubernetes core/v1.Container](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#container-v1-core)** | Containers |
| `ephemeralContainers`  
**[\[\]Kubernetes core/v1.EphemeralContainer](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#ephemeralcontainer-v1-core)** | EphemeralContainers |
| `restartPolicy`  
**[Kubernetes core/v1.RestartPolicy](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#restartpolicy-v1-core)** | RestartPolicy |
| `terminationGracePeriodSeconds`  
int64 | TerminationGracePeriodSeconds |
| `activeDeadlineSeconds`  
int64 | ActiveDeadlineSeconds |
| `dnsPolicy`  
**[Kubernetes core/v1.DNSPolicy](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#dnspolicy-v1-core)** | DNSPolicy |
| `nodeSelector`  
map\[string\]string | NodeSelector |
| `topologySpreadConstraints`  
**[\[\]Kubernetes core/v1.TopologySpreadConstraint](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#topologyspreadconstraint-v1-core)** | TopologySpreadConstraints |
| `securityContext`  
**[Kubernetes core/v1.PodSecurityContext](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#podsecuritycontext-v1-core)** | PodSecurityContext |

### PodSpecTemplate

**Appears on:**

-   [IntegrationSpec](#_camel_apache_org_v1_IntegrationSpec)
    

PodSpecTemplate represent a template used to deploy an Integration `Pod`.

 
| Field | Description |
| --- | --- |
| `spec`  
**[PodSpec](#_camel_apache_org_v1_PodSpec)** | the specification |

### Properties(`map[string]string` alias)

**Appears on:**

-   [Server](#_camel_apache_org_v1_Server)
    
-   [StringOrProperties](#_camel_apache_org_v1_StringOrProperties)
    

Properties — .

### PublishTask

**Appears on:**

-   [BuildahTask](#_camel_apache_org_v1_BuildahTask)
    
-   [JibTask](#_camel_apache_org_v1_JibTask)
    
-   [KanikoTask](#_camel_apache_org_v1_KanikoTask)
    
-   [S2iTask](#_camel_apache_org_v1_S2iTask)
    
-   [SpectrumTask](#_camel_apache_org_v1_SpectrumTask)
    

PublishTask image publish configuration.

 
| Field | Description |
| --- | --- |
| `contextDir`  
string | can be useful to share info with other tasks |
| `baseImage`  
string | base image layer |
| `image`  
string | final image name |
| `registry`  
**[RegistrySpec](#_camel_apache_org_v1_RegistrySpec)** | where to publish the final image |

### RawMessage(`[]byte` alias)

**Appears on:**

-   [AddonTrait](#_camel_apache_org_v1_AddonTrait)
    
-   [BeanProperties](#_camel_apache_org_v1_BeanProperties)
    
-   [EndpointProperties](#_camel_apache_org_v1_EndpointProperties)
    
-   [ErrorHandlerParameters](#_camel_apache_org_v1_ErrorHandlerParameters)
    
-   [ErrorHandlerSpec](#_camel_apache_org_v1_ErrorHandlerSpec)
    
-   [Flow](#_camel_apache_org_v1_Flow)
    
-   [HealthCheckResponse](#_camel_apache_org_v1_HealthCheckResponse)
    
-   [JSON](#_camel_apache_org_v1_JSON)
    
-   [Template](#_camel_apache_org_v1_Template)
    
-   [TraitConfiguration](#_camel_apache_org_v1_TraitConfiguration)
    

RawMessage is a raw encoded JSON value. It implements Marshaler and Unmarshaler and can be used to delay JSON decoding or precompute a JSON encoding.

### RegistrySpec

**Appears on:**

-   [IntegrationPlatformBuildSpec](#_camel_apache_org_v1_IntegrationPlatformBuildSpec)
    
-   [IntegrationProfileBuildSpec](#_camel_apache_org_v1_IntegrationProfileBuildSpec)
    
-   [PublishTask](#_camel_apache_org_v1_PublishTask)
    

RegistrySpec provides the configuration for the container registry.

 
| Field | Description |
| --- | --- |
| `insecure`  
bool | if the container registry is insecure (ie, http only) |
| `address`  
string | the URI to access |
| `secret`  
string | the secret where credentials are stored |
| `ca`  
string | the configmap which stores the Certificate Authority |
| `organization`  
string | the registry organization |

### Repository

**Appears on:**

-   [MavenBuildSpec](#_camel_apache_org_v1_MavenBuildSpec)
    

Repository defines a Maven repository.

 
| Field | Description |
| --- | --- |
| `id`  
string | identifies the repository |
| `name`  
string | name of the repository |
| `url`  
string | location of the repository |
| `snapshots`  
**[RepositoryPolicy](#_camel_apache_org_v1_RepositoryPolicy)** | can use snapshot |
| `releases`  
**[RepositoryPolicy](#_camel_apache_org_v1_RepositoryPolicy)** | can use stable releases |

### RepositoryPolicy

**Appears on:**

-   [Repository](#_camel_apache_org_v1_Repository)
    

RepositoryPolicy defines the policy associated to a Maven repository.

 
| Field | Description |
| --- | --- |
| `enabled`  
bool | is the policy activated or not |
| `updatePolicy`  
string | This element specifies how often updates should attempt to occur. Maven will compare the local POM’s timestamp (stored in a repository’s maven-metadata file) to the remote. The choices are: `always`, `daily` (default), `interval:X` (where X is an integer in minutes) or `never` |
| `checksumPolicy`  
string | When Maven deploys files to the repository, it also deploys corresponding checksum files. Your options are to `ignore`, `fail`, or `warn` on missing or incorrect checksums. |

### ResourceCondition

ResourceCondition is a common type for all conditions.

### RuntimeProvider(`string` alias)

**Appears on:**

-   [Catalog](#_camel_apache_org_v1_Catalog)
    
-   [IntegrationKitStatus](#_camel_apache_org_v1_IntegrationKitStatus)
    
-   [IntegrationPlatformBuildSpec](#_camel_apache_org_v1_IntegrationPlatformBuildSpec)
    
-   [IntegrationProfileBuildSpec](#_camel_apache_org_v1_IntegrationProfileBuildSpec)
    
-   [IntegrationStatus](#_camel_apache_org_v1_IntegrationStatus)
    
-   [RuntimeSpec](#_camel_apache_org_v1_RuntimeSpec)
    

RuntimeProvider is the provider chosen for the runtime.

### RuntimeSpec

**Appears on:**

-   [BuilderTask](#_camel_apache_org_v1_BuilderTask)
    
-   [CamelCatalogSpec](#_camel_apache_org_v1_CamelCatalogSpec)
    

RuntimeSpec represents the configuration for the Java runtime in charge to execute the Camel application.

 
| Field | Description |
| --- | --- |
| `version`  
string | Camel K Runtime version |
| `provider`  
**[RuntimeProvider](#_camel_apache_org_v1_RuntimeProvider)** | Camel main application provider, ie, Camel Quarkus |
| `applicationClass`  
string | application entry point (main) to be executed |
| `dependencies`  
**[\[\]MavenArtifact](#_camel_apache_org_v1_MavenArtifact)** | list of dependencies needed to run the application |
| `metadata`  
map\[string\]string | set of metadata |
| `capabilities`  
**[map\[string\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.Capability](#_camel_apache_org_v1_Capability)** | features offered by this runtime |

### S2iTask

**Appears on:**

-   [Task](#_camel_apache_org_v1_Task)
    

S2iTask is used to configure S2I.

 
| Field | Description |
| --- | --- |
| `BaseTask`  
**[BaseTask](#_camel_apache_org_v1_BaseTask)** | (Members of `BaseTask` are embedded into this type.) |
| `PublishTask`  
**[PublishTask](#_camel_apache_org_v1_PublishTask)** | (Members of `PublishTask` are embedded into this type.) |
| `tag`  
string | used by the ImageStream |

### Server

**Appears on:**

-   [MavenBuildSpec](#_camel_apache_org_v1_MavenBuildSpec)
    

Server see [Maven settings](https://maven.apache.org/settings.md).

 
| Field | Description |
| --- | --- |
| `-`  
encoding/xml.Name | 
 |
| `id`  
string | 

 |
| `username`  
string | 

 |
| `password`  
string | 

 |
| `configuration`  
**[Properties](#_camel_apache_org_v1_Properties)** | 

 |

### SourceSpec

**Appears on:**

-   [BuilderTask](#_camel_apache_org_v1_BuilderTask)
    
-   [IntegrationKitSpec](#_camel_apache_org_v1_IntegrationKitSpec)
    
-   [IntegrationSpec](#_camel_apache_org_v1_IntegrationSpec)
    
-   [IntegrationStatus](#_camel_apache_org_v1_IntegrationStatus)
    
-   [KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)
    

SourceSpec defines the configuration for one or more routes to be executed in a certain Camel DSL language.

 
| Field | Description |
| --- | --- |
| `DataSpec`  
**[DataSpec](#_camel_apache_org_v1_DataSpec)** | (Members of `DataSpec` are embedded into this type.)
contains configuration related to the source code

 |
| `language`  
**[Language](#_camel_apache_org_v1_Language)** | specify which is the language (Camel DSL) used to interpret this source code |
| `loader`  
string | Loader is an optional id of the org.apache.camel.k.RoutesLoader that will interpret this source at runtime |
| `interceptors`  
\[\]string | Interceptors are optional identifiers the org.apache.camel.k.RoutesLoader uses to pre/post process sources.

Deprecated: no longer in use.

 |
| `type`  
**[SourceType](#_camel_apache_org_v1_SourceType)** | Type defines the kind of source described by this object |
| `property-names`  
\[\]string | List of property names defined in the source (e.g. if type is "template") |
| `from-kamelet`  
bool | True if the spec is generated from a Kamelet |

### SourceType(`string` alias)

**Appears on:**

-   [SourceSpec](#_camel_apache_org_v1_SourceSpec)
    

SourceType represents an available source type.

### SpectrumTask

**Appears on:**

-   [Task](#_camel_apache_org_v1_Task)
    

SpectrumTask is used to configure Spectrum.

Deprecated: no longer in use.

 
| Field | Description |
| --- | --- |
| `BaseTask`  
**[BaseTask](#_camel_apache_org_v1_BaseTask)** | (Members of `BaseTask` are embedded into this type.) |
| `PublishTask`  
**[PublishTask](#_camel_apache_org_v1_PublishTask)** | (Members of `PublishTask` are embedded into this type.) |

### StringOrProperties

StringOrProperties — .

 
| Field | Description |
| --- | --- |
| `-`  
string | 
 |
| `properties`  
**[Properties](#_camel_apache_org_v1_Properties)** | 

 |

### Task

**Appears on:**

-   [BuildSpec](#_camel_apache_org_v1_BuildSpec)
    

Task represents the abstract task. Only one of the task should be configured to represent the specific task chosen.

 
| Field | Description |
| --- | --- |
| `builder`  
**[BuilderTask](#_camel_apache_org_v1_BuilderTask)** | a BuilderTask, used to generate and build the project |
| `custom`  
**[UserTask](#_camel_apache_org_v1_UserTask)** | User customizable task execution. These are executed after the build and before the package task. |
| `package`  
**[BuilderTask](#_camel_apache_org_v1_BuilderTask)** | Application pre publishing a PackageTask, used to package the project |
| `buildah`  
**[BuildahTask](#_camel_apache_org_v1_BuildahTask)** | a BuildahTask, for Buildah strategy.
Deprecated: use jib or a custom publishing strategy instead

 |
| `kaniko`  
**[KanikoTask](#_camel_apache_org_v1_KanikoTask)** | a KanikoTask, for Kaniko strategy.

Deprecated: use jib or a custom publishing strategy instead

 |
| `spectrum`  
**[SpectrumTask](#_camel_apache_org_v1_SpectrumTask)** | a SpectrumTask, for Spectrum strategy.

Deprecated: use jib or a custom publishing strategy instead

 |
| `s2i`  
**[S2iTask](#_camel_apache_org_v1_S2iTask)** | a S2iTask, for S2I strategy.

Deprecated: use jib or a custom publishing strategy instead

 |
| `jib`  
**[JibTask](#_camel_apache_org_v1_JibTask)** | a JibTask, for Jib strategy |

### Template

**Appears on:**

-   [KameletSpecBase](#_camel_apache_org_v1_KameletSpecBase)
    

Template is an unstructured object representing a Kamelet template in YAML/JSON DSL.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.)
an unstructured raw message

 |

### TraitConfiguration

**Appears on:**

-   [TraitSpec](#_camel_apache_org_v1_TraitSpec)
    

TraitConfiguration represents the expected configuration for a given trait parameter.

Deprecated: superseded by each Trait type, left for backward compatibility.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_RawMessage)** | (Members of `RawMessage` are embedded into this type.)
generic raw message, typically a map containing the keys (trait parameters) and the values (either single text or array)

 |

### TraitProfile(`string` alias)

**Appears on:**

-   [IntegrationKitSpec](#_camel_apache_org_v1_IntegrationKitSpec)
    
-   [IntegrationPlatformSpec](#_camel_apache_org_v1_IntegrationPlatformSpec)
    
-   [IntegrationSpec](#_camel_apache_org_v1_IntegrationSpec)
    
-   [IntegrationStatus](#_camel_apache_org_v1_IntegrationStatus)
    

TraitProfile represents lists of traits that are enabled for the specific installation/integration.

Deprecated: may be removed in future releases.

### TraitSpec

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

A TraitSpec contains the configuration of a trait.

Deprecated: superseded by each Trait type, left for backward compatibility.

 
| Field | Description |
| --- | --- |
| `configuration`  
**[TraitConfiguration](#_camel_apache_org_v1_TraitConfiguration)** | TraitConfiguration parameters configuration |

### Traits

**Appears on:**

-   [IntegrationPlatformSpec](#_camel_apache_org_v1_IntegrationPlatformSpec)
    
-   [IntegrationProfileSpec](#_camel_apache_org_v1_IntegrationProfileSpec)
    
-   [IntegrationSpec](#_camel_apache_org_v1_IntegrationSpec)
    
-   [IntegrationStatus](#_camel_apache_org_v1_IntegrationStatus)
    
-   [PipeSpec](#_camel_apache_org_v1_PipeSpec)
    

Traits represents the collection of trait configurations.

 
| Field | Description |
| --- | --- |
| `affinity`  
**[AffinityTrait](#_camel_apache_org_v1_trait_AffinityTrait)** | The configuration of Affinity trait |
| `builder`  
**[BuilderTrait](#_camel_apache_org_v1_trait_BuilderTrait)** | The configuration of Builder trait |
| `camel`  
**[CamelTrait](#_camel_apache_org_v1_trait_CamelTrait)** | The configuration of Camel trait |
| `container`  
**[ContainerTrait](#_camel_apache_org_v1_trait_ContainerTrait)** | The configuration of Container trait |
| `cron`  
**[CronTrait](#_camel_apache_org_v1_trait_CronTrait)** | The configuration of Cron trait |
| `dependencies`  
**[DependenciesTrait](#_camel_apache_org_v1_trait_DependenciesTrait)** | The configuration of Dependencies trait |
| `deployer`  
**[DeployerTrait](#_camel_apache_org_v1_trait_DeployerTrait)** | The configuration of Deployer trait |
| `deployment`  
**[DeploymentTrait](#_camel_apache_org_v1_trait_DeploymentTrait)** | The configuration of Deployment trait |
| `environment`  
**[EnvironmentTrait](#_camel_apache_org_v1_trait_EnvironmentTrait)** | The configuration of Environment trait |
| `error-handler`  
**[ErrorHandlerTrait](#_camel_apache_org_v1_trait_ErrorHandlerTrait)** | The configuration of Error Handler trait.
Deprecated: no longer in use.

 |
| `gateway`  
**[GatewayTrait](#_camel_apache_org_v1_trait_GatewayTrait)** | The configuration of Istio trait |
| `gc`  
**[GCTrait](#_camel_apache_org_v1_trait_GCTrait)** | The configuration of GC trait |
| `gitops`  
**[GitOpsTrait](#_camel_apache_org_v1_trait_GitOpsTrait)** | The configuration of GitOps trait |
| `health`  
**[HealthTrait](#_camel_apache_org_v1_trait_HealthTrait)** | The configuration of Health trait |
| `ingress`  
**[IngressTrait](#_camel_apache_org_v1_trait_IngressTrait)** | The configuration of Ingress trait |
| `init-containers`  
**[InitContainersTrait](#_camel_apache_org_v1_trait_InitContainersTrait)** | The configuration of Init Containers trait |
| `istio`  
**[IstioTrait](#_camel_apache_org_v1_trait_IstioTrait)** | The configuration of Istio trait |
| `jolokia`  
**[JolokiaTrait](#_camel_apache_org_v1_trait_JolokiaTrait)** | The configuration of Jolokia trait.

Deprecated: no longer in use.

 |
| `jvm`  
**[JVMTrait](#_camel_apache_org_v1_trait_JVMTrait)** | The configuration of JVM trait |
| `kamelets`  
**[KameletsTrait](#_camel_apache_org_v1_trait_KameletsTrait)** | The configuration of Kamelets trait |
| `keda`  
**[KedaTrait](#_camel_apache_org_v1_trait_KedaTrait)** | The configuration of Keda trait |
| `knative`  
**[KnativeTrait](#_camel_apache_org_v1_trait_KnativeTrait)** | The configuration of Knative trait |
| `knative-service`  
**[KnativeServiceTrait](#_camel_apache_org_v1_trait_KnativeServiceTrait)** | The configuration of Knative Service trait |
| `logging`  
**[LoggingTrait](#_camel_apache_org_v1_trait_LoggingTrait)** | The configuration of Logging trait |
| `master`  
**[MasterTrait](#_camel_apache_org_v1_trait_MasterTrait)** | The configuration of Master trait |
| `mount`  
**[MountTrait](#_camel_apache_org_v1_trait_MountTrait)** | The configuration of Mount trait |
| `openapi`  
**[OpenAPITrait](#_camel_apache_org_v1_trait_OpenAPITrait)** | The configuration of OpenAPI trait.

Deprecated: no longer in use.

 |
| `owner`  
**[OwnerTrait](#_camel_apache_org_v1_trait_OwnerTrait)** | The configuration of Owner trait |
| `pdb`  
**[PDBTrait](#_camel_apache_org_v1_trait_PDBTrait)** | The configuration of PDB trait |
| `platform`  
**[PlatformTrait](#_camel_apache_org_v1_trait_PlatformTrait)** | The configuration of Platform trait |
| `pod`  
**[PodTrait](#_camel_apache_org_v1_trait_PodTrait)** | The configuration of Pod trait. |
| `prometheus`  
**[PrometheusTrait](#_camel_apache_org_v1_trait_PrometheusTrait)** | The configuration of Prometheus trait |
| `pull-secret`  
**[PullSecretTrait](#_camel_apache_org_v1_trait_PullSecretTrait)** | The configuration of Pull Secret trait |
| `quarkus`  
**[QuarkusTrait](#_camel_apache_org_v1_trait_QuarkusTrait)** | The configuration of Quarkus trait |
| `registry`  
**[RegistryTrait](#_camel_apache_org_v1_trait_RegistryTrait)** | The configuration of Registry trait (support removed since version 2.5.0).

Deprecated: no longer in use.

 |
| `route`  
**[RouteTrait](#_camel_apache_org_v1_trait_RouteTrait)** | The configuration of Route trait.

Deprecated: use ingress instead.

 |
| `security-context`  
**[SecurityContextTrait](#_camel_apache_org_v1_trait_SecurityContextTrait)** | The configuration of Security Context trait |
| `service`  
**[ServiceTrait](#_camel_apache_org_v1_trait_ServiceTrait)** | The configuration of Service trait |
| `service-binding`  
**[ServiceBindingTrait](#_camel_apache_org_v1_trait_ServiceBindingTrait)** | The configuration of Service Binding trait.

Deprecated: no longer in use.

 |
| `telemetry`  
**[TelemetryTrait](#_camel_apache_org_v1_trait_TelemetryTrait)** | The configuration of Telemetry trait |
| `toleration`  
**[TolerationTrait](#_camel_apache_org_v1_trait_TolerationTrait)** | The configuration of Toleration trait |
| `addons`  
**[map\[string\]github.com/apache/camel-k/v2/pkg/apis/camel/v1.AddonTrait](#_camel_apache_org_v1_AddonTrait)** | Deprecated: no longer in use. |
| `strimzi`  
**[TraitSpec](#_camel_apache_org_v1_TraitSpec)** | Deprecated: no longer in use. |
| `3scale`  
**[TraitSpec](#_camel_apache_org_v1_TraitSpec)** | Deprecated: no longer in use. |
| `tracing`  
**[TraitSpec](#_camel_apache_org_v1_TraitSpec)** | Deprecated: no longer in use. |

### TypeSlot(`string` alias)

TypeSlot represent a kind of data (ie, input, output, …​).

### UserTask

**Appears on:**

-   [Task](#_camel_apache_org_v1_Task)
    

UserTask is used to execute any generic custom operation.

 
| Field | Description |
| --- | --- |
| `BaseTask`  
**[BaseTask](#_camel_apache_org_v1_BaseTask)** | (Members of `BaseTask` are embedded into this type.) |
| `image`  
string | the container image to use |
| `userId`  
int64 | the user id used to run the container |
| `command`  
string | the command to execute.
Deprecated: use ContainerCommands

 |
| `commands`  
\[\]string | the command to execute |
| `publishingImage`  
string | the desired image build name |

### ValueSource

**Appears on:**

-   [MavenSpec](#_camel_apache_org_v1_MavenSpec)
    

ValueSource --.

 
| Field | Description |
| --- | --- |
| `configMapKeyRef`  
**[Kubernetes core/v1.ConfigMapKeySelector](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#configmapkeyselector-v1-core)** | Selects a key of a ConfigMap. |
| `secretKeyRef`  
**[Kubernetes core/v1.SecretKeySelector](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#secretkeyselector-v1-core)** | Selects a key of a secret. |

### AffinityTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

Allows constraining which nodes the integration pod(s) are eligible to be scheduled on, based on labels on the node, or with inter-pod affinity and anti-affinity, based on labels on pods that are already running on the nodes.

It’s disabled by default.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `podAffinity`  
bool | Always co-locates multiple replicas of the integration in the same node (default `false`). |
| `podAntiAffinity`  
bool | Never co-locates multiple replicas of the integration in the same node (default `false`). |
| `nodeAffinityLabels`  
\[\]string | Defines a set of nodes the integration pod(s) are eligible to be scheduled on, based on labels on the node. |
| `podAffinityLabels`  
\[\]string | Defines a set of pods (namely those matching the label selector, relative to the given namespace) that the integration pod(s) should be co-located with. |
| `podAntiAffinityLabels`  
\[\]string | Defines a set of pods (namely those matching the label selector, relative to the given namespace) that the integration pod(s) should not be co-located with. |

### BaseTruststore

**Appears on:**

-   [JVMTrait](#_camel_apache_org_v1_trait_JVMTrait)
    

BaseTruststore represents an existing truststore to use as the base for adding certificates.

 
| Field | Description |
| --- | --- |
| `truststorePath`  
string | Path to the base truststore file. |
| `passwordPath`  
string | Path to a file containing the password for the base truststore. |

### BuilderTrait

**Appears on:**

-   [IntegrationKitTraits](#_camel_apache_org_v1_IntegrationKitTraits)
    
-   [Traits](#_camel_apache_org_v1_Traits)
    

The builder trait is internally used to determine the best strategy to build and configure IntegrationKits.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `verbose`  
bool | Enable verbose logging on build components that support it (e.g. Kaniko build pod).
Deprecated: no longer in use

 |
| `properties`  
\[\]string | A list of properties to be provided to the build task |
| `strategy`  
string | The strategy to use, either `pod` or `routine` (default `routine`) |
| `baseImage`  
string | Specify a base image. In order to have the application working properly it must be a container image which has a Java JDK installed and ready to use on path (ie `/usr/bin/java`). |
| `incrementalImageBuild`  
bool | Use the incremental image build option, to reuse existing containers (default `true`) |
| `orderStrategy`  
string | The build order strategy to use, either `dependencies`, `fifo` or `sequential` (default is the platform default) |
| `requestCPU`  
string | When using `pod` strategy, the minimum amount of CPU required by the pod builder.

Deprecated: use TasksRequestCPU instead with task name `builder`.

 |
| `requestMemory`  
string | When using `pod` strategy, the minimum amount of memory required by the pod builder.

Deprecated: use TasksRequestCPU instead with task name `builder`.

 |
| `limitCPU`  
string | When using `pod` strategy, the maximum amount of CPU required by the pod builder.

Deprecated: use TasksRequestCPU instead with task name `builder`.

 |
| `limitMemory`  
string | When using `pod` strategy, the maximum amount of memory required by the pod builder.

Deprecated: use TasksRequestCPU instead with task name `builder`.

 |
| `mavenProfiles`  
\[\]string | Deprecated: no longer in use. |
| `tasks`  
\[\]string | A list of tasks to be executed (available only when using `pod` strategy) with format `<name>;<container-image>;<container-command>`.

Deprecated: may be removed in future versions.

 |
| `tasksFilter`  
string | A list of tasks sorted by the order of execution in a csv format, ie, `<taskName1>,<taskName2>,…​`. Mind that you must include also the operator tasks (`builder`, `quarkus-native`, `package`, `jib`, `s2i`) if you need to execute them. Useful only with `pod` strategy. Disabled by default, you need to enable via BUILDER\_TASKS\_ENABLED=true environment variable on operator Deployment.

Deprecated: may be removed in future versions.

 |
| `tasksRequestCPU`  
\[\]string | A list of request cpu configuration for the specific task with format `<task-name>:<request-cpu-conf>`. |
| `tasksRequestMemory`  
\[\]string | A list of request memory configuration for the specific task with format `<task-name>:<request-memory-conf>`. |
| `tasksLimitCPU`  
\[\]string | A list of limit cpu configuration for the specific task with format `<task-name>:<limit-cpu-conf>`. |
| `tasksLimitMemory`  
\[\]string | A list of limit memory configuration for the specific task with format `<task-name>:<limit-memory-conf>`. |
| `nodeSelector`  
map\[string\]string | Defines a set of nodes the builder pod is eligible to be scheduled on, based on labels on the node. |
| `annotations`  
map\[string\]string | When using `pod` strategy, annotation to use for the builder pod. |
| `platforms`  
\[\]string | The list of manifest platforms to use to build a container image (default `linux/amd64`). |

### CACertConfig

**Appears on:**

-   [JVMTrait](#_camel_apache_org_v1_trait_JVMTrait)
    

CACertConfig specifies a CA certificate to import into the truststore.

 
| Field | Description |
| --- | --- |
| `certPath`  
string | Path to the PEM-encoded CA certificate file to import. |

### CamelTrait

**Appears on:**

-   [IntegrationKitTraits](#_camel_apache_org_v1_IntegrationKitTraits)
    
-   [Traits](#_camel_apache_org_v1_Traits)
    

The Camel trait can be used to configure versions of Camel runtime and related libraries, it cannot be disabled.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `runtimeProvider`  
string | The runtime provider to use for the integration. (Default, plain Quarkus). |
| `runtimeVersion`  
string | The runtime version to use for the integration. It overrides the default version set in the Integration Platform. You can use a fixed version (for example "3.2.3") or a semantic version (for example "3.x") which will try to resolve to the best matching Catalog existing on the cluster (Default, the one provided by the operator version). |
| `properties`  
\[\]string | A list of properties to be provided to the Integration runtime |

### Configuration

**Appears on:**

-   [PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)
    
-   [Trait](#_camel_apache_org_v1_trait_Trait)
    

Configuration defines the trait structure.

Deprecated: for backward compatibility.

 
| Field | Description |
| --- | --- |
| `RawMessage`  
**[RawMessage](#_camel_apache_org_v1_trait_RawMessage)** | (Members of `RawMessage` are embedded into this type.) |

### ContainerTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Container trait can be used to configure properties of the container where the integration will run.

It also provides configuration for Services associated to the container.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `auto`  
bool | To automatically enable the trait |
| `requestCPU`  
string | The minimum amount of CPU required (default 125 millicores). |
| `requestMemory`  
string | The minimum amount of memory required (default 128 Mi). |
| `limitCPU`  
string | The maximum amount of CPU to be provided (default 500 millicores). |
| `limitMemory`  
string | The maximum amount of memory to be provided (default 512 Mi). |
| `ports`  
\[\]string | List of container ports available in the container (syntax: <port-name>;<port-number>\[;port-protocol\]). When omitted, `port-protocol` (admitted values `TCP`, `UDP` or `SCTP`) is `TCP`. Don’t use this for the primary http managed port (for which case you need to use `portName` and `port`). Don’t use in Knative based environments. |
| `expose`  
bool | Can be used to enable/disable http exposure via kubernetes Service. |
| `port`  
int32 | To configure a different http port exposed by the container (default `8080`). |
| `portName`  
string | To configure a different http port name for the port exposed by the container. It defaults to `http` only when the `expose` parameter is true. |
| `servicePort`  
int32 | To configure under which service port the http container port is to be exposed (default `80`). |
| `servicePortName`  
string | To configure under which service port name the http container port is to be exposed (default `http`). |
| `name`  
string | The main container name. It’s named `integration` by default. |
| `image`  
string | The main container image to use for the Integration. When using this parameter the operator will create a synthetic IntegrationKit which won’t be able to execute traits requiring CamelCatalog. If the container image you’re using is coming from an IntegrationKit, use instead Integration `.spec.integrationKit` parameter. If you’re moving the Integration across environments, you will also need to create an "external" IntegrationKit. |
| `imagePullPolicy`  
**[Kubernetes core/v1.PullPolicy](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#pullpolicy-v1-core)** | The pull policy: Always|Never|IfNotPresent |
| `runAsUser`  
int64 | Security Context RunAsUser configuration (default none): this value is automatically retrieved in Openshift clusters when not explicitly set. |
| `runAsNonRoot`  
bool | Security Context RunAsNonRoot configuration (default false). |
| `seccompProfileType`  
**[Kubernetes core/v1.SeccompProfileType](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#seccompprofiletype-v1-core)** | Security Context SeccompProfileType configuration (default RuntimeDefault). |
| `allowPrivilegeEscalation`  
bool | Security Context AllowPrivilegeEscalation configuration (default false). |
| `capabilitiesDrop`  
**[\[\]Kubernetes core/v1.Capability](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#capability-v1-core)** | Security Context Capabilities Drop configuration (default ALL). |
| `capabilitiesAdd`  
**[\[\]Kubernetes core/v1.Capability](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#capability-v1-core)** | Security Context Capabilities Add configuration (default none). |

### CronTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Cron trait can be used to customize the behaviour of periodic timer/cron based integrations.

While normally an integration requires a pod to be always up and running, some periodic tasks, such as batch jobs, require to be activated at specific hours of the day or with a periodic delay of minutes. For such tasks, the cron trait can materialize the integration as a Kubernetes CronJob instead of a standard deployment, in order to save resources when the integration does not need to be executed.

Integrations that start from the following components are evaluated by the cron trait: `timer`, `cron`, `quartz`. The trait does support multiple evaluated components only if they have the same schedule, else it will fallback to Camel implementation instead of instantiating a Kubernetes CronJob.

> **Warning**
> In case of native build-mode defined in [quarkus](../traits/quarkus.md) trait, the component can’t be customized.

The rules for using a Kubernetes CronJob are the following:

-   `timer`: when period is set in milliseconds with no remaining seconds, for example 120000. If there is any second left as in 121000 (120s and 1s) or the presence of any of these parameters (delay, repeatCount, time) then a CronJob won’t be created, but a standard deployment.
    
-   `cron`, `quartz`: when the cron expression does not contain seconds (or the "seconds" part is set to 0). E.g.
    
    \`cron:tab?schedule=0/2 \* \* \* ?\` or \`quartz:trigger?cron=0 0/2 \* \* \* ?\`.
    

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `schedule`  
string | The CronJob schedule for the whole integration. If multiple routes are declared, they must have the same schedule for this mechanism to work correctly. |
| `timeZone`  
string | The timezone that the CronJob will run on |
| `components`  
string | A comma separated list of the Camel components that need to be customized in order for them to work when the schedule is triggered externally by Kubernetes. Supported components are currently: `cron`, `timer` and `quartz`. |
| `fallback`  
bool | Use the default Camel implementation of the `cron` endpoint (`quartz`) instead of trying to materialize the integration as Kubernetes CronJob. |
| `concurrencyPolicy`  
string | Specifies how to treat concurrent executions of a Job. Valid values are: - "Allow": allows CronJobs to run concurrently; - "Forbid" (default): forbids concurrent runs, skipping next run if previous run hasn’t finished yet; - "Replace": cancels currently running job and replaces it with a new one |
| `auto`  
bool | Automatically deploy the integration as CronJob when all routes are either starting from a periodic consumer (only `cron`, `timer` and `quartz` are supported) or a passive consumer (e.g. `direct` is a passive consumer).
It’s required that all periodic consumers have the same period, and it can be expressed as cron schedule (e.g. `1m` can be expressed as `0/1 * * * *`, while `35m` or `50s` cannot).

 |
| `startingDeadlineSeconds`  
int64 | Optional deadline in seconds for starting the job if it misses scheduled time for any reason. Missed jobs executions will be counted as failed ones. |
| `activeDeadlineSeconds`  
int64 | Specifies the duration in seconds, relative to the start time, that the job may be continuously active before it is considered to be failed. It defaults to 60s. |
| `backoffLimit`  
int32 | Specifies the number of retries before marking the job failed. It defaults to 2. |

### DependenciesTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Dependencies trait is internally used to automatically add runtime dependencies based on the integration that the user wants to run.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |

### DeployerTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The deployer trait is responsible for deploying the resources owned by the integration, and can be used to explicitly select the underlying controller that will manage the integration pods.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `kind`  
string | Allows to explicitly select the desired deployment kind between `deployment`, `cron-job` or `knative-service` when creating the resources for running the integration.
Deprecated: this feature will be removed in future releases.

 |
| `useSSA`  
bool | Deprecated: no longer in use. |

### DeploymentTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Deployment trait is responsible for generating the Kubernetes deployment that will make sure the integration will run in the cluster.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `progressDeadlineSeconds`  
int32 | The maximum time in seconds for the deployment to make progress before it is considered to be failed. It defaults to `60s`. |
| `strategy`  
**[Kubernetes apps/v1.DeploymentStrategyType](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#deploymentstrategytype-v1-apps)** | The deployment strategy to use to replace existing pods with new ones. |
| `rollingUpdateMaxUnavailable`  
k8s.io/apimachinery/pkg/util/intstr.IntOrString | The maximum number of pods that can be unavailable during the update. Value can be an absolute number (ex: 5) or a percentage of desired pods (ex: 10%). Absolute number is calculated from percentage by rounding down. This can not be 0 if MaxSurge is 0. Defaults to `25%`. |
| `rollingUpdateMaxSurge`  
k8s.io/apimachinery/pkg/util/intstr.IntOrString | The maximum number of pods that can be scheduled above the desired number of pods. Value can be an absolute number (ex: 5) or a percentage of desired pods (ex: 10%). This can not be 0 if MaxUnavailable is 0. Absolute number is calculated from percentage by rounding up. Defaults to `25%`. |

### DiscoveryCacheType(`string` alias)

**Appears on:**

-   [GCTrait](#_camel_apache_org_v1_trait_GCTrait)
    

DiscoveryCacheType --.

### EnvironmentTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The environment trait is used internally to inject standard environment variables in the integration container, such as `NAMESPACE`, `POD_NAME` and others.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `containerMeta`  
bool | Enables injection of `NAMESPACE` and `POD_NAME` environment variables (default `true`) |
| `httpProxy`  
bool | Propagates the `HTTP_PROXY`, `HTTPS_PROXY` and `NO_PROXY` environment variables (default `true`) |
| `vars`  
\[\]string | A list of environment variables to be added to the integration container. The syntax is either VAR=VALUE or VAR=\[configmap|secret\]:name/key, where name represents the resource name, and key represents the resource key to be mapped as and environment variable. These take precedence over any previously defined environment variables. |

### ErrorHandlerTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

> **Warning**
> This trait is no longer in use.

The error-handler is a platform trait used to inject Error Handler source into the integration runtime.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `ref`  
string | The error handler ref name provided or found in application properties |

### GCTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The GC Trait garbage-collects all resources that are no longer necessary upon integration updates.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `discoveryCache`  
**[DiscoveryCacheType](#_camel_apache_org_v1_trait_DiscoveryCacheType)** | Discovery client cache to be used, either `disabled`, `disk` or `memory` (default `memory`).
Deprecated: no longer in use.

 |

### GatewayTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Gateway trait can be used to expose the service associated with the Integration to the outside world with a Kubernetes Gateway API. The trait is in charge to automatically discover associate the Integration Service generated with a Gateway and an HTTPRoute resource (HTTP/HTTPS protocol only supported).

> **Note**
> if any other protocol is required, please create a request in order to develop it.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `className`  
string | The class name to use for the gateway configuration. |
| `listeners`  
\[\]string | The listeners in the format "port;protocol" (default, "8080;HTTP"). |

### GitOpsTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The GitOps Trait is used to configure the repository where you want to push a GitOps Kustomize overlay configuration of the Integration or Pipe built. If the trait is enabled but no pull configuration is provided, then, the operator will use the values stored in Integration `.spec.git` field used to pull the project. When used with a Pipe, the `url` and `secret` parameters are required as Pipes do not have a `.spec.git` fallback.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `url`  
string | the URL of the repository where the project is stored. |
| `secret`  
string | the Kubernetes secret where the Git token is stored. The operator will pick up the first secret key only, whichever the name it is. |
| `branch`  
string | the git branch to check out. |
| `tag`  
string | the git tag to check out. |
| `commit`  
string | the git commit (full SHA) to check out. |
| `branchPush`  
string | the git branch to push to. If omitted, the operator will push to a new branch named as `cicd/release-candidate-<datetime>`. |
| `overlays`  
\[\]string | a list of overlays to provide (default \\{"dev","stag","prod"}). |
| `overwriteOverlay`  
bool | a flag (default, false) to overwrite any existing overlay. |
| `integrationDirectory`  
string | The root path where to store Kustomize overlays (default `integrations`). |
| `committerName`  
string | The name used to commit the GitOps changes (default `Camel K Operator`). |
| `committerEmail`  
string | The email used to commit the GitOps changes (default `camel-k-operator@apache.org`). |

### HealthTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The health trait is responsible for configuring the container probes on the Integration container.

> **Note**
> this trait is enabled by default in `plain-quarkus` runtime, leveraging the `camel-observability-services` component. You can disable turning it off.

The trait uses Camel health component in order to provide a readiness probe. You can also configure liveness and startup probes which are disabled by default. The default values (delay, timeout, etc…​), whereas not specified are the default ones provided by Kubernetes.

You can also configure manually the trait parameters in order to provide a customized probes configuration.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `livenessProbeEnabled`  
bool | Configures the liveness probe for the integration container (default `false`). |
| `livenessScheme`  
string | Scheme to use when connecting to the liveness probe (default `HTTP`). |
| `livenessInitialDelay`  
int32 | Number of seconds after the container has started before the liveness probe is initiated. |
| `livenessTimeout`  
int32 | Number of seconds after which the liveness probe times out. |
| `livenessPeriod`  
int32 | How often to perform the liveness probe. |
| `livenessSuccessThreshold`  
int32 | Minimum consecutive successes for the liveness probe to be considered successful after having failed. |
| `livenessFailureThreshold`  
int32 | Minimum consecutive failures for the liveness probe to be considered failed after having succeeded. |
| `livenessProbe`  
string | The liveness probe path to use (default provided by the dependency used). |
| `livenessPort`  
int32 | The liveness port to use (default 8080). |
| `readinessProbeEnabled`  
bool | Configures the readiness probe for the integration container (default `true`). |
| `readinessScheme`  
string | Scheme to use when connecting to the readiness probe (default `HTTP`). |
| `readinessInitialDelay`  
int32 | Number of seconds after the container has started before the readiness probe is initiated. |
| `readinessTimeout`  
int32 | Number of seconds after which the readiness probe times out. |
| `readinessPeriod`  
int32 | How often to perform the readiness probe. |
| `readinessSuccessThreshold`  
int32 | Minimum consecutive successes for the readiness probe to be considered successful after having failed. |
| `readinessFailureThreshold`  
int32 | Minimum consecutive failures for the readiness probe to be considered failed after having succeeded. |
| `readinessProbe`  
string | The readiness probe path to use (default provided by the dependency used). |
| `readinessPort`  
int32 | The readiness port to use (default 8080). |
| `startupProbeEnabled`  
bool | Configures the startup probe for the integration container (default `false`). |
| `startupScheme`  
string | Scheme to use when connecting to the startup probe (default `HTTP`). |
| `startupInitialDelay`  
int32 | Number of seconds after the container has started before the startup probe is initiated. |
| `startupTimeout`  
int32 | Number of seconds after which the startup probe times out. |
| `startupPeriod`  
int32 | How often to perform the startup probe. |
| `startupSuccessThreshold`  
int32 | Minimum consecutive successes for the startup probe to be considered successful after having failed. |
| `startupFailureThreshold`  
int32 | Minimum consecutive failures for the startup probe to be considered failed after having succeeded (default 10 if not specified). |
| `startupProbe`  
string | The startup probe path to use (default provided by the dependency used). |
| `startupPort`  
int32 | The startup port to use (default 8080). |

### IngressTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Ingress trait can be used to expose the service associated with the integration to the outside world with a Kubernetes Ingress.

It’s enabled by default whenever a Service is added to the integration (through the `service` trait).

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `ingressClassName`  
string | The Ingress class name as defined by the Ingress spec See [https://kubernetes.io/docs/concepts/services-networking/ingress/](https://kubernetes.io/docs/concepts/services-networking/ingress/) |
| `annotations`  
map\[string\]string | The annotations added to the ingress. This can be used to set controller specific annotations, e.g., when using the NGINX Ingress controller: See [https://github.com/kubernetes/ingress-nginx/blob/main/docs/user-guide/nginx-configuration/annotations.md](https://github.com/kubernetes/ingress-nginx/blob/main/docs/user-guide/nginx-configuration/annotations.md) |
| `host`  
string | To configure the host exposed by the ingress. |
| `path`  
string | To configure the path exposed by the ingress (default `/`).
Deprecated: In favor of `paths` - left for backward compatibility.

 |
| `paths`  
\[\]string | To configure the paths exposed by the ingress (default `['/']`). |
| `pathType`  
**[Kubernetes networking/v1.PathType](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#pathtype-v1-networking)** | To configure the path type exposed by the ingress. One of `Exact`, `Prefix`, `ImplementationSpecific` (default to `Prefix`). |
| `auto`  
bool | To automatically add an ingress whenever the integration uses an HTTP endpoint consumer. |
| `tlsHosts`  
\[\]string | To configure tls hosts |
| `tlsSecretName`  
string | To configure tls secret name |

### InitContainersTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Init Containers trait can be used to configure `init containers` or `sidecar containers`.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `initTasks`  
\[\]string | A list of init tasks to be executed. Each task accepts the format `<name>;<container-image>;<container-command>` or key=value format `name=<name>;image=<image>;command=<command>;request-cpu=<quantity>;limit-cpu=<quantity>;request-memory=<quantity>;limit-memory=<quantity>`. Resource keys (request-cpu, limit-cpu, request-memory, limit-memory) are optional and accept Kubernetes resource quantities. |
| `sideCarTasks`  
\[\]string | A list of sidecar tasks to be executed. Each task accepts the format `<name>;<container-image>;<container-command>` or key=value format `name=<name>;image=<image>;command=<command>;request-cpu=<quantity>;limit-cpu=<quantity>;request-memory=<quantity>;limit-memory=<quantity>`. Resource keys (request-cpu, limit-cpu, request-memory, limit-memory) are optional and accept Kubernetes resource quantities. |

### IstioTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Istio trait allows configuring properties related to the Istio service mesh, such as sidecar injection and outbound IP ranges.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `allow`  
string | Configures a (comma-separated) list of CIDR subnets that should not be intercepted by the Istio proxy (`10.0.0.0/8,172.16.0.0/12,192.168.0.0/16` by default). |
| `inject`  
bool | Forces the value for labels `sidecar.istio.io/inject`. By default the label is set to `true` on deployment and not set on Knative Service. |

### JVMTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The JVM trait is used to configure the JVM that runs the Integration. This trait is configured only for Integration and related IntegrationKits (bound to a container image) built by Camel K operator. If the system detects the usage of a different container image (ie, built externally), then, the trait is disabled by the platform.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `debug`  
bool | Activates remote debugging, so that a debugger can be attached to the JVM, e.g., using port-forwarding |
| `debugSuspend`  
bool | Suspends the target JVM immediately before the main class is loaded |
| `printCommand`  
bool | Prints the command used the start the JVM in the container logs (default `true`).
Deprecated: no longer in use.

 |
| `debugAddress`  
string | Transport address at which to listen for the newly launched JVM (default `*:5005`) |
| `options`  
\[\]string | A list of JVM options |
| `classpath`  
string | Additional JVM classpath (use `Linux` classpath separator) |
| `jar`  
string | The Jar dependency which will run the application. Leave it empty for managed Integrations. |
| `agents`  
\[\]string | A list of JVM agents to download and execute with format `<agent-name>;<agent-url>[;<jvm-agent-options>]`. |
| `caCertificates`  
**[\[\]CACertConfig](#_camel_apache_org_v1_trait_CACertConfig)** | A list of CA certificates to import into the truststore. Certificates must be mounted via the mount trait. |
| `baseTruststore`  
**[BaseTruststore](#_camel_apache_org_v1_trait_BaseTruststore)** | Optional base truststore to use as the starting point for adding certificates. |
| `truststorePasswordPath`  
string | Path to a file containing the password for the generated truststore. Required when using ca-certificates without base-truststore. |
| `caCertMountPath`  
string | The path where the generated truststore will be mounted (default `/etc/camel/conf.d/_truststore`). |
| `caCert`  
string | Deprecated: Use CACertificates instead. Path to a PEM-encoded CA certificate file. |
| `caCertPassword`  
string | Deprecated: Use CACertificates instead. Path to a file containing the truststore password. |

### JolokiaTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

> **Warning**
> This trait is no longer in use.

The Jolokia trait activates and configures the Jolokia Java agent. This trait is useful to enable JMX access to Camel application. Make sure you have the right privileges to perform such an action on the cluster.

See [https://jolokia.org/reference/html/manual/agents.html](https://jolokia.org/reference/html/manual/agents.md)

> **Warning**
> The Jolokia trait is **deprecated** and will removed in future release versions: use `jvm.agents` configuration instead.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `CACert`  
string | The PEM encoded CA certification file path, used to verify client certificates, applicable when `protocol` is `https` and `use-ssl-client-authentication` is `true` (default `/var/run/secrets/kubernetes.io/serviceaccount/service-ca.crt` for OpenShift). |
| `clientPrincipal`  
\[\]string | The principal(s) which must be given in a client certificate to allow access to the Jolokia endpoint, applicable when `protocol` is `https` and `use-ssl-client-authentication` is `true` (default `clientPrincipal=cn=system:master-proxy`, `cn=hawtio-online.hawtio.svc` and `cn=fuse-console.fuse.svc` for OpenShift). |
| `discoveryEnabled`  
bool | Listen for multicast requests (default `false`) |
| `extendedClientCheck`  
bool | Mandate the client certificate contains a client flag in the extended key usage section, applicable when `protocol` is `https` and `use-ssl-client-authentication` is `true` (default `true` for OpenShift). |
| `host`  
string | The Host address to which the Jolokia agent should bind to. If `"*"` or `"0.0.0.0"` is given, the servers binds to every network interface (default `"*"`). |
| `password`  
string | The password used for authentication, applicable when the `user` option is set. |
| `port`  
int32 | The Jolokia endpoint port (default `8778`). |
| `protocol`  
string | The protocol to use, either `http` or `https` (default `https` for OpenShift) |
| `user`  
string | The user to be used for authentication |
| `useSSLClientAuthentication`  
bool | Whether client certificates should be used for authentication (default `true` for OpenShift). |
| `options`  
\[\]string | A list of additional Jolokia options as defined in [JVM agent configuration options](https://jolokia.org/reference/html/agents.html#agent-jvm-config) |

### KameletsTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The kamelets trait is a platform trait used to inject Kamelets into the integration runtime.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `auto`  
bool | Automatically inject all referenced Kamelets and their default configuration (enabled by default) |
| `list`  
string | Comma separated list of Kamelet names to load into the current integration |
| `mountPoint`  
string | The directory where the application mounts and reads Kamelet spec (default `/etc/camel/kamelets`) |

### KedaSecret

**Appears on:**

-   [KedaTrigger](#_camel_apache_org_v1_trait_KedaTrigger)
    

 
| Field | Description |
| --- | --- |
| `name`  
string | The name of the secret to use. |
| `mapping`  
map\[string\]string | The mapping to use for this secret (eg, `database-secret-key:keda-secret-key`) |

### KedaTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The KEDA trait allows you to configure KEDA autoscalers to scale up and down based of events.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `pollingInterval`  
int32 | Interval (seconds) to check each trigger on. |
| `cooldownPeriod`  
int32 | The wait period between the last active trigger reported and scaling the resource back to 0. |
| `idleReplicaCount`  
int32 | Enabling this property allows KEDA to scale the resource down to the specified number of replicas. |
| `minReplicaCount`  
int32 | Minimum number of replicas. |
| `maxReplicaCount`  
int32 | Maximum number of replicas. |
| `triggers`  
**[\[\]KedaTrigger](#_camel_apache_org_v1_trait_KedaTrigger)** | Definition of triggers according to the KEDA format. Each trigger must contain `type` field corresponding to the name of a KEDA autoscaler and a key/value map named `metadata` containing specific trigger options and optionally a mapping of secrets, used by Keda operator to poll resources according to the autoscaler type. |
| `auto`  
bool | Automatically discover KEDA triggers from Camel component URIs. |
| `autoMetadata`  
map\[string\]map\[string\]string | Additional metadata to merge into auto-discovered triggers. Keys are trigger types (e.g., "kafka"), values are maps of metadata key-value pairs to merge (e.g., {"lagThreshold": "10"}). |

### KedaTrigger

**Appears on:**

-   [KedaTrait](#_camel_apache_org_v1_trait_KedaTrait)
    

 
| Field | Description |
| --- | --- |
| `type`  
string | The autoscaler type. |
| `metricType`  
string | **(Optional)**
The metric type for this trigger, mapping to KEDA’s trigger-level `metricType` (`Utilization`, `AverageValue` or `Value`).

 |
| `metadata`  
map\[string\]string | The trigger metadata (see Keda documentation to learn how to fill for each type). |
| `secrets`  
**[\[\]KedaSecret](#_camel_apache_org_v1_trait_KedaSecret)** | The secrets mapping to use. Keda allows the possibility to use values coming from different secrets. |

### KnativeServiceTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Knative Service trait allows configuring options when running the Integration as a Knative service, instead of a standard Kubernetes Deployment.

Running an Integration as a Knative Service enables auto-scaling (and scaling-to-zero), but those features are only relevant when the Camel route(s) use(s) an HTTP endpoint consumer.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `annotations`  
map\[string\]string | The annotations added to route. This can be used to set knative service specific annotations CLI usage example: -t "knative-service.annotations.'haproxy.router.openshift.io/balance'=true" |
| `class`  
string | Configures the Knative autoscaling class property (e.g. to set `hpa.autoscaling.knative.dev` or `kpa.autoscaling.knative.dev` autoscaling).
Refer to the Knative documentation for more information.

 |
| `autoscalingMetric`  
string | Configures the Knative autoscaling metric property (e.g. to set `concurrency` based or `cpu` based autoscaling).

Refer to the Knative documentation for more information.

 |
| `autoscalingTarget`  
int | Sets the allowed concurrency level or CPU percentage (depending on the autoscaling metric) for each Pod.

Refer to the Knative documentation for more information.

 |
| `minScale`  
int | The minimum number of Pods that should be running at any time for the integration. It’s **zero** by default, meaning that the integration is scaled down to zero when not used for a configured amount of time.

Refer to the Knative documentation for more information.

 |
| `maxScale`  
int | An upper bound for the number of Pods that can be running in parallel for the integration. Knative has its own cap value that depends on the installation.

Refer to the Knative documentation for more information.

 |
| `rolloutDuration`  
string | Enables to gradually shift traffic to the latest Revision and sets the rollout duration. It’s disabled by default and must be expressed as a Golang `time.Duration` string representation, rounded to a second precision. |
| `visibility`  
string | Setting `cluster-local`, Knative service becomes a private service. Specifically, this option applies the `networking.knative.dev/visibility` label to Knative service.

Refer to the Knative documentation for more information.

 |
| `auto`  
bool | 

Automatically deploy the integration as Knative service when all conditions hold:

-   Integration is using the Knative profile
    
-   All routes are either starting from an HTTP based consumer or a passive consumer (e.g. `direct` is a passive consumer)
    





 |
| `timeoutSeconds`  
int64 | The maximum duration in seconds that the request instance is allowed to respond to a request. This field propagates to the integration pod’s terminationGracePeriodSeconds

Refer to the Knative documentation for more information.

 |

### KnativeTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Knative trait automatically discovers addresses of Knative resources and inject them into the running integration.

The Camel Knative component will then use the full configuration to configure the routes.

> **Warning**
> The Knative trait is **deprecated** and will be removed in future release versions: use Camel (Quarkus) Knative component instead.

The trait is enabled by default when the Knative profile is active.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `config`  
string | Can be used to inject a Knative complete configuration in JSON format. |
| `channelSources`  
\[\]string | List of channels used as source of integration routes. Can contain simple channel names or full Camel URIs. |
| `channelSinks`  
\[\]string | List of channels used as destination of integration routes. Can contain simple channel names or full Camel URIs. |
| `endpointSources`  
\[\]string | List of channels used as source of integration routes. |
| `endpointSinks`  
\[\]string | List of endpoints used as destination of integration routes. Can contain simple endpoint names or full Camel URIs. |
| `eventSources`  
\[\]string | List of event types that the integration will be subscribed to. Can contain simple event types or full Camel URIs (to use a specific broker different from "default"). |
| `eventSinks`  
\[\]string | List of event types that the integration will produce. Can contain simple event types or full Camel URIs (to use a specific broker). |
| `filterSourceChannels`  
bool | Enables filtering on events based on the header "ce-knativehistory". Since this header has been removed in newer versions of Knative, filtering is disabled by default. |
| `sinkBinding`  
bool | Allows binding the integration to a sink via a Knative SinkBinding resource. This can be used when the integration targets a single sink. It’s enabled by default when the integration targets a single sink (except when the integration is owned by a Knative source). |
| `auto`  
bool | Enable automatic discovery of all trait properties. |
| `namespaceLabel`  
bool | Enables the camel-k-operator to set the "bindings.knative.dev/include=true" label to the namespace As Knative requires this label to perform injection of K\_SINK URL into the service. If this is false, the integration pod may start and fail, read the SinkBinding Knative documentation. (default: true) |
| `filters`  
\[\]string | Sets filter attributes on the event stream (such as event type, source, subject and so on). A list of key-value pairs that represent filter attributes and its values. The syntax is KEY=VALUE, e.g., `source="my.source"`. Filter attributes get set on the Knative trigger that is being created as part of this integration. |
| `filterEventType`  
bool | Enables the default filtering for the Knative trigger using the event type If this is true, the created Knative trigger uses the event type as a filter on the event stream when no other filter criteria is given. (default: true) |

### LoggingTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Logging trait is used to configure Integration runtime logging options (such as color and format). The logging backend is provided by Quarkus, whose configuration is documented at [https://quarkus.io/guides/logging](https://quarkus.io/guides/logging).

> **Warning**
> The Logging trait is **deprecated** and will be removed in future release versions: use Quarkus logging properties directly instead.

Migration example:

Before: traits.logging.level=DEBUG
After:  -p quarkus.log.level=DEBUG

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `color`  
bool | Colorize the log output |
| `format`  
string | Logs message format |
| `level`  
string | Adjust the logging level (defaults to `INFO`) |
| `json`  
bool | Output the logs in JSON |
| `jsonPrettyPrint`  
bool | Enable "pretty printing" of the JSON logs |

### MasterTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Master trait allows to configure the integration to automatically leverage Kubernetes resources for doing leader election and starting **master** routes only on certain instances.

It’s activated automatically when using the master endpoint in a route, e.g. `from("master:lockname:telegram:bots")…​`.

> **Note**
> this trait adds special permissions to the integration service account in order to read/write configmaps and read pods. It’s recommended to use a different service account than "default" when running the integration.

> **Warning**
> The Master trait is **deprecated** and will be removed in future release versions. This trait requires the operator to manage RBAC explicitly, which should be avoided for security and simplicity reasons. Users should manually create the required Role and RoleBinding, then configure Quarkus properties directly:

\-p quarkus.camel.cluster.kubernetes.resource-name=<integration>-lock
-p quarkus.camel.cluster.kubernetes.resource-type=Lease
-p quarkus.camel.cluster.kubernetes.labels."camel.apache.org/integration"=<integration-name>

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `auto`  
bool | Enables automatic configuration of the trait. |
| `includeDelegateDependencies`  
bool | When this flag is active, the operator analyzes the source code to add dependencies required by delegate endpoints. E.g. when using `master:lockname:timer`, then `camel:timer` is automatically added to the set of dependencies. It’s enabled by default. |
| `resourceName`  
string | Name of the configmap that will be used to store the lock. Defaults to "<integration-name>-lock". Name of the configmap/lease resource that will be used to store the lock. Defaults to "<integration-name>-lock". |
| `resourceType`  
string | Type of Kubernetes resource to use for locking ("ConfigMap" or "Lease"). Defaults to "Lease". |
| `labelKey`  
string | Label that will be used to identify all pods contending the lock. Defaults to "camel.apache.org/integration". |
| `labelValue`  
string | Label value that will be used to identify all pods contending the lock. Defaults to the integration name. |

### MountTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Mount trait can be used to configure volumes mounted on the Integration Pods.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `configs`  
\[\]string | A list of configuration pointing to configmap/secret. The configuration are expected to be UTF-8 resources as they are processed by runtime Camel Context and tried to be parsed as property files. They are also made available on the classpath in order to ease their usage directly from the Route. Syntax: \[configmap|secret\]:name\[/key\], where name represents the resource name and key optionally represents the resource key to be filtered |
| `resources`  
\[\]string | A list of resources (text or binary content) pointing to configmap/secret. The resources are expected to be any resource type (text or binary content). The destination path can be either a default location or any path specified by the user. Syntax: \[configmap|secret\]:name\[/key\]\[@path\], where name represents the resource name, key optionally represents the resource key to be filtered and path represents the destination path |
| `volumes`  
\[\]string | A list of Persistent Volume Claims to be mounted. Syntax: \[pvcname:/container/path\]. If the PVC is not found, the Integration fails. You can use the syntax \[pvcname:/container/path:size:accessMode<:storageClass>\] to create a dynamic PVC based on the Storage Class provided or the default cluster Storage Class. However, if the PVC exists, the operator would mount it. |
| `emptyDirs`  
\[\]string | A list of EmptyDir volumes to be mounted. An optional size limit may be configured (default 500Mi). Syntax: name:/container/path\[:sizeLimit\] |
| `hotReload`  
bool | Enable "hot reload" when a secret/configmap mounted is edited (default `false`). The configmap/secret must be marked with `camel.apache.org/integration` label to be taken in account. The resource will be watched for any kind change, also for changes in metadata. |
| `scanKameletsImplicitLabelSecrets`  
bool | Deprecated: no longer available since version 2.5. |

### OpenAPITrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

> **Warning**
> The OpenAPI trait was deprecated in version 2.5.0 and is no longer active since version 2.9.0.

The OpenAPI DSL trait is internally used to allow creating integrations from a OpenAPI specs.

> **Warning**
> The Openapi trait is **deprecated** and will removed in future release versions: use Camel REST contract first instead (see Camel core documentation).

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `configmaps`  
\[\]string | The configmaps holding the spec of the OpenAPI (compatible with > 3.0 spec only). |

### OwnerTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Owner trait ensures that all created resources belong to the integration being created and transfers annotations and labels on the integration onto these owned resources.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `targetAnnotations`  
\[\]string | The set of annotations to be transferred. Use "\*" to transfer all annotations. |
| `targetLabels`  
\[\]string | The set of labels to be transferred. Use "\*" to transfer all labels. |

### PDBTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The PDB trait allows to configure the PodDisruptionBudget resource for the Integration pods.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `minAvailable`  
string | The number of pods for the Integration that must still be available after an eviction. It can be either an absolute number or a percentage. Only one of `min-available` and `max-unavailable` can be specified. |
| `maxUnavailable`  
string | The number of pods for the Integration that can be unavailable after an eviction. It can be either an absolute number or a percentage (default `1` if `min-available` is also not set). Only one of `max-unavailable` and `min-available` can be specified. |

### PlatformBaseTrait

**Appears on:**

-   [BuilderTrait](#_camel_apache_org_v1_trait_BuilderTrait)
    
-   [CamelTrait](#_camel_apache_org_v1_trait_CamelTrait)
    
-   [ContainerTrait](#_camel_apache_org_v1_trait_ContainerTrait)
    
-   [DependenciesTrait](#_camel_apache_org_v1_trait_DependenciesTrait)
    
-   [DeployerTrait](#_camel_apache_org_v1_trait_DeployerTrait)
    
-   [DeploymentTrait](#_camel_apache_org_v1_trait_DeploymentTrait)
    
-   [EnvironmentTrait](#_camel_apache_org_v1_trait_EnvironmentTrait)
    
-   [ErrorHandlerTrait](#_camel_apache_org_v1_trait_ErrorHandlerTrait)
    
-   [MountTrait](#_camel_apache_org_v1_trait_MountTrait)
    
-   [OpenAPITrait](#_camel_apache_org_v1_trait_OpenAPITrait)
    
-   [PlatformTrait](#_camel_apache_org_v1_trait_PlatformTrait)
    
-   [PodTrait](#_camel_apache_org_v1_trait_PodTrait)
    
-   [QuarkusTrait](#_camel_apache_org_v1_trait_QuarkusTrait)
    
-   [SecurityContextTrait](#_camel_apache_org_v1_trait_SecurityContextTrait)
    

PlatformBaseTrait is the base type for platform traits. It cannot be disabled by the user.

 
| Field | Description |
| --- | --- |
| `enabled`  
bool | Deprecated: no longer in use. |
| `configuration`  
**[Configuration](#_camel_apache_org_v1_trait_Configuration)** | Legacy trait configuration parameters.
Deprecated: for backward compatibility.

 |

### PlatformTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The platform trait is a base trait that is used to assign an integration platform to an integration.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `createDefault`  
bool | Deprecated: no longer in use. |
| `global`  
bool | Deprecated: no longer in use. |
| `auto`  
bool | Deprecated: no longer in use. |

### PodTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The pod trait allows the customization of the Integration pods. It applies the `PodSpecTemplate` struct contained in the Integration `.spec.podTemplate` field, into the Integration deployment Pods template, using strategic merge patch.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |

### PrometheusTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

> **Warning**
> The Prometheus trait is **deprecated** and will removed in future release versions: use Camel Monitor operator ([https://camel-tooling.github.io/camel-dashboard/docs/installation-guide/advanced/operator/](https://camel-tooling.github.io/camel-dashboard/docs/installation-guide/advanced/operator/)) instead.

The Prometheus trait configures a Prometheus-compatible endpoint. It also creates a `PodMonitor` resource, so that the endpoint can be scraped automatically, when using the Prometheus operator.

The metrics are exposed using Micrometer Metrics.

> **Warning**
> The creation of the `PodMonitor` resource requires the [Prometheus Operator](https://github.com/coreos/prometheus-operator) custom resource definition to be installed. You can set `pod-monitor` to `false` for the Prometheus trait to work without the Prometheus Operator.

> **Warning**
> By default the metrics API is not available in JSON

The Prometheus trait is disabled by default.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `podMonitor`  
bool | Whether a `PodMonitor` resource is created (default `true`). |
| `podMonitorLabels`  
\[\]string | The `PodMonitor` resource labels, applicable when `pod-monitor` is `true`. |

### PullSecretTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Pull Secret trait sets a pull secret on the pod to allow Kubernetes to retrieve the container image from an external registry.

In a production environment it is highly advisable to provide such authentication and ensure the secret exists in the Integration namespace.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `secretName`  
string | The pull secret name to set on the Pod. |
| `imagePullerDelegation`  
bool | When using a global operator with a shared platform, this enables delegation of the `system:image-puller` cluster role on the operator namespace to the integration service account.
Deprecated: may be removed in future releases.

 |
| `auto`  
bool | Automatically configures the platform registry secret on the pod if it is of type `kubernetes.io/dockerconfigjson`. |

### QuarkusMode(`string` alias)

**Appears on:**

-   [QuarkusTrait](#_camel_apache_org_v1_trait_QuarkusTrait)
    

QuarkusMode is the type of Quarkus build packaging.

### QuarkusPackageType(`string` alias)

**Appears on:**

-   [QuarkusTrait](#_camel_apache_org_v1_trait_QuarkusTrait)
    

QuarkusPackageType is the type of Quarkus build packaging.

Deprecated: use `QuarkusMode` instead.

### QuarkusTrait

**Appears on:**

-   [IntegrationKitTraits](#_camel_apache_org_v1_IntegrationKitTraits)
    
-   [Traits](#_camel_apache_org_v1_Traits)
    

The Quarkus trait configures the Quarkus runtime.

It’s enabled by default.

> **Note**
> A native based compilation will be forced to use a `pod` build strategy. Compiling to a native executable, i.e. when using `build-mode=native`, requires at least 4GiB of memory, so the Pod running the native build, must have enough memory available.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `packageTypes`  
**[\[\]QuarkusPackageType](#_camel_apache_org_v1_trait_QuarkusPackageType)** | The Quarkus package types, `fast-jar` or `native` (default `fast-jar`). In case both `fast-jar` and `native` are specified, two `IntegrationKit` resources are created, with the native kit having precedence over the `fast-jar` one once ready. The order influences the resolution of the current kit for the integration. The kit corresponding to the first package type will be assigned to the integration in case no existing kit that matches the integration exists.
Deprecated: use `build-mode` instead.

 |
| `buildMode`  
**[\[\]QuarkusMode](#_camel_apache_org_v1_trait_QuarkusMode)** | The Quarkus mode to run: either `jvm` or `native` (default `jvm`). In case both `jvm` and `native` are specified, two `IntegrationKit` resources are created, with the `native` kit having precedence over the `jvm` one once ready. |
| `nativeBaseImage`  
string | The base image to use when running a native build (default `quay.io/quarkus/quarkus-micro-image:2.0`) |
| `nativeBuilderImage`  
string | The image containing the tooling required for a native build (by default it will use the one provided in the runtime catalog) |

### RawMessage(`[]byte` alias)

**Appears on:**

-   [Configuration](#_camel_apache_org_v1_trait_Configuration)
    

RawMessage defines a binary type for configuration

Deprecated: for backward compatibility.

### RegistryTrait

**Appears on:**

-   [IntegrationKitTraits](#_camel_apache_org_v1_IntegrationKitTraits)
    
-   [Traits](#_camel_apache_org_v1_Traits)
    

> **Warning**
> The Registry trait was deprecated in version 2.2.0 and is no longer active since version 2.5.0.

The Registry trait sets up Maven to use the Image registry as a Maven repository.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |

### RouteTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

> **Warning**
> The Route trait is **deprecated** and will removed in future release versions: use Ingress trait istead.

The Route trait can be used to configure the creation of OpenShift routes for the integration.

The certificate and key contents may be sourced either from the local filesystem or in a OpenShift `secret` object. The user may use the parameters ending in `-secret` (example: `tls-certificate-secret`) to reference a certificate stored in a `secret`. Parameters ending in `-secret` have higher priorities and in case the same route parameter is set, for example: `tls-key-secret` and `tls-key`, then `tls-key-secret` is used. The recommended approach to set the key and certificates is to use `secrets` to store their contents and use the following parameters to reference them: `tls-certificate-secret`, `tls-key-secret`, `tls-ca-certificate-secret`, `tls-destination-ca-certificate-secret` See the examples section at the end of this page to see the setup options.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `annotations`  
map\[string\]string | The annotations added to route. This can be used to set route specific annotations For annotations options see [https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html#route-specific-annotations](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html#route-specific-annotations) CLI usage example: -t "route.annotations.'haproxy.router.openshift.io/balance'=true" |
| `host`  
string | To configure the host exposed by the route. |
| `tlsTermination`  
string | The TLS termination type, like `edge`, `passthrough` or `reencrypt`.
Refer to the OpenShift route documentation for additional information.

 |
| `tlsCertificate`  
string | The TLS certificate contents.

Refer to the OpenShift route documentation for additional information.

 |
| `tlsCertificateSecret`  
string | The secret name and key reference to the TLS certificate. The format is "secret-name\[/key-name\]", the value represents the secret name, if there is only one key in the secret it will be read, otherwise you can set a key name separated with a "/".

Refer to the OpenShift route documentation for additional information.

 |
| `tlsKey`  
string | The TLS certificate key contents.

Refer to the OpenShift route documentation for additional information.

 |
| `tlsKeySecret`  
string | The secret name and key reference to the TLS certificate key. The format is "secret-name\[/key-name\]", the value represents the secret name, if there is only one key in the secret it will be read, otherwise you can set a key name separated with a "/".

Refer to the OpenShift route documentation for additional information.

 |
| `tlsCACertificate`  
string | The TLS CA certificate contents.

Refer to the OpenShift route documentation for additional information.

 |
| `tlsCACertificateSecret`  
string | The secret name and key reference to the TLS CA certificate. The format is "secret-name\[/key-name\]", the value represents the secret name, if there is only one key in the secret it will be read, otherwise you can set a key name separated with a "/".

Refer to the OpenShift route documentation for additional information.

 |
| `tlsDestinationCACertificate`  
string | The destination CA certificate provides the contents of the ca certificate of the final destination. When using reencrypt termination this file should be provided in order to have routers use it for health checks on the secure connection. If this field is not specified, the router may provide its own destination CA and perform hostname validation using the short service name (service.namespace.svc), which allows infrastructure generated certificates to automatically verify.

Refer to the OpenShift route documentation for additional information.

 |
| `tlsDestinationCACertificateSecret`  
string | The secret name and key reference to the destination CA certificate. The format is "secret-name\[/key-name\]", the value represents the secret name, if there is only one key in the secret it will be read, otherwise you can set a key name separated with a "/".

Refer to the OpenShift route documentation for additional information.

 |
| `tlsInsecureEdgeTerminationPolicy`  
string | To configure how to deal with insecure traffic, e.g. `Allow`, `Disable` or `Redirect` traffic.

Refer to the OpenShift route documentation for additional information.

 |

### SecurityContextTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Security Context trait can be used to configure the security setting of the Pod running the application.

 
| Field | Description |
| --- | --- |
| `PlatformBaseTrait`  
**[PlatformBaseTrait](#_camel_apache_org_v1_trait_PlatformBaseTrait)** | (Members of `PlatformBaseTrait` are embedded into this type.) |
| `runAsUser`  
int64 | Security Context RunAsUser configuration (default user 1000): this value is automatically retrieved in Openshift clusters when not explicitly set. |
| `runAsNonRoot`  
bool | Security Context RunAsNonRoot configuration (default true). |
| `seccompProfileType`  
**[Kubernetes core/v1.SeccompProfileType](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#seccompprofiletype-v1-core)** | Security Context SeccompProfileType configuration (default RuntimeDefault). |

### ServiceBindingTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Service Binding trait allows users to connect to Services in Kubernetes: [https://github.com/k8s-service-bindings/spec#service-binding](https://github.com/k8s-service-bindings/spec#service-binding) As the specification is still evolving this is subject to change.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `services`  
\[\]string | List of Services in the form \[\[apigroup/\]version:\]kind:\[namespace/\]name |

### ServiceTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Service trait exposes the Integration with a Service resource so that it can be accessed by other applications (or Integrations) in the same namespace.

> **Note**
> this trait is automatically disabled if the Knative Service trait is enabled.

It’s enabled by default if the integration depends on a Camel component that can expose a HTTP endpoint.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `auto`  
bool | To automatically detect from the code if a Service needs to be created. |
| `nodePort`  
bool | Enable Service to be exposed as NodePort (default `false`).
Deprecated: Use service type instead.

 |
| `type`  
**[ServiceType](#_camel_apache_org_v1_trait_ServiceType)** | The type of service to be used, either 'ClusterIP', 'NodePort' or 'LoadBalancer'. |
| `annotations`  
map\[string\]string | The annotations added to the Service object. |
| `labels`  
map\[string\]string | The labels added to the Service object. |
| `ports`  
\[\]string | List of container ports available in the container to expose (syntax: <port-name>;<port-number>;<container-port-number>\[;<port-protocol\]). When omitted, `port-protocol` (admitted values `TCP`, `UDP` or `SCTP`) is `TCP`. Don’t use this for the primary http managed port (which is managed by container trait). Don’t use in Knative based environments. |

### ServiceType(`string` alias)

**Appears on:**

-   [ServiceTrait](#_camel_apache_org_v1_trait_ServiceTrait)
    

### TelemetryTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

The Telemetry trait can be used to automatically publish tracing information to an OTLP compatible collector.

The trait is able to automatically discover the telemetry OTLP endpoint available in the namespace (supports **Jaerger** in version 1.35+).

The Telemetry trait is disabled by default.

> **Warning**
> The Telemetry trait is **deprecated** and will be removed in future release versions. The same behavior can be achieved via properties and dependencies configuration.

Migration example:

Before: --trait telemetry.endpoint=http://jaeger:4317
After:  -p quarkus.otel.exporter.otlp.traces.endpoint=http://jaeger:4317

> **Warning**
> The Telemetry trait can’t be enabled at the same time as the Tracing trait.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `auto`  
bool | Enables automatic configuration of the trait, including automatic discovery of the telemetry endpoint. |
| `serviceName`  
string | The name of the service that publishes telemetry data (defaults to the integration name) |
| `endpoint`  
string | The target endpoint of the Telemetry service (automatically discovered by default) |
| `sampler`  
string | The sampler of the telemetry used for tracing (default "on") |
| `sampler-ratio`  
string | The sampler ratio of the telemetry used for tracing |
| `sampler-parent-based`  
bool | The sampler of the telemetry used for tracing is parent based (default "true") |

### TolerationTrait

**Appears on:**

-   [Traits](#_camel_apache_org_v1_Traits)
    

This trait sets Tolerations over Integration pods. Tolerations allow (but do not require) the pods to schedule onto nodes with matching taints. See [https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for more details.

The toleration should be expressed in a similar manner that of taints, i.e., `Key[=Value]:Effect[:Seconds]`, where values in square brackets are optional.

For examples:

-   `node-role.kubernetes.io/master:NoSchedule`
    
-   `node.kubernetes.io/network-unavailable:NoExecute:3000`
    
-   `disktype=ssd:PreferNoSchedule`
    

It’s disabled by default.

 
| Field | Description |
| --- | --- |
| `Trait`  
**[Trait](#_camel_apache_org_v1_trait_Trait)** | (Members of `Trait` are embedded into this type.) |
| `taints`  
\[\]string | The list of taints to tolerate, in the form `Key[=Value]:Effect[:Seconds]` |

### Trait

**Appears on:**

-   [AffinityTrait](#_camel_apache_org_v1_trait_AffinityTrait)
    
-   [CronTrait](#_camel_apache_org_v1_trait_CronTrait)
    
-   [GCTrait](#_camel_apache_org_v1_trait_GCTrait)
    
-   [GatewayTrait](#_camel_apache_org_v1_trait_GatewayTrait)
    
-   [GitOpsTrait](#_camel_apache_org_v1_trait_GitOpsTrait)
    
-   [HealthTrait](#_camel_apache_org_v1_trait_HealthTrait)
    
-   [IngressTrait](#_camel_apache_org_v1_trait_IngressTrait)
    
-   [InitContainersTrait](#_camel_apache_org_v1_trait_InitContainersTrait)
    
-   [IstioTrait](#_camel_apache_org_v1_trait_IstioTrait)
    
-   [JVMTrait](#_camel_apache_org_v1_trait_JVMTrait)
    
-   [JolokiaTrait](#_camel_apache_org_v1_trait_JolokiaTrait)
    
-   [KameletsTrait](#_camel_apache_org_v1_trait_KameletsTrait)
    
-   [KedaTrait](#_camel_apache_org_v1_trait_KedaTrait)
    
-   [KnativeServiceTrait](#_camel_apache_org_v1_trait_KnativeServiceTrait)
    
-   [KnativeTrait](#_camel_apache_org_v1_trait_KnativeTrait)
    
-   [LoggingTrait](#_camel_apache_org_v1_trait_LoggingTrait)
    
-   [MasterTrait](#_camel_apache_org_v1_trait_MasterTrait)
    
-   [OwnerTrait](#_camel_apache_org_v1_trait_OwnerTrait)
    
-   [PDBTrait](#_camel_apache_org_v1_trait_PDBTrait)
    
-   [PrometheusTrait](#_camel_apache_org_v1_trait_PrometheusTrait)
    
-   [PullSecretTrait](#_camel_apache_org_v1_trait_PullSecretTrait)
    
-   [RegistryTrait](#_camel_apache_org_v1_trait_RegistryTrait)
    
-   [RouteTrait](#_camel_apache_org_v1_trait_RouteTrait)
    
-   [ServiceBindingTrait](#_camel_apache_org_v1_trait_ServiceBindingTrait)
    
-   [ServiceTrait](#_camel_apache_org_v1_trait_ServiceTrait)
    
-   [TelemetryTrait](#_camel_apache_org_v1_trait_TelemetryTrait)
    
-   [TolerationTrait](#_camel_apache_org_v1_trait_TolerationTrait)
    

Trait is the base type for all traits. It could be disabled by the user.

 
| Field | Description |
| --- | --- |
| `enabled`  
bool | Can be used to enable or disable a trait. All traits share this common property. |
| `configuration`  
**[Configuration](#_camel_apache_org_v1_trait_Configuration)** | Legacy trait configuration parameters.
Deprecated: for backward compatibility.

 |
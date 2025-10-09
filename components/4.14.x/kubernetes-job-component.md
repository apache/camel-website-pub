# Kubernetes Job

**Since Camel 2.23**

**Only producer is supported**

The Kubernetes Job component is one of [Kubernetes Components](kubernetes-summary.md) which provides a producer to execute kubernetes Job operations.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The Kubernetes Job component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **kubernetesClient** (producer) | **Autowired** To use an existing kubernetes client. |  | KubernetesClient |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Kubernetes Job endpoint is configured using URI syntax:

kubernetes-job:masterUrl

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **masterUrl** (producer) | **Required** URL to a remote Kubernetes API server. This should only be used when your Camel application is connecting from outside Kubernetes. If you run your Camel application inside Kubernetes, then you can use local or client as the URL to tell Camel to run in local mode. If you connect remotely to Kubernetes, then you may also need some of the many other configuration options for secured connection with certificates, etc. |  | String |

### Query Parameters (21 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiVersion** (producer) | The Kubernetes API Version to use. |  | String |
| **dnsDomain** (producer) | The dns domain, used for ServiceCall EIP. |  | String |
| **kubernetesClient** (producer) | Default KubernetesClient to use if provided. |  | KubernetesClient |
| **namespace** (producer) | The namespace. |  | String |
| **operation** (producer) | Producer operation to do on Kubernetes. |  | String |
| **portName** (producer) | The port name, used for ServiceCall EIP. |  | String |
| **portProtocol** (producer) | The port protocol, used for ServiceCall EIP. | tcp | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connectionTimeout** (advanced) | Connection timeout in milliseconds to use when making requests to the Kubernetes API server. |  | Integer |
| **caCertData** (security) | The CA Cert Data. |  | String |
| **caCertFile** (security) | The CA Cert File. |  | String |
| **clientCertData** (security) | The Client Cert Data. |  | String |
| **clientCertFile** (security) | The Client Cert File. |  | String |
| **clientKeyAlgo** (security) | The Key Algorithm used by the client. |  | String |
| **clientKeyData** (security) | The Client Key data. |  | String |
| **clientKeyFile** (security) | The Client Key file. |  | String |
| **clientKeyPassphrase** (security) | The Client Key Passphrase. |  | String |
| **oauthToken** (security) | The Auth Token. |  | String |
| **password** (security) | Password to connect to Kubernetes. |  | String |
| **trustCerts** (security) | Define if the certs we used are trusted anyway or not. | false | Boolean |
| **username** (security) | Username to connect to Kubernetes. |  | String |

## Message Headers

The Kubernetes Job component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelKubernetesOperation** (producer) Constant: [`KUBERNETES_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_OPERATION) | The Producer operation. |  | String |
| **CamelKubernetesNamespaceName** (producer) Constant: [`KUBERNETES_NAMESPACE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_NAMESPACE_NAME) | The namespace name. |  | String |
| **CamelKubernetesJobName** (producer) Constant: [`KUBERNETES_JOB_NAME`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_JOB_NAME) | The Job name. |  | String |
| **CamelKubernetesJobSpec** (producer) Constant: [`KUBERNETES_JOB_SPEC`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_JOB_SPEC) | The spec for a Job. |  | JobSpec |
| **CamelKubernetesJobLabels** (producer) Constant: [`KUBERNETES_JOB_LABELS`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_JOB_LABELS) | The Job labels. |  | Map |
| **CamelKubernetesJobAnnotations** (producer) Constant: [`KUBERNETES_JOB_ANNOTATIONS`](https://javadoc.io/doc/org.apache.camel/camel-kubernetes/latest/org/apache/camel/component/kubernetes/KubernetesConstants.html#KUBERNETES_JOB_ANNOTATIONS) | The Job annotations. |  | Map |

## Usage

### Supported producer operation

-   `listJob`
    
-   `listJobByLabels`
    
-   `getJob`
    
-   `createJob`
    
-   `updateJob`
    
-   `deleteJob`
    

## Examples

### Kubernetes Job Producer Examples

-   `listJob`: this operation lists the jobs on a kubernetes cluster
    

```java
from("direct:list").
    toF("kubernetes-job:///?kubernetesClient=#kubernetesClient&operation=listJob").
    to("mock:result");
```

This operation returns a list of jobs from your cluster

-   `listJobByLabels`: this operation lists the jobs by labels on a kubernetes cluster
    

```java
from("direct:listByLabels").process(new Processor() {
            @Override
            public void process(Exchange exchange) throws Exception {
                Map<String, String> labels = new HashMap<>();
                labels.put("key1", "value1");
                labels.put("key2", "value2");
                exchange.getIn().setHeader(KubernetesConstants.KUBERNETES_JOB_LABELS, labels);
            }
        });
    toF("kubernetes-job:///?kubernetesClient=#kubernetesClient&operation=listJobByLabels").
    to("mock:result");
```

This operation returns a list of jobs from your cluster, using a label selector (with key1 and key2, with value value1 and value2)

-   `createJob`: This operation creates a job on a Kubernetes Cluster
    

We have a wonderful example of this operation thanks to [Emmerson Miranda](https://github.com/Emmerson-Miranda) from this [Java test](https://github.com/Emmerson-Miranda/camel/blob/master/camel3-cdi/cdi-k8s-pocs/src/main/java/edu/emmerson/camel/k8s/jobs/camel_k8s_jobs/KubernetesCreateJob.java)

```java
import java.util.ArrayList;
import java.util.Date;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import javax.inject.Inject;

import org.apache.camel.Endpoint;
import org.apache.camel.builder.RouteBuilder;
import org.apache.camel.cdi.Uri;
import org.apache.camel.component.kubernetes.KubernetesConstants;
import org.apache.camel.component.kubernetes.KubernetesOperations;

import io.fabric8.kubernetes.api.model.Container;
import io.fabric8.kubernetes.api.model.ObjectMeta;
import io.fabric8.kubernetes.api.model.PodSpec;
import io.fabric8.kubernetes.api.model.PodTemplateSpec;
import io.fabric8.kubernetes.api.model.batch.JobSpec;

public class KubernetesCreateJob extends RouteBuilder {

    @Inject
    @Uri("timer:foo?delay=1000&repeatCount=1")
    private Endpoint inputEndpoint;

    @Inject
    @Uri("log:output")
    private Endpoint resultEndpoint;

    @Override
    public void configure() {
        // you can configure the route rule with Java DSL here

        from(inputEndpoint)
        	.routeId("kubernetes-jobcreate-client")
        	.process(exchange -> {
        		exchange.getIn().setHeader(KubernetesConstants.KUBERNETES_JOB_NAME, "camel-job"); //DNS-1123 subdomain must consist of lower case alphanumeric characters, '-' or '.', and must start and end with an alphanumeric character (e.g. 'example.com', regex used for validation is '[a-z0-9]([-a-z0-9]*[a-z0-9])?(\.[a-z0-9]([-a-z0-9]*[a-z0-9])?)*')
                exchange.getIn().setHeader(KubernetesConstants.KUBERNETES_NAMESPACE_NAME, "default");

                Map<String, String> joblabels = new HashMap<String, String>();
                joblabels.put("jobLabelKey1", "value1");
                joblabels.put("jobLabelKey2", "value2");
                joblabels.put("app", "jobFromCamelApp");
                exchange.getIn().setHeader(KubernetesConstants.KUBERNETES_JOB_LABELS, joblabels);

                exchange.getIn().setHeader(KubernetesConstants.KUBERNETES_JOB_SPEC, generateJobSpec());
        	})
        	.toF("kubernetes-job:///{{kubernetes-master-url}}?oauthToken={{kubernetes-oauth-token:}}&operation=" + KubernetesOperations.CREATE_JOB_OPERATION)
        	.log("Job created:")
        	.process(exchange -> {
        		System.out.println(exchange.getIn().getBody());
        	})
            .to(resultEndpoint);
    }

	private JobSpec generateJobSpec() {
		JobSpec js = new JobSpec();

		PodTemplateSpec pts = new PodTemplateSpec();

		PodSpec ps = new PodSpec();
		ps.setRestartPolicy("Never");
		ps.setContainers(generateContainers());
		pts.setSpec(ps);

		ObjectMeta metadata = new ObjectMeta();
		Map<String, String> annotations = new HashMap<String, String>();
		annotations.put("jobMetadataAnnotation1", "random value");
		metadata.setAnnotations(annotations);

		Map<String, String> podlabels = new HashMap<String, String>();
		podlabels.put("podLabelKey1", "value1");
		podlabels.put("podLabelKey2", "value2");
		podlabels.put("app", "podFromCamelApp");
		metadata.setLabels(podlabels);

		pts.setMetadata(metadata);
		js.setTemplate(pts);
		return js;
	}

	private List<Container> generateContainers() {
		Container container = new Container();
		container.setName("pi");
		container.setImage("perl");
		List<String> command = new ArrayList<String>();
		command.add("echo");
		command.add("Job created from Apache Camel code at " + (new Date()));
		container.setCommand(command);
		List<Container> containers = new ArrayList<Container>();
		containers.add(container);
		return containers;
	}
}
```

## Spring Boot Auto-Configuration

When using kubernetes-job with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-kubernetes-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 91 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.kubernetes-config-maps.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-config-maps.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-config-maps.enabled** | Whether to enable auto configuration of the kubernetes-config-maps component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-config-maps.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-config-maps.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-cronjob.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-cronjob.enabled** | Whether to enable auto configuration of the kubernetes-cronjob component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-cronjob.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-cronjob.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-custom-resources.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-custom-resources.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-custom-resources.enabled** | Whether to enable auto configuration of the kubernetes-custom-resources component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-custom-resources.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-custom-resources.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-deployments.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-deployments.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-deployments.enabled** | Whether to enable auto configuration of the kubernetes-deployments component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-deployments.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-deployments.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-events.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-events.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-events.enabled** | Whether to enable auto configuration of the kubernetes-events component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-events.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-events.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-hpa.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-hpa.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-hpa.enabled** | Whether to enable auto configuration of the kubernetes-hpa component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-hpa.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-hpa.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-job.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-job.enabled** | Whether to enable auto configuration of the kubernetes-job component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-job.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-job.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-namespaces.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-namespaces.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-namespaces.enabled** | Whether to enable auto configuration of the kubernetes-namespaces component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-namespaces.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-namespaces.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-nodes.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-nodes.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-nodes.enabled** | Whether to enable auto configuration of the kubernetes-nodes component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-nodes.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-nodes.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-persistent-volumes-claims.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-persistent-volumes-claims.enabled** | Whether to enable auto configuration of the kubernetes-persistent-volumes-claims component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-persistent-volumes-claims.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-persistent-volumes-claims.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-persistent-volumes.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-persistent-volumes.enabled** | Whether to enable auto configuration of the kubernetes-persistent-volumes component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-persistent-volumes.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-persistent-volumes.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-pods.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-pods.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-pods.enabled** | Whether to enable auto configuration of the kubernetes-pods component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-pods.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-pods.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-replication-controllers.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-replication-controllers.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-replication-controllers.enabled** | Whether to enable auto configuration of the kubernetes-replication-controllers component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-replication-controllers.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-replication-controllers.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-resources-quota.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-resources-quota.enabled** | Whether to enable auto configuration of the kubernetes-resources-quota component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-resources-quota.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-resources-quota.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-secrets.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-secrets.enabled** | Whether to enable auto configuration of the kubernetes-secrets component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-secrets.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-secrets.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-service-accounts.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-service-accounts.enabled** | Whether to enable auto configuration of the kubernetes-service-accounts component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-service-accounts.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-service-accounts.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kubernetes-services.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kubernetes-services.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kubernetes-services.enabled** | Whether to enable auto configuration of the kubernetes-services component. This is enabled by default. |  | Boolean |
| **camel.component.kubernetes-services.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.kubernetes-services.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openshift-build-configs.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openshift-build-configs.enabled** | Whether to enable auto configuration of the openshift-build-configs component. This is enabled by default. |  | Boolean |
| **camel.component.openshift-build-configs.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.openshift-build-configs.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openshift-builds.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openshift-builds.enabled** | Whether to enable auto configuration of the openshift-builds component. This is enabled by default. |  | Boolean |
| **camel.component.openshift-builds.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.openshift-builds.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openshift-deploymentconfigs.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openshift-deploymentconfigs.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.openshift-deploymentconfigs.enabled** | Whether to enable auto configuration of the openshift-deploymentconfigs component. This is enabled by default. |  | Boolean |
| **camel.component.openshift-deploymentconfigs.kubernetes-client** | To use an existing kubernetes client. The option is a io.fabric8.kubernetes.client.KubernetesClient type. |  | KubernetesClient |
| **camel.component.openshift-deploymentconfigs.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
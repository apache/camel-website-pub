# Writing Components

Apache Camel is designed to make it very easy to drop in new components whether they be routing components, transformers, transports etc. The idea of a component is to be a factory and manager of [Endpoints](endpoint.md).

Here are the main steps to add a new component:

-   Write a POJO which implements the `Component` interface. The simplest approach is just to derive from `DefaultComponent`.
    
-   To support auto-discovery of your component, add a file of `META-INF/services/org/apache/camel/component/FOO` where FOO is the URI scheme for your component and any related endpoints created on the fly. This file should contain the information of the component class full name. For example if your component is implemented by the `com.example.CustomComponent` class, the file should contain the following line — `class=com.example.CustomComponent`.
    

Users can then either explicitly create your component, configure it and register it with a `CamelContext` or they can use a URI which auto-creates your component.

> **Note**
> It is recommended to bootstrap your initial component using [Camel Maven Archetypes](camel-maven-archetypes.md), as it will give you all the necessary bits to start developing your component with ease. You will need as well to make sure to have [Camel Component Maven Plugin](camel-component-maven-plugin.md) included in your component’s `pom.xml` file, order to generate all the necessary metadata and Java files for your component.

## Writing Endpoints

When implementing an [Endpoint](endpoint.md) you typically may implement one or more of the following methods:

-   `createProducer` will create a producer for sending message exchanges to the endpoint
    
-   `createConsumer` implements the [Event Driven Consumer](../components/4.18.x/eips/eventDrivenConsumer-eip.md) pattern for consuming message exchanges from the endpoint.
    

Typically, you just derive from `DefaultEndpoint`

## Annotating your Endpoint

If you want to benefit from the automatic generation of metadata documentation for all the parameters on your endpoint as part of you need to[annotate your Endpoint’s parameters](endpoint-annotations.md). This metadata allows tooling such as IDE plugins, JBang and others to better understand your custom component and provide code assistance.

So this means you add a `@UriEndpoint` annotation to your Endpoint class and then annotate each parameter you wish to be configured via the URI configuration mechanism with `@UriParam` (or `@UriParams` for nested configuration objects).

Refer to the [Endpoint Annotations guide for details](endpoint-annotations.md).

## Options

If your component has options you can let it have public getters/setters and Camel will automatically set the properties when the endpoint is created.

If you however want to take the matter in your own hands, then you must remove the option from the given parameter list as Camel will validate that all options are used. If not Camel will throw a `ResolveEndpointFailedException` stating which options are unknown.

The parameters are provided by Camel in the `createEndpoint` method from `DefaultComponent` class:

```java
protected abstract Endpoint<E> createEndpoint(String uri, String remaining, Map parameters)
```

The code is an example from the [SEDA](../components/4.18.x/seda-component.md) component that removes the size parameter:

```java
    public BlockingQueue<Exchange> createQueue(String uri, Map parameters) {
        int size = 1000;
        Object value = parameters.remove("size");
        if (value != null) {
            Integer i = convertTo(Integer.class, value);
            if (i != null) {
                size = i;
            }
        }
        return new LinkedBlockingQueue<Exchange>(size);
    }
```

> **Tip**
> To learn how to build a custom component its recommended to take a look at any of the existing components from the source code. For a beginner component then look at the log or timer component.
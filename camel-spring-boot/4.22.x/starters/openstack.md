# OpenStack Cinder

Access data in OpenStack Cinder block storage.

## What’s inside

-   [OpenStack Cinder component](../../../components/4.22.x/openstack-cinder-component.md), URI syntax: `openstack-cinder:host`
    
-   [OpenStack Glance component](../../../components/4.22.x/openstack-glance-component.md), URI syntax: `openstack-glance:host`
    
-   [OpenStack Keystone component](../../../components/4.22.x/openstack-keystone-component.md), URI syntax: `openstack-keystone:host`
    
-   [OpenStack Neutron component](../../../components/4.22.x/openstack-neutron-component.md), URI syntax: `openstack-neutron:host`
    
-   [OpenStack Nova component](../../../components/4.22.x/openstack-nova-component.md), URI syntax: `openstack-nova:host`
    
-   [OpenStack Swift component](../../../components/4.22.x/openstack-swift-component.md), URI syntax: `openstack-swift:host`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-openstack-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 18 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.component.openstack-cinder.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.openstack-cinder.enabled | Whether to enable auto configuration of the openstack-cinder component. This is enabled by default. |  | Boolean |
| camel.component.openstack-cinder.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.openstack-glance.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.openstack-glance.enabled | Whether to enable auto configuration of the openstack-glance component. This is enabled by default. |  | Boolean |
| camel.component.openstack-glance.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.openstack-keystone.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.openstack-keystone.enabled | Whether to enable auto configuration of the openstack-keystone component. This is enabled by default. |  | Boolean |
| camel.component.openstack-keystone.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.openstack-neutron.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.openstack-neutron.enabled | Whether to enable auto configuration of the openstack-neutron component. This is enabled by default. |  | Boolean |
| camel.component.openstack-neutron.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.openstack-nova.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.openstack-nova.enabled | Whether to enable auto configuration of the openstack-nova component. This is enabled by default. |  | Boolean |
| camel.component.openstack-nova.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.openstack-swift.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.openstack-swift.enabled | Whether to enable auto configuration of the openstack-swift component. This is enabled by default. |  | Boolean |
| camel.component.openstack-swift.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
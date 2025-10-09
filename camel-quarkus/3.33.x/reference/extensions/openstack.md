# OpenStack

JVM since1.0.0 Native since2.0.0

Interact with OpenStack APIs

## What’s inside

-   [OpenStack Cinder component](../../../../components/4.18.x/openstack-cinder-component.md), URI syntax: `openstack-cinder:host`
    
-   [OpenStack Glance component](../../../../components/4.18.x/openstack-glance-component.md), URI syntax: `openstack-glance:host`
    
-   [OpenStack Keystone component](../../../../components/4.18.x/openstack-keystone-component.md), URI syntax: `openstack-keystone:host`
    
-   [OpenStack Neutron component](../../../../components/4.18.x/openstack-neutron-component.md), URI syntax: `openstack-neutron:host`
    
-   [OpenStack Nova component](../../../../components/4.18.x/openstack-nova-component.md), URI syntax: `openstack-nova:host`
    
-   [OpenStack Swift component](../../../../components/4.18.x/openstack-swift-component.md), URI syntax: `openstack-swift:host`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-openstack)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-openstack</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).
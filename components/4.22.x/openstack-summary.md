# OpenStack

**Since Camel 2.19**

The OpenStack component is a component for managing your [OpenStack](https://www.openstack.org//) applications.

## OpenStack components

See the following for usage of each component:

[OpenStack Cinder](openstack-cinder-component.md)

Access data in OpenStack Cinder block storage.

[OpenStack Glance](openstack-glance-component.md)

Manage VM images and metadata definitions in OpenStack Glance.

[OpenStack Keystone](openstack-keystone-component.md)

Access OpenStack Keystone for API client authentication, service discovery and distributed multi-tenant authorization.

[OpenStack Neutron](openstack-neutron-component.md)

Access OpenStack Neutron for network services.

[OpenStack Nova](openstack-nova-component.md)

Access OpenStack to manage compute resources.

[OpenStack Swift](openstack-swift-component.md)

Access OpenStack Swift object/blob store.

## Installation

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-openstack</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```
# Undertow Spring Security

**Since Camel 3.3**

**OSGi is not supported**

The Spring Security Provider provides Spring Security (5.x) token bearer security over camel-undertow component. To force camel-undertow to use spring security provider:

-   Add spring security provider library on classpath.
    
-   Provide instance of SpringSecurityConfiguration as `securityConfiguration` parameter into camel-undertow component or provide both `securityConfiguration` and `securityProvider` into camel-undertow component.
    
-   Configure spring-security.
    

Configuration has to provide following security attribute:

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top">Name</td><td class="tableblock halign-left valign-top">Description</td><td class="tableblock halign-left valign-top">Type</td></tr><tr><td class="tableblock halign-left valign-top"><strong>securityFiler</strong></td><td class="tableblock halign-left valign-top">Provides security filter gained from configured spring security (5.x). Filter could be obtained for example from DelegatingFilterProxyRegistrationBean.</td><td class="tableblock halign-left valign-top">Filter</td></tr></tbody></table>

Each exchange created by Undertow endpoint with spring security contains header 'SpringSecurityProvider\_principal' ( name of header is provided as a constant `SpringSecurityProvider.PRINCIPAL_NAME_HEADER`) with current authorized identity as value or header is not present in case of rejected requests.

## Spring Boot Auto-Configuration

When using undertow-spring-security with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-undertow-spring-security-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.security.undertow.keycloak** | Properties defined for keycloak provider. Value is gathered together from properties with prefix "camel.component.undertow.spring.security.keycloak". |  | KeycloakProviderConfiguration |
| **camel.security.undertow.keycloak.client-id** | Client id from the Keycloak server used for authentication. |  | String |
| **camel.security.undertow.keycloak.realm-id** | Realm id from the keycloak server used for authentication. |  | String |
| **camel.security.undertow.keycloak.url** | Url to keycloak server which will be used in spring security configuration. (Example "http://localhost:8080"). |  | String |
| **camel.security.undertow.keycloak.user-name-attribute** | Name of the attribute, which will be used as username. | preferred\_username | String |
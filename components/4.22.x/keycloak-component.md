# Keycloak

**Since Camel 4.15**

**Both producer and consumer are supported**

The Keycloak component supports running operations on Keycloak instance and policy enforcements.

## Component Features

The Keycloak component provides three main functionalities:

1.  **[Producer Operations](others/keycloak-producer.md)** - Manage Keycloak instances via the Admin API (realms, users, roles, clients, groups, sessions, tokens, and more)
    
2.  **[Consumer Operations](others/keycloak-consumer.md)** - Poll and consume user events and admin events from Keycloak for monitoring, auditing, and event-driven workflows
    
3.  **[Security Policies](others/keycloak-security.md)** - Route-level authorization using Keycloak authentication and authorization services, including role-based access, permission-based access, and OAuth 2.0 token introspection
    

## URI Format

keycloak://label\[?options\]

You can append query options to the URI in the following format:

`?options=value&option2=value&…​`

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

The Keycloak component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accessToken** (common) | Pre-obtained access token for authentication. When provided, this token will be used directly instead of obtaining one through username/password or client credentials flow. |  | String |
| **authClient** (common) | Filter admin events by authentication client ID. |  | String |
| **authIpAddress** (common) | Filter admin events by authentication IP address. |  | String |
| **authRealm** (common) | Keycloak realm to authenticate against. If not specified, the realm parameter is used for authentication. This is useful when you want to authenticate against one realm (e.g., master) but perform operations on another realm. | master | String |
| **authRealmFilter** (common) | Filter admin events by authentication realm. |  | String |
| **authUser** (common) | Filter admin events by authentication user ID. |  | String |
| **client** (common) | Filter events by client ID. |  | String |
| **clientId** (common) | Keycloak client ID. |  | String |
| **clientSecret** (common) | Keycloak client secret. |  | String |
| **configuration** (common) | Component configuration. |  | KeycloakConfiguration |
| **dateFrom** (common) | Filter events by start date/time in milliseconds since epoch. |  | String |
| **dateTo** (common) | Filter events by end date/time in milliseconds since epoch. |  | String |
| **eventType** (common) | Type of events to consume: events or admin-events. | events | String |
| **first** (common) | Offset for pagination (first result index). | 0 | int |
| **introspectionCacheEnabled** (common) | Enable caching of token introspection results to reduce API calls to Keycloak. | true | boolean |
| **introspectionCacheTtl** (common) | Time-to-live for cached introspection results in seconds. | 60 | long |
| **ipAddress** (common) | Filter events by IP address. |  | String |
| **keycloakClient** (common) | **Autowired** To use an existing configured Keycloak admin client. |  | Keycloak |
| **maxResults** (common) | Maximum number of events to retrieve per poll. | 100 | int |
| **operation** (common) | 
The operation to perform.

Enum values:

-   createRealm
    
-   deleteRealm
    
-   getRealm
    
-   updateRealm
    
-   createUser
    
-   deleteUser
    
-   getUser
    
-   updateUser
    
-   listUsers
    
-   searchUsers
    
-   createRole
    
-   deleteRole
    
-   getRole
    
-   updateRole
    
-   listRoles
    
-   assignRoleToUser
    
-   removeRoleFromUser
    
-   getUserRoles
    
-   createGroup
    
-   deleteGroup
    
-   getGroup
    
-   updateGroup
    
-   listGroups
    
-   addUserToGroup
    
-   removeUserFromGroup
    
-   listUserGroups
    
-   createClient
    
-   deleteClient
    
-   getClient
    
-   updateClient
    
-   listClients
    
-   resetUserPassword
    
-   createClientRole
    
-   deleteClientRole
    
-   getClientRole
    
-   updateClientRole
    
-   listClientRoles
    
-   assignClientRoleToUser
    
-   removeClientRoleFromUser
    
-   listUserSessions
    
-   logoutUser
    
-   logoutAllUsers
    
-   revokeAccessToken
    
-   revokeRefreshToken
    
-   introspectToken
    
-   pushNotBefore
    
-   createClientScope
    
-   deleteClientScope
    
-   getClientScope
    
-   updateClientScope
    
-   listClientScopes
    
-   createIdentityProvider
    
-   deleteIdentityProvider
    
-   getIdentityProvider
    
-   updateIdentityProvider
    
-   listIdentityProviders
    
-   createResource
    
-   deleteResource
    
-   getResource
    
-   updateResource
    
-   listResources
    
-   createResourcePolicy
    
-   deleteResourcePolicy
    
-   getResourcePolicy
    
-   updateResourcePolicy
    
-   listResourcePolicies
    
-   createResourcePermission
    
-   deleteResourcePermission
    
-   getResourcePermission
    
-   updateResourcePermission
    
-   listResourcePermissions
    
-   evaluatePermission
    
-   getUserAttributes
    
-   setUserAttribute
    
-   deleteUserAttribute
    
-   getUserCredentials
    
-   deleteUserCredential
    
-   sendVerifyEmail
    
-   sendPasswordResetEmail
    
-   addRequiredAction
    
-   removeRequiredAction
    
-   executeActionsEmail
    
-   getClientSecret
    
-   regenerateClientSecret
    
-   bulkCreateUsers
    
-   bulkDeleteUsers
    
-   bulkAssignRolesToUser
    
-   bulkAssignRoleToUsers
    
-   bulkUpdateUsers
    
-   createOrganization
    
-   updateOrganization
    
-   deleteOrganization
    
-   getOrganization
    
-   listOrganizations
    
-   searchOrganizations
    
-   addOrganizationMember
    
-   removeOrganizationMember
    
-   listOrganizationMembers
    
-   linkOrganizationIdentityProvider
    
-   unlinkOrganizationIdentityProvider
    
-   listOrganizationIdentityProviders
    
-   addFederatedIdentity
    
-   removeFederatedIdentity
    
-   getFederatedIdentities
    





 |  | KeycloakOperations |
| **operationTypes** (common) | Filter admin events by operation types (comma-separated list, e.g., CREATE,UPDATE,DELETE). |  | String |
| **password** (common) | Keycloak password. |  | String |
| **pojoRequest** (common) | If we want to use a POJO request as body or not. | false | boolean |
| **realm** (common) | Keycloak realm, the default is master because usually all the operations are done starting from the master realm. | master | String |
| **resourcePath** (common) | Filter admin events by resource path. |  | String |
| **serverUrl** (common) | Keycloak server URL. |  | String |
| **types** (common) | Filter events by event types (comma-separated list, e.g., LOGIN,LOGOUT). |  | String |
| **user** (common) | Filter events by user ID. |  | String |
| **username** (common) | Keycloak username. |  | String |
| **useTokenIntrospection** (common) | Enable OAuth 2.0 token introspection for real-time token validation. When enabled, tokens are validated by calling Keycloak’s introspection endpoint instead of local JWT parsing. This allows detecting revoked tokens before expiration. | false | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Keycloak endpoint is configured using URI syntax:

keycloak:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (common) | **Required** Logical name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accessToken** (common) | Pre-obtained access token for authentication. When provided, this token will be used directly instead of obtaining one through username/password or client credentials flow. |  | String |
| **authClient** (common) | Filter admin events by authentication client ID. |  | String |
| **authIpAddress** (common) | Filter admin events by authentication IP address. |  | String |
| **authRealm** (common) | Keycloak realm to authenticate against. If not specified, the realm parameter is used for authentication. This is useful when you want to authenticate against one realm (e.g., master) but perform operations on another realm. | master | String |
| **authRealmFilter** (common) | Filter admin events by authentication realm. |  | String |
| **authUser** (common) | Filter admin events by authentication user ID. |  | String |
| **client** (common) | Filter events by client ID. |  | String |
| **clientId** (common) | Keycloak client ID. |  | String |
| **clientSecret** (common) | Keycloak client secret. |  | String |
| **dateFrom** (common) | Filter events by start date/time in milliseconds since epoch. |  | String |
| **dateTo** (common) | Filter events by end date/time in milliseconds since epoch. |  | String |
| **eventType** (common) | Type of events to consume: events or admin-events. | events | String |
| **first** (common) | Offset for pagination (first result index). | 0 | int |
| **introspectionCacheEnabled** (common) | Enable caching of token introspection results to reduce API calls to Keycloak. | true | boolean |
| **introspectionCacheTtl** (common) | Time-to-live for cached introspection results in seconds. | 60 | long |
| **ipAddress** (common) | Filter events by IP address. |  | String |
| **keycloakClient** (common) | **Autowired** To use an existing configured Keycloak admin client. |  | Keycloak |
| **maxResults** (common) | Maximum number of events to retrieve per poll. | 100 | int |
| **operation** (common) | 
The operation to perform.

Enum values:

-   createRealm
    
-   deleteRealm
    
-   getRealm
    
-   updateRealm
    
-   createUser
    
-   deleteUser
    
-   getUser
    
-   updateUser
    
-   listUsers
    
-   searchUsers
    
-   createRole
    
-   deleteRole
    
-   getRole
    
-   updateRole
    
-   listRoles
    
-   assignRoleToUser
    
-   removeRoleFromUser
    
-   getUserRoles
    
-   createGroup
    
-   deleteGroup
    
-   getGroup
    
-   updateGroup
    
-   listGroups
    
-   addUserToGroup
    
-   removeUserFromGroup
    
-   listUserGroups
    
-   createClient
    
-   deleteClient
    
-   getClient
    
-   updateClient
    
-   listClients
    
-   resetUserPassword
    
-   createClientRole
    
-   deleteClientRole
    
-   getClientRole
    
-   updateClientRole
    
-   listClientRoles
    
-   assignClientRoleToUser
    
-   removeClientRoleFromUser
    
-   listUserSessions
    
-   logoutUser
    
-   logoutAllUsers
    
-   revokeAccessToken
    
-   revokeRefreshToken
    
-   introspectToken
    
-   pushNotBefore
    
-   createClientScope
    
-   deleteClientScope
    
-   getClientScope
    
-   updateClientScope
    
-   listClientScopes
    
-   createIdentityProvider
    
-   deleteIdentityProvider
    
-   getIdentityProvider
    
-   updateIdentityProvider
    
-   listIdentityProviders
    
-   createResource
    
-   deleteResource
    
-   getResource
    
-   updateResource
    
-   listResources
    
-   createResourcePolicy
    
-   deleteResourcePolicy
    
-   getResourcePolicy
    
-   updateResourcePolicy
    
-   listResourcePolicies
    
-   createResourcePermission
    
-   deleteResourcePermission
    
-   getResourcePermission
    
-   updateResourcePermission
    
-   listResourcePermissions
    
-   evaluatePermission
    
-   getUserAttributes
    
-   setUserAttribute
    
-   deleteUserAttribute
    
-   getUserCredentials
    
-   deleteUserCredential
    
-   sendVerifyEmail
    
-   sendPasswordResetEmail
    
-   addRequiredAction
    
-   removeRequiredAction
    
-   executeActionsEmail
    
-   getClientSecret
    
-   regenerateClientSecret
    
-   bulkCreateUsers
    
-   bulkDeleteUsers
    
-   bulkAssignRolesToUser
    
-   bulkAssignRoleToUsers
    
-   bulkUpdateUsers
    
-   createOrganization
    
-   updateOrganization
    
-   deleteOrganization
    
-   getOrganization
    
-   listOrganizations
    
-   searchOrganizations
    
-   addOrganizationMember
    
-   removeOrganizationMember
    
-   listOrganizationMembers
    
-   linkOrganizationIdentityProvider
    
-   unlinkOrganizationIdentityProvider
    
-   listOrganizationIdentityProviders
    
-   addFederatedIdentity
    
-   removeFederatedIdentity
    
-   getFederatedIdentities
    





 |  | KeycloakOperations |
| **operationTypes** (common) | Filter admin events by operation types (comma-separated list, e.g., CREATE,UPDATE,DELETE). |  | String |
| **password** (common) | Keycloak password. |  | String |
| **pojoRequest** (common) | If we want to use a POJO request as body or not. | false | boolean |
| **realm** (common) | Keycloak realm, the default is master because usually all the operations are done starting from the master realm. | master | String |
| **resourcePath** (common) | Filter admin events by resource path. |  | String |
| **serverUrl** (common) | Keycloak server URL. |  | String |
| **types** (common) | Filter events by event types (comma-separated list, e.g., LOGIN,LOGOUT). |  | String |
| **user** (common) | Filter events by user ID. |  | String |
| **username** (common) | Keycloak username. |  | String |
| **useTokenIntrospection** (common) | Enable OAuth 2.0 token introspection for real-time token validation. When enabled, tokens are validated by calling Keycloak’s introspection endpoint instead of local JWT parsing. This allows detecting revoked tokens before expiration. | false | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |

## Message Headers

The Keycloak component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelKeycloakOperation** (common) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   createRealm
    
-   deleteRealm
    
-   getRealm
    
-   updateRealm
    
-   createUser
    
-   deleteUser
    
-   getUser
    
-   updateUser
    
-   listUsers
    
-   searchUsers
    
-   createRole
    
-   deleteRole
    
-   getRole
    
-   updateRole
    
-   listRoles
    
-   assignRoleToUser
    
-   removeRoleFromUser
    
-   getUserRoles
    
-   createGroup
    
-   deleteGroup
    
-   getGroup
    
-   updateGroup
    
-   listGroups
    
-   addUserToGroup
    
-   removeUserFromGroup
    
-   listUserGroups
    
-   createClient
    
-   deleteClient
    
-   getClient
    
-   updateClient
    
-   listClients
    
-   resetUserPassword
    
-   createClientRole
    
-   deleteClientRole
    
-   getClientRole
    
-   updateClientRole
    
-   listClientRoles
    
-   assignClientRoleToUser
    
-   removeClientRoleFromUser
    
-   listUserSessions
    
-   logoutUser
    
-   logoutAllUsers
    
-   revokeAccessToken
    
-   revokeRefreshToken
    
-   introspectToken
    
-   pushNotBefore
    
-   createClientScope
    
-   deleteClientScope
    
-   getClientScope
    
-   updateClientScope
    
-   listClientScopes
    
-   createIdentityProvider
    
-   deleteIdentityProvider
    
-   getIdentityProvider
    
-   updateIdentityProvider
    
-   listIdentityProviders
    
-   createResource
    
-   deleteResource
    
-   getResource
    
-   updateResource
    
-   listResources
    
-   createResourcePolicy
    
-   deleteResourcePolicy
    
-   getResourcePolicy
    
-   updateResourcePolicy
    
-   listResourcePolicies
    
-   createResourcePermission
    
-   deleteResourcePermission
    
-   getResourcePermission
    
-   updateResourcePermission
    
-   listResourcePermissions
    
-   evaluatePermission
    
-   getUserAttributes
    
-   setUserAttribute
    
-   deleteUserAttribute
    
-   getUserCredentials
    
-   deleteUserCredential
    
-   sendVerifyEmail
    
-   sendPasswordResetEmail
    
-   addRequiredAction
    
-   removeRequiredAction
    
-   executeActionsEmail
    
-   getClientSecret
    
-   regenerateClientSecret
    
-   bulkCreateUsers
    
-   bulkDeleteUsers
    
-   bulkAssignRolesToUser
    
-   bulkAssignRoleToUsers
    
-   bulkUpdateUsers
    
-   createOrganization
    
-   updateOrganization
    
-   deleteOrganization
    
-   getOrganization
    
-   listOrganizations
    
-   searchOrganizations
    
-   addOrganizationMember
    
-   removeOrganizationMember
    
-   listOrganizationMembers
    
-   linkOrganizationIdentityProvider
    
-   unlinkOrganizationIdentityProvider
    
-   listOrganizationIdentityProviders
    
-   addFederatedIdentity
    
-   removeFederatedIdentity
    
-   getFederatedIdentities
    





 |  | KeycloakOperations |
| **CamelKeycloakRealmName** (common) Constant: [`REALM_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#REALM_NAME) | The realm name. |  | String |
| **CamelKeycloakUserId** (common) Constant: [`USER_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#USER_ID) | The user ID. |  | String |
| **CamelKeycloakUsername** (common) Constant: [`USERNAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#USERNAME) | The username. |  | String |
| **CamelKeycloakUserEmail** (common) Constant: [`USER_EMAIL`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#USER_EMAIL) | The user email. |  | String |
| **CamelKeycloakUserFirstName** (common) Constant: [`USER_FIRST_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#USER_FIRST_NAME) | The user first name. |  | String |
| **CamelKeycloakUserLastName** (common) Constant: [`USER_LAST_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#USER_LAST_NAME) | The user last name. |  | String |
| **CamelKeycloakRoleId** (common) Constant: [`ROLE_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ROLE_ID) | The role ID. |  | String |
| **CamelKeycloakRoleName** (common) Constant: [`ROLE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ROLE_NAME) | The role name. |  | String |
| **CamelKeycloakRoleDescription** (common) Constant: [`ROLE_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ROLE_DESCRIPTION) | The role description. |  | String |
| **CamelKeycloakGroupId** (common) Constant: [`GROUP_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#GROUP_ID) | The group ID. |  | String |
| **CamelKeycloakGroupName** (common) Constant: [`GROUP_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#GROUP_NAME) | The group name. |  | String |
| **CamelKeycloakClientId** (common) Constant: [`CLIENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#CLIENT_ID) | The client ID. |  | String |
| **CamelKeycloakClientUuid** (common) Constant: [`CLIENT_UUID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#CLIENT_UUID) | The client UUID. |  | String |
| **CamelKeycloakUserPassword** (common) Constant: [`USER_PASSWORD`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#USER_PASSWORD) | The user password. |  | String |
| **CamelKeycloakPasswordTemporary** (common) Constant: [`PASSWORD_TEMPORARY`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#PASSWORD_TEMPORARY) | Whether the password is temporary. |  | Boolean |
| **CamelKeycloakSearchQuery** (common) Constant: [`SEARCH_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#SEARCH_QUERY) | Search query string. |  | String |
| **CamelKeycloakMaxResults** (common) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#MAX_RESULTS) | Maximum number of results. |  | Integer |
| **CamelKeycloakFirstResult** (common) Constant: [`FIRST_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#FIRST_RESULT) | First result index. |  | Integer |
| **CamelKeycloakClientScopeId** (common) Constant: [`CLIENT_SCOPE_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#CLIENT_SCOPE_ID) | The client scope ID. |  | String |
| **CamelKeycloakClientScopeName** (common) Constant: [`CLIENT_SCOPE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#CLIENT_SCOPE_NAME) | The client scope name. |  | String |
| **CamelKeycloakEventType** (common) Constant: [`EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#EVENT_TYPE) | The event type (event or admin-event). |  | String |
| **CamelKeycloakEventId** (common) Constant: [`EVENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#EVENT_ID) | The event ID or timestamp. |  | Long |
| **CamelKeycloakIdpAlias** (common) Constant: [`IDP_ALIAS`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#IDP_ALIAS) | The identity provider alias. |  | String |
| **CamelKeycloakIdpId** (common) Constant: [`IDP_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#IDP_ID) | The identity provider ID. |  | String |
| **CamelKeycloakResourceId** (common) Constant: [`RESOURCE_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#RESOURCE_ID) | The resource ID. |  | String |
| **CamelKeycloakResourceName** (common) Constant: [`RESOURCE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#RESOURCE_NAME) | The resource name. |  | String |
| **CamelKeycloakResourceType** (common) Constant: [`RESOURCE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#RESOURCE_TYPE) | The resource type. |  | String |
| **CamelKeycloakResourceUri** (common) Constant: [`RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#RESOURCE_URI) | The resource URI. |  | String |
| **CamelKeycloakPolicyId** (common) Constant: [`POLICY_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#POLICY_ID) | The policy ID. |  | String |
| **CamelKeycloakPolicyName** (common) Constant: [`POLICY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#POLICY_NAME) | The policy name. |  | String |
| **CamelKeycloakPolicyType** (common) Constant: [`POLICY_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#POLICY_TYPE) | The policy type. |  | String |
| **CamelKeycloakPermissionId** (common) Constant: [`PERMISSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#PERMISSION_ID) | The permission ID. |  | String |
| **CamelKeycloakPermissionName** (common) Constant: [`PERMISSION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#PERMISSION_NAME) | The permission name. |  | String |
| **CamelKeycloakScopeName** (common) Constant: [`SCOPE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#SCOPE_NAME) | The scope name. |  | String |
| **CamelKeycloakAttributeName** (common) Constant: [`ATTRIBUTE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ATTRIBUTE_NAME) | The user attribute name. |  | String |
| **CamelKeycloakAttributeValue** (common) Constant: [`ATTRIBUTE_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ATTRIBUTE_VALUE) | The user attribute value. |  | String |
| **CamelKeycloakCredentialId** (common) Constant: [`CREDENTIAL_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#CREDENTIAL_ID) | The credential ID. |  | String |
| **CamelKeycloakCredentialType** (common) Constant: [`CREDENTIAL_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#CREDENTIAL_TYPE) | The credential type. |  | String |
| **CamelKeycloakRequiredAction** (common) Constant: [`REQUIRED_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#REQUIRED_ACTION) | The required action type. |  | String |
| **CamelKeycloakActions** (common) Constant: [`ACTIONS`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ACTIONS) | The list of actions to execute. |  | List |
| **CamelKeycloakRedirectUri** (common) Constant: [`REDIRECT_URI`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#REDIRECT_URI) | The redirect URI. |  | String |
| **CamelKeycloakLifespan** (common) Constant: [`LIFESPAN`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#LIFESPAN) | The lifespan in seconds. |  | Integer |
| **CamelKeycloakUsers** (common) Constant: [`USERS`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#USERS) | The list of users for bulk operations. |  | List |
| **CamelKeycloakUserIds** (common) Constant: [`USER_IDS`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#USER_IDS) | The list of user IDs for bulk operations. |  | List |
| **CamelKeycloakUsernames** (common) Constant: [`USERNAMES`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#USERNAMES) | The list of usernames for bulk operations. |  | List |
| **CamelKeycloakRoleNames** (common) Constant: [`ROLE_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ROLE_NAMES) | The list of role names for bulk operations. |  | List |
| **CamelKeycloakContinueOnError** (common) Constant: [`CONTINUE_ON_ERROR`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#CONTINUE_ON_ERROR) | Continue on error during bulk operations. |  | Boolean |
| **CamelKeycloakBatchSize** (common) Constant: [`BATCH_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#BATCH_SIZE) | Batch size for bulk operations. |  | Integer |
| **CamelKeycloakAccessToken** (common) Constant: [`ACCESS_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ACCESS_TOKEN) | The access token for permission evaluation. |  | String |
| **CamelKeycloakToken** (common) Constant: [`TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#TOKEN) | The token for revocation or introspection. |  | String |
| **CamelKeycloakTokenTypeHint** (common) Constant: [`TOKEN_TYPE_HINT`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#TOKEN_TYPE_HINT) | The token type hint for revocation. |  | String |
| **CamelKeycloakPermissionResourceNames** (common) Constant: [`PERMISSION_RESOURCE_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#PERMISSION_RESOURCE_NAMES) | Comma-separated list of resource names or IDs to evaluate permissions for. |  | String |
| **CamelKeycloakPermissionScopes** (common) Constant: [`PERMISSION_SCOPES`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#PERMISSION_SCOPES) | Comma-separated list of scopes to evaluate permissions for. |  | String |
| **CamelKeycloakSubjectToken** (common) Constant: [`SUBJECT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#SUBJECT_TOKEN) | Subject token for permission evaluation on behalf of a user. |  | String |
| **CamelKeycloakPermissionAudience** (common) Constant: [`PERMISSION_AUDIENCE`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#PERMISSION_AUDIENCE) | Audience for permission evaluation. |  | String |
| **CamelKeycloakPermissionsOnly** (common) Constant: [`PERMISSIONS_ONLY`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#PERMISSIONS_ONLY) | Whether to only return the list of permissions without obtaining an RPT. |  | Boolean |
| **CamelKeycloakOrganizationId** (common) Constant: [`ORGANIZATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ORGANIZATION_ID) | The organization ID. |  | String |
| **CamelKeycloakOrganizationName** (common) Constant: [`ORGANIZATION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ORGANIZATION_NAME) | The organization name. |  | String |
| **CamelKeycloakOrganizationAlias** (common) Constant: [`ORGANIZATION_ALIAS`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ORGANIZATION_ALIAS) | The organization alias. |  | String |
| **CamelKeycloakOrganizationDescription** (common) Constant: [`ORGANIZATION_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ORGANIZATION_DESCRIPTION) | The organization description. |  | String |
| **CamelKeycloakOrganizationRedirectUrl** (common) Constant: [`ORGANIZATION_REDIRECT_URL`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ORGANIZATION_REDIRECT_URL) | The organization redirect URL. |  | String |
| **CamelKeycloakOrganizationDomain** (common) Constant: [`ORGANIZATION_DOMAIN`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ORGANIZATION_DOMAIN) | The organization domain name. |  | String |
| **CamelKeycloakOrganizationSearch** (common) Constant: [`ORGANIZATION_SEARCH`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#ORGANIZATION_SEARCH) | Search query for organizations. |  | String |
| **CamelKeycloakIdentityProvider** (common) Constant: [`IDENTITY_PROVIDER`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#IDENTITY_PROVIDER) | The identity provider alias for a federated identity link. |  | String |
| **CamelKeycloakFederatedUserId** (common) Constant: [`FEDERATED_USER_ID`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#FEDERATED_USER_ID) | The user id at the external identity provider. |  | String |
| **CamelKeycloakFederatedUsername** (common) Constant: [`FEDERATED_USERNAME`](https://javadoc.io/doc/org.apache.camel/camel-keycloak/latest/org/apache/camel/component/keycloak/KeycloakConstants.html#FEDERATED_USERNAME) | The username at the external identity provider. |  | String |

## Overview

### Producer

The producer supports a comprehensive set of administrative operations on Keycloak via the Admin API, including user management, role management, client management, group management, session management, token management, identity providers, organizations, authorization services, and bulk operations.

See [Keycloak Producer Operations](others/keycloak-producer.md) for the full list of supported operations, configuration details, and examples.

### Consumer

The consumer allows you to poll Keycloak for user events (logins, logouts, registrations) and admin events (resource creates, updates, deletes). It supports filtering by event type, operation type, date range, user, client, and IP address, with built-in fingerprint-based deduplication.

See [Keycloak Consumer Operations](others/keycloak-consumer.md) for configuration, event processing patterns, and examples.

### Security Policies

The security policy provides route-level authorization by validating Keycloak access tokens. It supports role-based and permission-based authorization, local JWT parsing and OAuth 2.0 token introspection (RFC 7662) with pluggable cache implementations.

See [Keycloak Security Policies](others/keycloak-security.md) for configuration, token introspection setup, and examples.

## Usage

### Providing Access Tokens

The security policy expects access tokens to be provided in one of the following ways:

1.  **Header**: `CamelKeycloakAccessToken`
    
2.  **Authorization Header**: `Authorization: Bearer <token>`
    
3.  **Exchange Property**: `CamelKeycloakAccessToken`
    

_Java-only: accessing token from exchange_

```java
// Using header
template.sendBodyAndHeader("direct:protected", "message",
    "CamelKeycloakAccessToken", accessToken);

// Using Authorization header
template.sendBodyAndHeader("direct:protected", "message",
    "Authorization", "Bearer " + accessToken);
```

### Route Examples

-   Java
    
-   YAML
    

```java
from("direct:admin-only")
    .policy(adminPolicy)
    .transform().constant("Admin access granted")
    .to("mock:admin");

from("direct:user-or-admin")
    .policy(userPolicy)
    .transform().constant("User access granted")
    .to("mock:user");

from("rest:get:/api/documents")
    .policy(documentsPolicy)
    .to("direct:list-documents");
```

```yaml
- route:
    from:
      uri: direct:admin-only
      steps:
        - policy:
            ref: adminPolicy
        - transform:
            constant: "Admin access granted"
        - to:
            uri: mock:admin

- route:
    from:
      uri: direct:user-or-admin
      steps:
        - policy:
            ref: userPolicy
        - transform:
            constant: "User access granted"
        - to:
            uri: mock:user

- rest:
    get:
      - uri: /api/documents
        to: direct:list-documents
        route:
          policy:
            ref: documentsPolicy
```

### Federated Identity Operations

Federated identity operations manage the links between a Keycloak user and an external identity provider account (Google, GitHub, a SAML provider, and so on). They are useful for SSO scenarios and for provisioning users with pre-linked IdP accounts during a migration.

-   `addFederatedIdentity` — link a user to an identity provider account.
    
-   `removeFederatedIdentity` — unlink a user from an identity provider.
    
-   `getFederatedIdentities` — list all identity provider links for a user.
    

All three require `CamelKeycloakRealmName` and `CamelKeycloakUserId`. In addition:

-   `addFederatedIdentity` requires `CamelKeycloakIdentityProvider` (the IdP alias) and `CamelKeycloakFederatedUserId` (the user id at the provider). `CamelKeycloakFederatedUsername` is optional — when it is not supplied the external user id is used as the username.
    
-   `removeFederatedIdentity` requires `CamelKeycloakIdentityProvider`.
    

`getFederatedIdentities` sets the out-message body to the `List<FederatedIdentityRepresentation>` of links.

-   Java
    
-   YAML
    

```java
from("direct:linkAccount")
    .setHeader(KeycloakConstants.REALM_NAME, constant("myrealm"))
    .setHeader(KeycloakConstants.USER_ID, constant("user-uuid"))
    .setHeader(KeycloakConstants.IDENTITY_PROVIDER, constant("google"))
    .setHeader(KeycloakConstants.FEDERATED_USER_ID, constant("google-account-id"))
    .setHeader(KeycloakConstants.FEDERATED_USERNAME, constant("jane@example.com"))
    .to("keycloak:admin?operation=addFederatedIdentity");

from("direct:listLinks")
    .setHeader(KeycloakConstants.REALM_NAME, constant("myrealm"))
    .setHeader(KeycloakConstants.USER_ID, constant("user-uuid"))
    .to("keycloak:admin?operation=getFederatedIdentities");
```

```yaml
- route:
    from:
      uri: direct:linkAccount
      steps:
        - setHeader:
            name: CamelKeycloakRealmName
            constant: "myrealm"
        - setHeader:
            name: CamelKeycloakUserId
            constant: "user-uuid"
        - setHeader:
            name: CamelKeycloakIdentityProvider
            constant: "google"
        - setHeader:
            name: CamelKeycloakFederatedUserId
            constant: "google-account-id"
        - to:
            uri: keycloak:admin?operation=addFederatedIdentity
```

## Configuration Options

  
| Name | Default | Description |
| --- | --- | --- |
| serverUrl |  | Keycloak server URL (e.g., [http://localhost:8080](http://localhost:8080)) |
| realm |  | Keycloak realm name |
| clientId |  | Keycloak client ID |
| clientSecret |  | Keycloak client secret (for client credentials flow) |
| username |  | Username (for resource owner password flow) |
| password |  | Password (for resource owner password flow) |
| requiredRoles | "" | Comma-separated list of required roles (e.g., "admin,user,manager") |
| requiredPermissions | "" | Comma-separated list of required permissions (e.g., "read:documents,write:documents") |
| allRolesRequired | true | Whether ALL roles are required (true) or ANY role (false) |
| allPermissionsRequired | true | Whether ALL permissions are required (true) or ANY permission (false) |
| useResourceOwnerPasswordCredentials | false | Whether to use resource owner password flow |

## Security Considerations

-   Always use HTTPS in production environments
    
-   Store client secrets securely (environment variables, secret management systems)
    
-   Regularly rotate client secrets and user passwords
    
-   Use the principle of least privilege when assigning roles and permissions
    
-   Consider token expiration and refresh strategies
    

## Error Handling

The component throws `CamelAuthorizationException` when:

-   Access token is missing or invalid
    
-   User doesn’t have required roles
    
-   User doesn’t have required permissions
    
-   Keycloak server is unreachable
    
-   Token verification fails
    

-   Java
    
-   YAML
    

```java
onException(CamelAuthorizationException.class)
    .handled(true)
    .setHeader(Exchange.HTTP_RESPONSE_CODE, constant(403))
    .transform().constant("Access denied");
```

```yaml
- onException:
    exception:
      - "org.apache.camel.CamelAuthorizationException"
    handled: true
    steps:
      - setHeader:
          name: "CamelHttpResponseCode"
          constant: 403
      - transform:
          constant: "Access denied"
```

## Running Integration Tests

The component includes integration tests that require a running Keycloak instance. These tests are disabled by default and only run when specific system properties are provided.

The integration tests include comprehensive testing for: \* Role-based authorization with different role requirements \* Permission-based authorization using custom claims and scopes \* Public key verification with JWKS endpoint integration \* Combined roles and permissions validation \* Token parsing with and without public key verification \* Different authorization header formats (Bearer token, custom header) \* Token expiration and validity checks \* Error handling for invalid tokens and insufficient privileges

### Starting Keycloak with Docker

#### 1\. Start Keycloak Container

```bash
# Start Keycloak in development mode
docker run -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin \
  quay.io/keycloak/keycloak:latest start-dev
```

#### 2\. Access Keycloak Admin Console

Open your browser to [http://localhost:8080/admin](http://localhost:8080/admin) and login with: - Username: `admin` - Password: `admin`

### Keycloak Configuration for Integration Tests

#### 3\. Create Test Realm

1.  In the Keycloak Admin Console, click **"Add realm"**
    
2.  Set realm name to: `test-realm`
    
3.  Click **"Create"**
    

#### 4\. Create Test Client

1.  In the `test-realm`, go to **Clients** → **"Create client"**
    
2.  Set the following:
    
    -   Client type: `OpenID Connect`
        
    -   Client ID: `test-client`
        
    -   Next → Client authentication: `ON`
        
    -   Authorization: `ON` (optional, for advanced features)
        
    -   Next → Valid redirect URIs: `*`
        
    -   Click **"Save"**
        
    
3.  Go to **Credentials** tab and copy the **Client Secret**
    

#### 5\. Create Test Roles

1.  Go to **Realm roles** → **"Create role"**
    
2.  Create the following roles:
    
    -   `admin-role`
        
    -   `user`
        
    -   `reader`
        
    

#### 6\. Create Test Users

Create three test users with the following configuration:

**User 1: myuser** 1. Go to **Users** → **"Add user"** 2. Set: - Username: `myuser` - Email: `myuser@test.com` - First name: `My` - Last name: `User` - Click **"Create"** 3. Go to **Credentials** tab → **"Set password"** - Password: `pippo123` - Temporary: `OFF` 4. Go to **Role mapping** tab → **"Assign role"** - Assign role: `admin-role`

**User 2: test-user** 1. Create user with: - Username: `test-user` - Password: `user123` (temporary: OFF) - Assign role: `user`

**User 3: reader-user** 1. Create user with: - Username: `reader-user` - Password: `reader123` (temporary: OFF) - Assign role: `reader`

### Running the Integration Tests

#### 7\. Execute Tests with Maven

**Run All Integration Tests:**

```bash
# Run integration tests with required properties
mvn test -Dtest=KeycloakSecurityIT \
  -Dkeycloak.server.url=http://localhost:8080 \
  -Dkeycloak.realm=test-realm \
  -Dkeycloak.client.id=test-client \
  -Dkeycloak.client.secret=YOUR_CLIENT_SECRET
```

**Run Specific Test Categories:**

```bash
# Test only role-based authorization
mvn test -Dtest=KeycloakSecurityIT#testKeycloakSecurityPolicyWithValidAdminToken,testKeycloakSecurityPolicyWithValidUserToken,testKeycloakSecurityPolicyUserCannotAccessAdminRoute \
  -Dkeycloak.server.url=http://localhost:8080 \
  -Dkeycloak.realm=test-realm \
  -Dkeycloak.client.id=test-client \
  -Dkeycloak.client.secret=YOUR_CLIENT_SECRET

# Test only permissions-based authorization
mvn test -Dtest=KeycloakSecurityIT#testKeycloakSecurityPolicyWithPermissions,testKeycloakSecurityPolicyWithScopeBasedPermissions,testKeycloakSecurityPolicyWithCombinedRolesAndPermissions \
  -Dkeycloak.server.url=http://localhost:8080 \
  -Dkeycloak.realm=test-realm \
  -Dkeycloak.client.id=test-client \
  -Dkeycloak.client.secret=YOUR_CLIENT_SECRET

# Test only public key verification
mvn test -Dtest=KeycloakSecurityIT#testKeycloakSecurityPolicyWithPublicKeyVerification,testParseTokenDirectlyWithPublicKey \
  -Dkeycloak.server.url=http://localhost:8080 \
  -Dkeycloak.realm=test-realm \
  -Dkeycloak.client.id=test-client \
  -Dkeycloak.client.secret=YOUR_CLIENT_SECRET
```

Replace `YOUR_CLIENT_SECRET` with the actual client secret from step 4.

**Run Manual Producer Tests:**

The `KeycloakProducerIT` test contains manual integration tests for producer operations. These tests are disabled by default and require explicit activation:

```bash
# Run manual producer integration tests
mvn test -Dtest=KeycloakProducerIT \
  -Dmanual.keycloak.test=true \
  -Dkeycloak.server.url=http://localhost:8080 \
  -Dkeycloak.realm=master \
  -Dkeycloak.username=admin \
  -Dkeycloak.password=admin
```

> **Note**
> The `-Dmanual.keycloak.test=true` flag is required to run `KeycloakProducerIT` tests. Without this flag, the tests will be skipped even if other Keycloak properties are provided. This prevents the tests from accidentally running in automated CI environments.

#### 8\. Alternative: Set Environment Variables

```bash
# For KeycloakSecurityIT tests
export KEYCLOAK_SERVER_URL=http://localhost:8080
export KEYCLOAK_REALM=test-realm
export KEYCLOAK_CLIENT_ID=test-client
export KEYCLOAK_CLIENT_SECRET=YOUR_CLIENT_SECRET

# Run security tests
mvn test -Dtest=KeycloakSecurityIT \
  -Dkeycloak.server.url=$KEYCLOAK_SERVER_URL \
  -Dkeycloak.realm=$KEYCLOAK_REALM \
  -Dkeycloak.client.id=$KEYCLOAK_CLIENT_ID \
  -Dkeycloak.client.secret=$KEYCLOAK_CLIENT_SECRET

# For manual producer tests (KeycloakProducerIT)
export KEYCLOAK_SERVER_URL=http://localhost:8080
export KEYCLOAK_REALM=master
export KEYCLOAK_USERNAME=admin
export KEYCLOAK_PASSWORD=admin

# Run manual producer tests (requires explicit flag)
mvn test -Dtest=KeycloakProducerIT \
  -Dmanual.keycloak.test=true \
  -Dkeycloak.server.url=$KEYCLOAK_SERVER_URL \
  -Dkeycloak.realm=$KEYCLOAK_REALM \
  -Dkeycloak.username=$KEYCLOAK_USERNAME \
  -Dkeycloak.password=$KEYCLOAK_PASSWORD
```

### Troubleshooting

**Tests are skipped**: - For `KeycloakSecurityIT`: Verify all four required properties are provided and Keycloak is running on the specified URL. - For `KeycloakProducerIT`: Ensure `-Dmanual.keycloak.test=true` is set along with the required Keycloak properties.

**401 Unauthorized**: Check that: - Users exist with correct passwords - Users have the required roles assigned - Client credentials are correct

**Connection refused**: Ensure Keycloak is running and accessible at the specified URL.

**Token validation errors**: Verify the realm name and client configuration match exactly.

### Setting up Permissions in Keycloak

For permissions-based authorization, you have several options to include permissions in tokens:

#### Option 1: Custom Claims Mapper

1.  In your realm, go to **Client Scopes** → **roles** → **Mappers** → **Create mapper**
    
2.  Set the following:
    
    -   Mapper Type: `User Attribute`
        
    -   Name: `permissions-mapper`
        
    -   User Attribute: `permissions`
        
    -   Token Claim Name: `permissions`
        
    -   Claim JSON Type: `JSON`
        
    -   Add to ID token: `ON`
        
    -   Add to access token: `ON`
        
    
3.  Add the `permissions` attribute to users:
    
    -   Go to **Users** → Select user → **Attributes** tab
        
    -   Add attribute: `permissions` with value like `["read:documents", "write:documents"]`
        
    

#### Option 2: Scope-based Permissions

1.  Configure client scopes:
    
    -   Go to **Client Scopes** → **Create client scope**
        
    -   Scope Name: `documents`
        
    -   Protocol: `openid-connect`
        
    
2.  Add scope to client:
    
    -   Go to **Clients** → Your client → **Client Scopes** tab
        
    -   Add the scope as **Default** or **Optional**
        
    
3.  In your application code, you can then use scopes as permissions:
    

_Java-only: programmatic security policy configuration_

```java
KeycloakSecurityPolicy policy = new KeycloakSecurityPolicy();
policy.setRequiredPermissions("documents,users,admin");
policy.setAllPermissionsRequired(false); // ANY permission
```

#### Option 3: Authorization Services (Advanced)

For complex permission models, enable Keycloak Authorization Services:

1.  Go to **Clients** → Your client → **Settings** → **Authorization Enabled**: `ON`
    
2.  Configure Resources, Scopes, and Policies in the **Authorization** tab
    
3.  Enable **Authorization** on the client
    

Note: Full Authorization Services integration requires additional setup and is more complex than the simple approaches above.
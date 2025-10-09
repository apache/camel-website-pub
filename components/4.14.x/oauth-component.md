# OAuth

**Since Camel 4.12**

**Set of Exchange Processors**

The camel-oauth module comes with Processors that can be added to a route on the client and resource owner side. These processors intercept the message flow and perform the necessary authentication steps against an Identity Provider (IdP) in some specs it also called Authorization Server. Our primary choice of IdP is [Keycloak](https://www.keycloak.org)

The idea is that a "Resource Owner" can give a "User Agent" access to some protected resources without sharing credentials directly with the agent.

For example, Alice has an account with Spotify and now wishes to use a cool service from Acme which compiles a daily playlist according based on Alice’s preferences. Instead of giving Acme her Spotify credentials (i.e. username/password) directly, Acme can obtain an access token from an Identity Provider that encodes the scope and duration for Acme to access Alice’s Spotify account. Alice can revoke access any time - Acme never sees more information thant waht Alice has granted and is necessary to perform the the wanted service.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-oauth</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Authentication/Authorization Flow Types

### OIDC Authorization Code Flow

The Authorization Code Flow returns an Authorization Code to the Client, which can then exchange it for an ID Token and an Access Token directly. The Authorization Code flow is suitable for Clients that can securely maintain a Client Secret between themselves and the Authorization Server.

This code flow relies on user interaction with a browser based application. It is not suitable for fully automated authorization for example in the case of REST based service interaction.

For details see the [OIDC 1.0](https://openid.net/specs/openid-connect-core-1_0.md) spec.

#### Configuration Properties

 
| Name | Description |
| --- | --- |
| `camel.oauth.base-uri` | The base URL to the identity provider (e.g. [https://keycloak.local/kc/realms/camel](https://keycloak.local/kc/realms/camel)) |
| `camel.oauth.redirect-uri` | Valid URI pattern a browser can redirect to after a successful login (e.g. [http://127.0.0.1:8080/auth](http://127.0.0.1:8080/auth)). Must be registered with the identity provider. |
| `camel.oauth.client-id` | The client identifier registered with the identity provider. |
| `camel.oauth.client-secret` | The client secret provided by the identity provider. |
| `camel.oauth.logout.redirect-uri` | (Optional) Valid URI pattern a browser can redirect to after a successful logout. Can be registered with the identity provider. |

### Client Credentials Grant

A client can request an access token using only the client id and secret shared with the identity provider.

This code flow suitable for fully automated authorization for example in the case of REST based service interaction.

For details see the [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749#section-4.4) spec.

#### Configuration Properties

 
| Name | Description |
| --- | --- |
| `camel.oauth.base-uri` | The base URL to the identity provider (e.g. [https://keycloak.local/kc/realms/camel](https://keycloak.local/kc/realms/camel)) |
| `camel.oauth.client-id` | The client identifier registered with the identity provider. |
| `camel.oauth.client-secret` | The client secret provided by the identity provider. |

## Trusted Certificates

Naturally, we want all communication between camel and the identity provider to be secured at the transport layer (TLS). For this, the Camel service need’s to trust the identity provider’s certificate.

```shell
# Fetch the certificate from the IdP endpoint
openssl s_client -connect keycloak.local:443 | openssl x509 > cluster.crt

# Import certificate to Java Keystore (i.e. trust the certificate)
sudo keytool -import -alias keycloak -file cluster.crt -keystore $JAVA_HOME/lib/security/cacerts -storepass changeit

# Trust this cert on macOS
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain cluster.crt

# Trust this cert on Linux
sudo cp cluster.crt /etc/pki/ca-trust/source/anchors/ && sudo update-ca-trust
```

## OAuth for Kafka

For Kafka we can use [strimzi-kafka-oauth](https://github.com/strimzi/strimzi-kafka-oauth) directly, for example [like this](https://github.com/tdiesler/camel-cloud-examples/blob/main/camel-main/kafka-oauth/kafka-oauth-files/kafka-oauth-route.yaml) …​

## Supported Runtimes

Camel OAuth is supported in all Camel Runtimes

-   camel-main
    
-   spring-boot
    
-   quarkus
    

Specifically, it provides an abstraction for the various http-platforms that are native to these runtimes.

## Supported Cluster Environments

Camel applications requiring OAuth authentication are likely part of a larger more complex system architecture, which also likely are part of some larger Kubernetes cluster deployment. In our examples we support these Kubernetes environments …​

-   Local Cluster (e.g. [DockerDesktop Kubernetes](https://docs.docker.com/desktop/features/kubernetes/))
    
-   Remote [K3S](https://k3s.io/) Cluster
    
-   Red Hat [OpenShift](https://www.redhat.com/en/technologies/cloud-computing/openshift)
    

As part of this project we provide a set of [Helm](https://helm.sh/) charts that install the required infrastructure components for the respective cluster environment. For details, have a look at the [dedicated readme](https://github.com/apache/camel/tree/main/components/camel-oauth/helm/README.md).

Keycloak is already configured in such a way that below examples should run without further ado.

## Camel OAuth Examples

There is a comprehensive set of camel-oauth examples as part of [camel-cloud-examples](https://github.com/tdiesler/camel-cloud-examples). You’ll find [camel-jbang kubernetes](../../manual/camel-jbang.md) examples for every OAuth flow, for every runtime, on every supported cluster.

For example …​

```makefile
k8s-fetch-cert:
	@mkdir -p tls
	@echo -n | openssl s_client -connect keycloak.local:443 | openssl x509 > tls/cluster.crt

k8s-export: k8s-fetch-cert
	@$(CAMEL_CMD) kubernetes export platform-http-files/* tls/* \
	--dep=org.apache.camel:camel-oauth:4.14.1-SNAPSHOT \
	--gav=examples:platform-http-oauth:1.0.0 \
	--property=camel.oauth.base-uri=https://keycloak.local/kc/realms/camel \
	--property=camel.oauth.redirect-uri=http://127.0.0.1:8080/auth \
	--property=camel.oauth.logout.redirect-uri=http://127.0.0.1:8080/ \
	--property=camel.oauth.client-id=camel-client \
	--property=camel.oauth.client-secret=camel-client-secret \
	--property=ssl.truststore.certificates=tls/cluster.crt \
	--ignore-loading-error=true \
	--image-builder=docker \
	--image-push=false \
	--trait container.image-pull-policy=IfNotPresent \
	--runtime=camel-main
```
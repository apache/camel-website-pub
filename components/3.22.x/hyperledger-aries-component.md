# Hyperledger Aries

**Since Camel 3.19**

**Only producer is supported**

The Hyperledger Aries component uses [Nessus Aries](https://github.com/tdiesler/nessus-aries) and transitively the [Aries Cloud Agent Java Client](https://github.com/tdiesler/acapy-java-client) to provide access to an ecosystems of Verifiable Credentials (VC). This is part of a larger effort to provide a digital [Self Sovereign Identity (SSI)](https://github.com/tdiesler/nessus-aries/blob/main/docs/img/ssi-book.png), to people, institutions and things - in the end it is all about "Trust over IP".

A good introduction video to this technology space is [The Story of Open SSI Standards](https://www.youtube.com/watch?v=RllH91rcFdE).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-hyperledger-aries</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

hyperledger-aries://wallet?service&options

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Hyperledger Aries component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **removeWalletsOnShutdown** (producer) | Remove wallets from the Agent on shutdown. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Hyperledger Aries endpoint is configured using URI syntax:

hyperledger-aries:walletName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **walletName** (producer) | **Required** The wallet to connect to. |  | String |

### Query Parameters (5 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoSchema** (producer) | Allow on-demand schema creation. | false | boolean |
| **schemaName** (producer) | A schema name. |  | String |
| **schemaVersion** (producer) | A schema version. |  | String |
| **service** (producer) | An API path (e.g. /issue-credential/records). |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Aries Cloud Agent Connection

This component communicates with an instance of [Aries Cloud Agent Python](https://github.com/hyperledger/aries-cloudagent-python) (a.k.a ACA-Py) via REST API, which in turn requires a connection to a Distributed Ledger (e.g. [Hyperledger Indy](https://github.com/bcgov/von-network)) and a [Indy Tails Server](https://github.com/bcgov/indy-tails-server) for Credential Revocation support.

The easiest way to get started is using the Docker Compose script provided by [Nessus Aries](https://github.com/tdiesler/nessus-aries)

docker compose up --detach && docker compose logs -f acapy

The Camel component uses an `AgentConfiguration` object to make the connection to ACA-Py. The connection parameters can be configured through these environment variables…​

ACAPY\_HOSTNAME: localhost
ACAPY\_ADMIN\_PORT: 8031
ACAPY\_USER\_PORT: 8030
ACAPY\_API\_KEY: adminkey

## Examples

Once the connection with ACA-Py is established we can access various [SSI related protocols](https://github.com/hyperledger/aries-rfcs/tree/main/features). Here, we use the classical Alice/Faber example walktrough. Alice, a former student of Faber College ("Knowledge is Good"), connects with the College, is issued a credential about her degree and then uses this verifiable credential to apply for a job with Acme Corp. Acme uses "Trust over IP" to verifiy that Alice actually graduated from Faber and perhaps even more imporantly that Faber is authorized to issue such credentials. Alice gets the job (of course ;-) and can now now use this employment credential to apply for a loan with Thrift Bank. At some point in the future, Alice decides to leave Acme for to pursue other things in life, uppon which, Acme revokes the previously issued credential. The transcript credential from Faber cannot be revoked - the associated cryptographic material remain immutably in the distributed ledger.

The code snipets below are abridged for readability - for the fully working copy have a look at [CamelGettingStartedTest](https://github.com/tdiesler/camel/blob/CAMEL-18156/components/camel-hyperledger-aries/src/test/java/org/apache/camel/component/aries/CamelGettingStartedTest.java).

### Working with Wallets

A Wallet primarily holds Credentials and Connections to other peers. The Ledger does not store personal information - instead, it holds cryptographic material, Credential Schemas, public Digital Identities (DID) and so on. The component can work with Wallets that already exist in ACA-Py or alternatively it can create/remove such Wallets

```java
from("direct:admin")
    .to("hyperledger-aries:admin?service=/multitenancy/wallet")

CreateWalletRequest walletRequest = CreateWalletRequest.builder()
        .walletDispatchType(WalletDispatchType.DEFAULT)
        .walletType(WalletType.INDY)
        .walletName(walletName)
        .walletKey(walletName + "Key")
        .build();

template.requestBodyAndHeaders("direct:admin", walletRequest, Map.of(
        HEADER_MULTITENANCY_TRUSTEE_WALLET, Government,
        HEADER_MULTITENANCY_LEDGER_ROLE, ENDORSER),
        WalletRecord.class);
```

### Creating Credential Schemas

Credential Schema is the base semantic structure that describes the list of attributes which one particular Credential can contain.

It’s not possible to update an existing Schema. If the Schema needs to be evolved, a new Schema with a new version or name needs to be created.

```java
from("direct:faber")
        .to("hyperledger-aries:faber");

SchemaSendRequest schemaRequest = SchemaSendRequest.builder()
        .schemaVersion("1.2")
        .schemaName("Transcript")
        .attributes(Arrays.asList(
                "first_name",
                "last_name",
                "ssn",
                "degree",
                "status",
                "year",
                "average"))
        .build();

SchemaSendResponse schemaResponse = template.requestBodyAndHeaders("direct:faber", schemaRequest, Map.of(
        HEADER_SERVICE, "/schemas"),
        SchemaSendResponse.class);
```

### Creating Credential Definitions

Credential Definition is similar in that the keys that the Issuer uses for the signing of Credentials also satisfies a specific Credential Schema.

It references it’s associated schema, announces who is going to be issuing credentials with that schema, what type of signature method they plan to use (“CL” = “Camenisch Lysyanskya”, the default method used for zero-knowledge proofs by indy), how they plan to handle revocation, and so forth.

It’s not possible to update data in an existing Credential Definition. If a Credential Definition needs to be evolved (for example, a key needs to be rotated), then a new Credential Definition needs to be created by a new Issuer DID.

A Credential Definition can be created and saved in the Ledger by an Endorser.

```java
from("direct:faber")
        .to("hyperledger-aries:faber");

CredentialDefinitionRequest credDefRequest = CredentialDefinitionRequest.builder()
        .schemaId(ctx.getAttachment(TranscriptSchemaId, String.class))
        .supportRevocation(false)
        .build();

CredentialDefinitionResponse credDefResponse = template.requestBodyAndHeaders("direct:faber", credDefRequest, Map.of(
        HEADER_SERVICE, "/credential-definitions"),
        CredentialDefinitionResponse.class);
```

### Create a Peer Connection

When Alice connects to Faber, she doesn’t use Faber’s public DID. Instead, both parties create new DIDs that they use for their Peer Connection.

That A has a trusted connection with B, is of nobody’s business except A and B.

```java
// Inviter creates an invitation (/connections/create-invitation)
UnaryOperator<String> uri = wn -> "direct:" + wn.toLowerCase();
CreateInvitationRequest createInvitationRequest = CreateInvitationRequest.builder().build();
CreateInvitationResponse createInvitationResponse = template.requestBodyAndHeaders("direct:faber",
        createInvitationRequest, Map.of(HEADER_SERVICE, "/connections/create-invitation"),
        CreateInvitationResponse.class);

// This invitation data finds its way to the Invitee somehow (i.e. out-of-band)
ConnectionInvitation invitation = createInvitationResponse.getInvitation();

// Invitee receives the invitation from the Inviter (/connections/receive-invitation)
ReceiveInvitationRequest receiveInvitationRequest = ReceiveInvitationRequest.builder()
        .recipientKeys(invitation.getRecipientKeys())
        .serviceEndpoint(invitation.getServiceEndpoint())
        .build();

ConnectionReceiveInvitationFilter receiveParams = ConnectionReceiveInvitationFilter.builder()
        .autoAccept(true)
        .build();

template.requestBodyAndHeaders("direct:alice", receiveInvitationRequest, Map.of(
        HEADER_SERVICE, "/connections/receive-invitation",
        ConnectionReceiveInvitationFilter.class.getName(), receiveParams),
        ConnectionRecord.class);
```

### Get a Verifiable Credential

A credential is a piece of information about an identity — a name, an age, a credit score…​ It is information claimed to be true.

Credentials are offered by an Issuer and stored in the Wallet of the Holder.

An issuer may be any identity owner known to the Ledger and any issuer may issue a credential about any identity owner it can identify.

The usefulness and reliability of a credential are tied to the reputation of the issuer with respect to the credential at hand. For Alice to self-issue a credential that she likes chocolate ice cream may be perfectly reasonable, but for her to self-issue a credential that she graduated from Faber College should not impress anyone.

```java
/* 1. Faber sends the Transcript Credential Offer
 *
 * The value of this Transcript Credential is that it is provably issued by Faber College
 */

V1CredentialOfferRequest credentialOffer = V1CredentialOfferRequest.builder()
        .connectionId(faberAliceConnectionId)
        .credentialDefinitionId(transcriptCredDefId)
        .credentialPreview(new CredentialPreview(
                CredentialAttributes.from(Map.of(
                        "first_name", "Alice",
                        "last_name", "Garcia",
                        "ssn", "123-45-6789",
                        "degree", "Bachelor of Science, Marketing",
                        "status", "graduated",
                        "year", "2015",
                        "average", "5"))))
        .build();

template.requestBodyAndHeaders("direct:faber", credentialOffer, Map.of(
        HEADER_SERVICE, "/issue-credential/send-offer"),
        V1CredentialExchange.class);

/* 2. Alice inspects the the Transcript Credential Offer
 *
 */

CredentialProposal credentialProposal = holderExchange.getCredentialProposalDict().getCredentialProposal();
CredentialProposalHelper credentialHelper = new CredentialProposalHelper(credentialProposal);
Assertions.assertEquals("Alice", credentialHelper.getAttributeValue("first_name"));
Assertions.assertEquals("Garcia", credentialHelper.getAttributeValue("last_name"));
Assertions.assertEquals("graduated", credentialHelper.getAttributeValue("status"));
Assertions.assertEquals("5", credentialHelper.getAttributeValue("average"));

/* 3. Alice sends the Transcript Credential Request
 *
 */

template.requestBodyAndHeaders("direct:alice", null, Map.of(
        HEADER_SERVICE, "/issue-credential/records/" + holderCredentialExchangeId + "/send-request"),
        V1CredentialExchange.class);

/* 4. Faber receives the Transcript Credential Request
 *
 */

V1CredentialExchange issuerExchange = issuerEvents.credentialEx()
        .filter(cex -> cex.getState() == CredentialExchangeState.REQUEST_RECEIVED)
        .blockFirst(Duration.ofSeconds(10));

/* 5. Faber issues the Transcript Credential
 *
 */

V1CredentialIssueRequest credentialIssueRequest = V1CredentialIssueRequest.builder().build();

template.requestBodyAndHeaders("direct:faber", credentialIssueRequest, Map.of(
        HEADER_SERVICE, "/issue-credential/records/" + issuerCredentialExchangeId + "/issue"),
        V1CredentialExchange.class);

/* 6. Alice receives the Transcript Credential
 *
 */

holderExchange = holderEvents.credentialEx()
        .filter(cex -> cex.getState() == CredentialExchangeState.CREDENTIAL_RECEIVED)
        .blockFirst(Duration.ofSeconds(10));

/* 7. Alice stores the Transcript Credential
 *
 */

V1CredentialStoreRequest credentialStoreRequest = V1CredentialStoreRequest.builder()
        .credentialId(holderCredentialId)
        .build();

template.requestBodyAndHeaders("direct:alice", credentialStoreRequest, Map.of(
        HEADER_SERVICE, "/issue-credential/records/" + holderCredentialExchangeId + "/store"),
        V1CredentialExchange.class);
```

### Verify a Credential

Above we said, that Credentials are offered by an Issuer and stored in the Wallet of the Holder.

During the Credential verification process, the Verifier may request Proof for some attribute claim from the Proover. In our case, Acme (the Verifier) requests proof from Alice (the Proover) that certain attribute claims in the Transcript Credential are infact true.

```java
/* 1. Acme creates a Job Application Proof Request
 *
 * Notice that some attributes are verifiable and others are not.
 *
 * The proof request says that degree, and graduation status, ssn and year must be formally asserted by an issuer and schema_key.
 * Notice also that the first_name, last_name and phone_number are not required to be verifiable.
 *
 * By not tagging these credentials with a verifiable status, Acme’s credential request is saying it will accept
 * Alice’s own credential about her names and phone number.
 */

PresentProofRequest proofRequest = PresentProofRequest.builder()
        .connectionId(acmeAliceConnectionId)
        .proofRequest(ProofRequest.builder()
                .name("Job-Application")
                .nonce("1")
                .requestedAttribute("attr1_referent", proofReqAttr.apply("first_name"))
                .requestedAttribute("attr2_referent", proofReqAttr.apply("last_name"))
                .requestedAttribute("attr3_referent", restrictedProofReqAttr.apply("ssn", transcriptCredDefId))
                .requestedAttribute("attr4_referent", restrictedProofReqAttr.apply("degree", transcriptCredDefId))
                .requestedAttribute("attr5_referent", restrictedProofReqAttr.apply("status", transcriptCredDefId))
                .requestedAttribute("attr6_referent", restrictedProofReqAttr.apply("year", transcriptCredDefId))
                .requestedPredicate("pred1_referent", restrictedProofReqPred.apply("average >= 4", transcriptCredDefId))
                .build())
        .build();

template.requestBodyAndHeaders("direct:acme", proofRequest, Map.of(
        HEADER_SERVICE, "/present-proof/send-request"),
        PresentationExchangeRecord.class);

// 2. Alice searches her Wallet for Credentials that she can use for the creating of Proof for the Job-Application Proof Request

credentials.stream().forEach(cred -> {
    List<String> presentationReferents = cred.getPresentationReferents();
    CredentialInfo credInfo = cred.getCredentialInfo();
    String credDefId = credInfo.getCredentialDefinitionId();
    Map<String, String> attributes = credInfo.getAttrs();
    String referent = credInfo.getReferent();
    log.info("{}", cred);
    log.info("+- CredDefId: {}", credDefId);
    log.info("+- PresentationReferents: {}", presentationReferents);
    log.info("+- Attributes: {}", attributes);
    log.info("+- Referent: {}", referent);

    // Map attribute referents to their respective credential referent
    presentationReferents.stream().forEach(pr -> referentMapping.put(pr, referent));
});

/* 3. Alice provides Job Application Proof
 *
 * Alice divides these attributes into the three groups:
 *
 * - attributes values of which will be revealed
 * - attributes values of which will be unrevealed
 * - attributes for which creating of verifiable proof is not required
 */

PresentationRequest presentationRequest = PresentationRequest.builder()
        .selfAttestedAttributes(Map.of(
                "attr1_referent", "Alice",
                "attr2_referent", "Garcia"))
        .requestedAttributes(Map.of(
                "attr3_referent", indyRequestedAttr.apply("attr3_referent", true),
                "attr4_referent", indyRequestedAttr.apply("attr4_referent", true),
                "attr5_referent", indyRequestedAttr.apply("attr5_referent", true),
                "attr6_referent", indyRequestedAttr.apply("attr6_referent", true)))
        .requestedPredicates(Map.of(
                "pred1_referent", indyRequestedPred.apply("pred1_referent")))
        .build();

template.requestBodyAndHeaders("direct:alice", presentationRequest, Map.of(
        HEADER_SERVICE, "/present-proof/records/" + proverExchangeId + "/send-presentation"),
        PresentationExchangeRecord.class);

/* 4. Acme verifies the Job Application Proof from Alice
 *
 */

template.requestBodyAndHeaders("direct:acme", null, Map.of(
        HEADER_SERVICE, "/present-proof/records/" + verifierExchangeId + "/verify-presentation"),
        PresentationExchangeRecord.class);

verifierExchangeRecord = verifierEvents.presentationEx()
        .filter(pex -> pex.getState() == PresentationExchangeState.VERIFIED)
        .blockFirst(Duration.ofSeconds(10));

Assertions.assertTrue(verifierExchangeRecord.isVerified(), "Not VERIFIED");
```

#### Connectionless proofs

There is a possibility to request proof without securing the connection beforehand. It’s similar to usual credential verification process with two changes:

1.  Verifier should use `/present-proof/create-request` instead of `send-request` service.
    
2.  Verifier should decorate proof presentation with `~service` decorator with their recipient key and endpoint.
    

```java
/* 1. Acme creates Job Application Proof Request.
 *
 * Notice no connectionId and new service endpoint.
 * Everything else is the same as for send-request process.
 */
PresentProofRequest proofRequest = PresentProofRequest.builder()
        .proofRequest(...)
        .build();

String exchangeId = template.requestBodyAndHeader("direct:acme", proofRequest,
        HEADER_SERVICE, "/present-proof/create-request",
        PresentationExchangeRecord.class).getPresentationExchangeId();

/* 2. Acme generates presentation JSON.
 *
 * This is a new step. Acme needs to decorate the presentation request with their service details.
 */
JsonObject presentation = template.requestBodyAndHeader("direct:acme", null,
        HEADER_SERVICE, "/present-proof/records/" + exchangeId,
        PresentationExchangeRecord.class).getPresentationRequestDict();

DID did = template.requestBodyAndHeader("direct:acme", null,
        HEADER_SERVICE, "/wallet/did/public",
        DID.class);

String endpoint = template.requestBodyAndHeaders("direct:acme", null,
        Map.of(HEADER_SERVICE, "/wallet/get-did-endpoint", HEADER_DID, did.getDid()),
        DIDEndpoint.class).getEndpoint();

var decorator = new JsonObject();
var recipients = new JsonArray();
recipients.add(did.getVerkey());
decorator.add("recipientKeys", recipients);
decorator.addProperty("serviceEndpoint", endpoint);

presentation.add("~service", decorator);

/* 3. Acme shares presentation request with Alice.
 *
 * This step is not Camel-specific, thus there is no example.
 * The easiest way to share this JSON is to generate QR code using it
 * and let Alice scan this QR using her Aries mobile wallet.
 */
```
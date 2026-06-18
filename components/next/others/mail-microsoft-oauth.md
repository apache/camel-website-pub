# Mail Microsoft Oauth

**Since Camel 3.18.4**

The Mail Microsoft OAuth2 provides an implementation of `org.apache.camel.component.mail.MailAuthenticator` to authenticate IMAP/POP/SMTP connections and access to Email via Spring’s Mail support and the underlying JavaMail system.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-mail-microsoft-oauth</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

The Mail Microsoft OAuth2 provides an authenticator usable by [Mail](../../4.18.x/mail-component.md) component. Importing `camel-mail-microsoft-oauth` it will automatically import the `camel-mail` component.

Parameters `authenticator` and `mail.imaps.auth.mechanisms` (with value `XOAUTH2`) are mandatory. See the example below for more information.

## Usage

### Microsoft Exchange Online OAuth2 Mail Authenticator IMAP example

To use OAuth, an application must be registered with Azure Active Directory.

Follow the instructions listed in [Register an application with the Microsoft identity platform](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app) guide to register a new application.  
Enable application to access Exchange mailboxes via client credentials flow. Instructions [here](https://learn.microsoft.com/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth)  
Once everything is set up, declare and register in the registry, an instance of `org.apache.camel.component.mail.microsoft.authenticator.MicrosoftExchangeOnlineOAuth2MailAuthenticator`.

For example,

-   in a Quarkus application:
    

_Java-only: registering the OAuth2 authenticator bean in Quarkus_

```java
@jakarta.enterprise.inject.Produces
@Named("auth")
public MicrosoftExchangeOnlineOAuth2MailAuthenticator exchangeAuthenticator() {
    return new MicrosoftExchangeOnlineOAuth2MailAuthenticator(tenantId.get(), clientId.get(), clientSecret.get(),
            username.get());
}
```

-   in a Spring Boot application:
    

_Java-only: registering the OAuth2 authenticator bean in Spring Boot_

```java
@BindToRegistry("auth")
public MicrosoftExchangeOnlineOAuth2MailAuthenticator exchangeAuthenticator(){
    return new MicrosoftExchangeOnlineOAuth2MailAuthenticator(tenantId, clientId, clientSecret, "jon@doe.com");
}
```

and then reference it in the Camel endpoint:

_Java-only: referencing the authenticator in the IMAP endpoint URI_

```java
 from("imaps://outlook.office365.com:993"
                    +  "?authenticator=#auth"
                    +  "&mail.imaps.auth.mechanisms=XOAUTH2"
                    +  "&debugMode=true"
                    +  "&delete=false")
```
# MIME Multipart

**Since Camel 2.17**

This data format that can convert a Camel message with attachments into a Camel message that has a MIME-Multipart message as message body (and no attachments).

The use case for this is to enable the user to send attachments over endpoints that do not directly support attachments, either as special protocol implementation (e.g. send a MIME-multipart over an HTTP endpoint) or as a kind of tunneling solution (e.g. because camel-jms does not support attachments but by marshalling the message with attachments into a MIME-Multipart, sending that to a JMS queue, receiving the message from the JMS queue and unmarshalling it again (into a message body with attachments).

The marshal option of the mimeMultipart data format will convert a message with attachments into a MIME-Multipart message. If the parameter `multipartWithoutAttachment` is set to true, it will also marshal messages without attachments into a multipart message with a single part, if the parameter is set to false it will leave the message alone.

MIME headers of the multipart as "MIME-Version" and "Content-Type" are set as camel headers to the message. If the parameter "headersInline" is set to true, it will also create a MIME multipart message in any case.  
Furthermore, the MIME headers of the multipart are written as part of the message body, not as camel headers.

The unmarshal option of the mimeMultipart data format will convert a MIME-Multipart message into a camel message with attachments and leave other messages alone. MIME-Headers of the MIME-Multipart message have to be set as Camel headers. The unmarshalling will only take place if the "Content-Type" header is set to a "multipart" type. If the option "headersInline" is set to true, the body is always parsed as a MIME message. As a consequence, if the message body is a stream and stream caching is not enabled, a message body that is actually not a MIME message with MIME headers in the message body will be replaced by an empty message.

## Options

The MIME Multipart dataformat supports 5 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **multipartSubType** (common) | `mixed` | `String` | Specify the subtype of the MIME Multipart. Default is mixed. |
| **multipartWithoutAttachment** (common) | `false` | `Boolean` | Defines whether a message without attachment is also marshaled into a MIME Multipart (with only one body part). Default is false. |
| **headersInline** (common) | `false` | `Boolean` | Defines whether the MIME-Multipart headers are part of the message body (true) or are set as Camel headers (false). Default is false. |
| **includeHeaders** (common) |  | `String` | A regex that defines which Camel headers are also included as MIME headers into the MIME multipart. This will only work if headersInline is set to true. Default is to include no headers. |
| **binaryContent** (common) | `false` | `Boolean` | Defines whether the content of binary parts in the MIME multipart is binary (true) or Base-64 encoded (false) Default is false. |

## Message Headers (marshal)

  
| Name | Type | Description |
| --- | --- | --- |
| Message-Id | String | The marshal operation will set this parameter to the generated MIME message id if the "headersInline" parameter is set to false. |
| MIME-Version | String | The marshal operation will set this parameter to the applied MIME version (1.0) if the "headersInline" parameter is set to false. |
| Content-Type | String | The content of this header will be used as a content type for the message body part. If no content type is set, "application/octet-stream" is assumed. After the marshal operation, the content type is set to "multipart/related" or empty if the "headersInline" parameter is set to true. |
| Content-Encoding | String | If the incoming content type is "text/\*" the content encoding will be set to the encoding parameter of the Content-Type MIME header of the body part. Furthermore, the given charset is applied for text to binary conversions. |

## Message Headers (unmarshal)

  
| Name | Type | Description |
| --- | --- | --- |
| Content-Type | String | If this header is not set to `multipart/*` the unmarshal operation will not do anything. In other cases, the multipart will be parsed into a camel message with attachments and the header is set to the Content-Type header of the body part, except if this is application/octet-stream. In the latter case, the header is removed. |
| Content-Encoding | String | If the content-type of the body part contains an encoding parameter, this header will be set to the value of this encoding parameter (converted from MIME encoding descriptor to Java encoding descriptor) |
| MIME-Version | String | The unmarshal operation will read this header and use it for parsing the MIME multipart. The header is removed afterward |

## Examples

```java
from(...).marshal().mimeMultipart()
```

With a message where no Content-Type header is set, will create a Message with the following message Camel headers:

**Camel Message Headers**

Content-Type=multipart/mixed; \\n boundary="----=\_Part\_0\_14180567.1447658227051"
Message-Id=<...>
MIME-Version=1.0

The message body will be:

**Camel Message Body**

\------=\_Part\_0\_14180567.1447658227051
Content-Type: application/octet-stream
Content-Transfer-Encoding: base64
Qm9keSB0ZXh0
------=\_Part\_0\_14180567.1447658227051
Content-Type: application/binary
Content-Transfer-Encoding: base64
Content-Disposition: attachment; filename="Attachment File Name"
AAECAwQFBgc=
------=\_Part\_0\_14180567.1447658227051--

A message with the header Content-Type set to "text/plain" sent to the route

```java
from("...").marshal().mimeMultipart("related", true, true, "(included|x-.*)", true);
```

will create a message without any specific MIME headers set as Camel headers (the Content-Type header is removed from the Camel message) and the following message body that includes also all headers of the original message starting with "x-" and the header with name "included":

**Camel Message Body**

Message-ID: <...>
MIME-Version: 1.0
Content-Type: multipart/related;
    boundary="----=\_Part\_0\_1134128170.1447659361365"
x-bar: also there
included: must be included
x-foo: any value

------=\_Part\_0\_1134128170.1447659361365
Content-Type: text/plain
Content-Transfer-Encoding: 8bit

Body text
------=\_Part\_0\_1134128170.1447659361365
Content-Type: application/binary
Content-Transfer-Encoding: binary
Content-Disposition: attachment; filename="Attachment File Name"

\[binary content\]
------=\_Part\_0\_1134128170.1447659361365

## Dependencies

To use MIME-Multipart in your Camel routes, you need to add a dependency on **camel-mail**, which implements this data format.

If you use Maven, you can add the following to your pom.xml:

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-mail</artifactId>
  <version>x.x.x</version> <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using mimeMultipart with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-mail-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 56 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.mail.additional-java-mail-properties** | Sets additional java mail properties, that will append/override any default properties that are set based on all the other options. This is useful if you need to add some special options but want to keep the others as is. This is a multi-value option with prefix: mail. The option is a java.util.Properties type. |  | Properties |
| **camel.component.mail.alternative-body-header** | Specifies the key to an IN message header that contains an alternative email body. For example, if you send emails in text/html format and want to provide an alternative mail body for non-HTML email clients, set the alternative mail body with this key as a header. | CamelMailAlternativeBody | String |
| **camel.component.mail.attachments-content-transfer-encoding-resolver** | To use a custom AttachmentsContentTransferEncodingResolver to resolve what content-type-encoding to use for attachments. The option is a org.apache.camel.component.mail.AttachmentsContentTransferEncodingResolver type. |  | AttachmentsContentTransferEncodingResolver |
| **camel.component.mail.authenticator** | The authenticator for login. If set then the password and username are ignored. It can be used for tokens which can expire and therefore must be read dynamically. The option is a org.apache.camel.component.mail.MailAuthenticator type. |  | MailAuthenticator |
| **camel.component.mail.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.mail.bcc** | Sets the BCC email address. Separate multiple email addresses with comma. |  | String |
| **camel.component.mail.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.mail.cc** | Sets the CC email address. Separate multiple email addresses with comma. |  | String |
| **camel.component.mail.close-folder** | Whether the consumer should close the folder after polling. Setting this option to false and having disconnect=false as well, then the consumer keeps the folder open between polls. | true | Boolean |
| **camel.component.mail.configuration** | Sets the Mail configuration. The option is a org.apache.camel.component.mail.MailConfiguration type. |  | MailConfiguration |
| **camel.component.mail.connection-timeout** | The connection timeout in milliseconds. | 30000 | Integer |
| **camel.component.mail.content-type** | The mail message content type. Use text/html for HTML mails. | text/plain | String |
| **camel.component.mail.content-type-resolver** | Resolver to determine Content-Type for file attachments. The option is a org.apache.camel.component.mail.ContentTypeResolver type. |  | ContentTypeResolver |
| **camel.component.mail.copy-to** | After processing a mail message, it can be copied to a mail folder with the given name. You can override this configuration value with a header with the key copyTo, allowing you to copy messages to folder names configured at runtime. |  | String |
| **camel.component.mail.debug-mode** | Enable debug mode on the underlying mail framework. The SUN Mail framework logs the debug messages to System.out by default. | false | Boolean |
| **camel.component.mail.decode-filename** | If set to true, the MimeUtility.decodeText method will be used to decode the filename. This is similar to setting JVM system property mail.mime.encodefilename. | false | Boolean |
| **camel.component.mail.delete** | Deletes the messages after they have been processed. This is done by setting the DELETED flag on the mail message. If false, the SEEN flag is set instead. You can override this configuration option by setting a header with the key delete to determine if the mail should be deleted or not. | false | Boolean |
| **camel.component.mail.disconnect** | Whether the consumer should disconnect after polling. If enabled, this forces Camel to connect on each poll. | false | Boolean |
| **camel.component.mail.enabled** | Whether to enable auto configuration of the mail component. This is enabled by default. |  | Boolean |
| **camel.component.mail.fail-on-duplicate-file-attachment** | Whether to fail processing the mail if the mail message contains attachments with duplicate file names. If set to false, then the duplicate attachment is skipped and a WARN is logged. If set to true, then an exception is thrown failing to process the mail message. | false | Boolean |
| **camel.component.mail.fetch-size** | Sets the maximum number of messages to consume during a poll. This can be used to avoid overloading a mail server, if a mailbox folder contains a lot of messages. The default value of -1 means no fetch size and all messages will be consumed. Setting the value to 0 is a special corner case, where Camel will not consume any messages at all. | \-1 | Integer |
| **camel.component.mail.folder-name** | The folder to poll. | INBOX | String |
| **camel.component.mail.from** | The from email address. | camel@localhost | String |
| **camel.component.mail.generate-missing-attachment-names** | Set this to 'uuid' to set a UUID for the filename of the attachment if no filename was set. |  | String |
| **camel.component.mail.handle-duplicate-attachment-names** | Set the strategy to handle duplicate filenames of attachments never: attachments that have a filename which is already present in the attachments will be ignored unless failOnDuplicateFileAttachment is set to true. uuidPrefix: this will prefix the duplicate attachment filenames each with an uuid and underscore (uuid\_filename.fileextension). uuidSuffix: this will suffix the duplicate attachment filenames each with an underscore and uuid (filename\_uuid.fileextension). |  | String |
| **camel.component.mail.handle-failed-message** | If the mail consumer cannot retrieve a given mail message, then this option allows handling the caused exception by the consumer’s error handler. By enabling the bridge error handler on the consumer, then the Camel routing error handler can handle the exception instead. The default behavior would be the consumer throws an exception and no mails from the batch would be able to be routed by Camel. | false | Boolean |
| **camel.component.mail.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.mail.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.mail.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.mail.ignore-unsupported-charset** | Option to let Camel ignore unsupported charset in the local JVM when sending mails. If the charset is unsupported, then charset=XXX (where XXX represents the unsupported charset) is removed from the content-type, and it relies on the platform default instead. | false | Boolean |
| **camel.component.mail.ignore-uri-scheme** | Option to let Camel ignore unsupported charset in the local JVM when sending mails. If the charset is unsupported, then charset=XXX (where XXX represents the unsupported charset) is removed from the content-type, and it relies on the platform default instead. | false | Boolean |
| **camel.component.mail.java-mail-properties** | Sets the java mail options. Will clear any default properties and only use the properties provided for this method. The option is a java.util.Properties type. |  | Properties |
| **camel.component.mail.java-mail-sender** | To use a custom org.apache.camel.component.mail.JavaMailSender for sending emails. The option is a org.apache.camel.component.mail.JavaMailSender type. |  | JavaMailSender |
| **camel.component.mail.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.mail.map-mail-message** | Specifies whether Camel should map the received mail message to Camel body/headers/attachments. If set to true, the body of the mail message is mapped to the body of the Camel IN message, the mail headers are mapped to IN headers, and the attachments to Camel IN attachment message. If this option is set to false, then the IN message contains a raw jakarta.mail.Message. You can retrieve this raw message by calling exchange.getIn().getBody(jakarta.mail.Message.class). | true | Boolean |
| **camel.component.mail.mime-decode-headers** | This option enables transparent MIME decoding and unfolding for mail headers. | false | Boolean |
| **camel.component.mail.move-to** | After processing a mail message, it can be moved to a mail folder with the given name. You can override this configuration value with a header with the key moveTo, allowing you to move messages to folder names configured at runtime. |  | String |
| **camel.component.mail.password** | The password for login. See also setAuthenticator(MailAuthenticator). |  | String |
| **camel.component.mail.peek** | Will mark the jakarta.mail.Message as peeked before processing the mail message. This applies to IMAPMessage messages types only. By using peek, the mail will not be eagerly marked as SEEN on the mail server, which allows us to roll back the mail message if there is a processing error in Camel. | true | Boolean |
| **camel.component.mail.reply-to** | The Reply-To recipients (the receivers of the response mail). Separate multiple email addresses with a comma. |  | String |
| **camel.component.mail.session** | Specifies the mail session that camel should use for all mail interactions. Useful in scenarios where mail sessions are created and managed by some other resource, such as a JavaEE container. When using a custom mail session, then the hostname and port from the mail session will be used (if configured on the session). The option is a jakarta.mail.Session type. |  | Session |
| **camel.component.mail.skip-failed-message** | If the mail consumer cannot retrieve a given mail message, then this option allows skipping the message and move on to retrieve the next mail message. The default behavior would be the consumer throws an exception and no mails from the batch would be able to be routed by Camel. | false | Boolean |
| **camel.component.mail.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.mail.subject** | The Subject of the message being sent. Note: Setting the subject in the header takes precedence over this option. |  | String |
| **camel.component.mail.to** | Sets the destination email address. Separate multiple email addresses with comma. |  | String |
| **camel.component.mail.unseen** | Whether to limit by unseen mails only. | true | Boolean |
| **camel.component.mail.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.mail.use-inline-attachments** | Whether to use disposition inline or attachment. | false | Boolean |
| **camel.component.mail.use-java-mail-session-properties-from-headers** | Whether to allow dynamic JavaMail session properties (message headers whose key starts with mail.smtp. or mail.smtps.) to override the endpoint configuration on a per-message basis. This is disabled by default. Only enable it when these headers originate exclusively from trusted route logic, never from data crossing a trust boundary (for example HTTP query parameters, or JMS/Kafka messages from untrusted producers). When enabled, an attacker able to set these headers could weaken transport security (such as mail.smtp.ssl.trust or mail.smtp.starttls.enable) or redirect the SMTP connection. | false | Boolean |
| **camel.component.mail.username** | The username for login. See also setAuthenticator(MailAuthenticator). |  | String |
| **camel.dataformat.mime-multipart.binary-content** | Defines whether the content of binary parts in the MIME multipart is binary (true) or Base-64 encoded (false) Default is false. | false | Boolean |
| **camel.dataformat.mime-multipart.enabled** | Whether to enable auto configuration of the mimeMultipart data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.mime-multipart.headers-inline** | Defines whether the MIME-Multipart headers are part of the message body (true) or are set as Camel headers (false). Default is false. | false | Boolean |
| **camel.dataformat.mime-multipart.include-headers** | A regex that defines which Camel headers are also included as MIME headers into the MIME multipart. This will only work if headersInline is set to true. Default is to include no headers. |  | String |
| **camel.dataformat.mime-multipart.multipart-sub-type** | Specify the subtype of the MIME Multipart. Default is mixed. | mixed | String |
| **camel.dataformat.mime-multipart.multipart-without-attachment** | Defines whether a message without attachment is also marshaled into a MIME Multipart (with only one body part). Default is false. | false | Boolean |
# ![websocket sink](_images/kamelets/websocket-sink.svg) WebSocket Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Sends each message to a WebSocket server, as a text message or as a binary message.

Use it to push events, commands or data to a service that takes them over WebSocket, such as a chat, a dashboard or a data intake. To receive the messages a WebSocket server pushes, use `websocket-source`.

Input: a text body is sent as a text message, and a bytes body as a binary message. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The headers of the message are not sent.

Output: when it is used inside a route, the body is unchanged, and the headers that start with `CamelVertxWebsocket` are removed.

Good to know: it connects when the first message is sent, and keeps the connection open for the next messages. After the connection is lost, for example because the server restarts, the next message connects again. A message fails when the server cannot be reached, or refuses the connection, for example with a 401 response when the login is wrong. A message is done once it is written to the connection: the server does not confirm it. The address comes only from `url`: the headers that start with `CamelVertxWebsocket` are removed first, so they cannot change where the message is sent. The login comes only from `authorization`, sent as the `Authorization` header when it connects. Query parameters in `url` are sent with it. Camel decodes the URL first, so write a value that contains `+`, `&` or `%`, such as a token or a signature, inside `RAW()`, for example `token=RAW(a+b&c)`: it then reaches the server as written. A `wss://` URL connects with TLS, and the certificate and the host name of the server are checked against the certificate authorities that Java trusts. To trust a private one with Camel JBang or Camel Main, set the application properties `camel.ssl.enabled=true`, `camel.ssl.trustStore`, `camel.ssl.trustStorePassword` and `camel.component.vertx-websocket.useGlobalSslContextParameters=true`: that trust store then replaces the one of Java for every WebSocket connection of the application. A `ws://` URL connects without TLS.

## Configuration Options

The following table summarizes the configuration options available for the `websocket-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The address of the WebSocket server, with the path and any query parameters. It starts with `ws://`, or with `wss://` for TLS. Without a port, it is 80 for `ws://` and 443 for `wss://`. Write a query value with `+`, `&` or `%` inside `RAW()`, such as `token=RAW(a+b&c)`. | string |  | wss://events.example.com/ingest |
| **authorization** | Authorization | The value of the `Authorization` header to send when connecting, for a server that asks for a login, such as `Bearer` followed by a token. It is sent once, when the connection opens, not with each message. | string |  | Bearer my-token |
| **subProtocols** | Subprotocols | The subprotocols to ask the server for, separated by commas, sent in the `Sec-WebSocket-Protocol` header when connecting. Set it only for a server that needs one, such as a GraphQL server. | string |  | graphql-transport-ws |

## Dependencies

At runtime, the `websocket-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:vertx-websocket
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:websocket-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/websocket-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/websocket-sink.kamelet.yaml)
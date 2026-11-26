# ![websocket source](_images/kamelets/websocket-source.svg) WebSocket Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Connects to a WebSocket server, such as a feed of prices, notifications or status updates, and sends on each message the server pushes.

Use it to receive live data that a partner or a public service pushes over WebSocket. To send messages to a WebSocket server, use `websocket-sink`. For a service that calls a URL of yours for each event (a webhook), use `webhook-source`.

Output: the body is the message as the server sent it: text for a text message, bytes for a binary message. No headers are set.

Good to know: it connects when the integration starts, and the integration fails to start when the server cannot be reached, refuses the connection or fails the TLS checks. When the connection is lost, for example because the server restarts, it connects again every `reconnectInterval` milliseconds, without end unless `maxReconnectAttempts` is set. Messages the server sends while it is not connected are lost. The messages are passed on one after the other, in the order the server sent them. For a server that sends nothing until the client asks, such as a feed that needs a subscribe request, set `connectMessage`: it is sent as a text message each time the source connects, when the integration starts and after each reconnect, so the subscription is made again after the connection was lost. Apart from that one message, it only receives. The login comes only from `authorization`, sent as the `Authorization` header when it connects. Query parameters in `url` are sent with it. Camel decodes the URL first, so write a value that contains `+`, `&` or `%`, such as a token or a signature, inside `RAW()`, for example `token=RAW(a+b&c)`: it then reaches the server as written. A `wss://` URL connects with TLS, and the certificate and the host name of the server are checked against the certificate authorities that Java trusts. To trust a private one with Camel JBang or Camel Main, set the application properties `camel.ssl.enabled=true`, `camel.ssl.trustStore`, `camel.ssl.trustStorePassword` and `camel.component.vertx-websocket.useGlobalSslContextParameters=true`: that trust store then replaces the one of Java for every WebSocket connection of the application. A `ws://` URL connects without TLS.

## Configuration Options

The following table summarizes the configuration options available for the `websocket-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The address of the WebSocket server, with the path and any query parameters. It starts with `ws://`, or with `wss://` for TLS. Without a port, it is 80 for `ws://` and 443 for `wss://`. Write a query value with `+`, `&` or `%` inside `RAW()`, such as `token=RAW(a+b&c)`. | string |  | wss://stream.example.com/prices?symbols=ACME |
| **authorization** | Authorization | The value of the `Authorization` header to send when connecting, for a server that asks for a login, such as `Bearer` followed by a token. It is sent once, when the connection opens, not with each message. | string |  | Bearer my-token |
| **connectMessage** | Connect Message | A text message to send to the server each time the source connects, when the integration starts and after each reconnect, such as a subscribe request. It is sent as it is written. Leave it empty for a server that pushes without being asked. | string |  | {"op": "subscribe", "args": \["prices"\]} |
| **maxReconnectAttempts** | Max Reconnect Attempts | How many attempts to connect again it makes after the connection was lost, before it gives up. After it gives up, it receives nothing more until the integration is restarted. 0 means no limit. | integer | 0 |  |
| **reconnectInterval** | Reconnect Interval | How long to wait between two attempts to connect again after the connection was lost, in milliseconds. The first attempt is made at once. | integer | 1000 |  |
| **subProtocols** | Subprotocols | The subprotocols to ask the server for, separated by commas, sent in the `Sec-WebSocket-Protocol` header when connecting. Set it only for a server that needs one, such as a GraphQL server. | string |  | graphql-transport-ws |

## Dependencies

At runtime, the `websocket-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:websocket-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/websocket-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/websocket-source.kamelet.yaml)
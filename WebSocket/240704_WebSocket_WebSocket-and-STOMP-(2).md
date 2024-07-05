# WebSocket and STOMP (2)

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/05
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

In [the previous article](https://github.com/glenn-syj/TIL/blob/master/WebSocket/240703_Websocket_WebSocket-and-STOMP-(1).md), there was a main concern that why WebSocket is related to STOMP.

This article features a brief description of the STOMP and the reason WebSocket and STOMP are tied together.

### Tackling Curiosity

**STOMP: a brief description**

> Simple (or Streaming) Text Oriented Message Protocol (STOMP), formerly known as TTMP, is a simple text-based protocol, designed for working with message-oriented middleware (MOM). It provides an interoperable wire format that allows STOMP clients to talk with any message broker supporting the protocol.
> 
> [Wikepedia - Streaming Text Oriented Messaging Protocol](https://en.wikipedia.org/wiki/Streaming_Text_Oriented_Messaging_Protocol)

- Protocol Overview

Here arises a simple question about how the protocol STOMP is constructed and structured. The main point is that the protocol frame consists of a command, key-value header, a blank line, and the body content. It should be awared that it ends with a null character `^@`.

```
{command}
{headers} (key: value)

{body content}
^@ (null character)
```

```
SEND
destination:/queue/a
content-type:text/plain

hello queue a
^@
```

STOMP commands includes `CONNECT`, `SEND`, `SUBSCRIBE`, `UNSUBSCRIBE`, `BEGIN`, `COMMIT`, `ABORT`, `ACK`, `NACK`, `DISCONNECT`. Also, the communication between server and client uses the command `MESSAGE`, `RECEIPT` or `ERROR`.

- STOMP and MOM, then WebSocket?

It had been found that STOMP is a kind of communication protocol in the application layer. Message Oriented Middlewares become improved with functionalities provided by STOMP. The real time messaging or communication in the distributed system would be exemplars.

Strickly saying, although WebSocket is not a MOM(Message Oriented Middleware), WebSocket serves a simliar but low level role if compared. MOMs like Apach Kafka provide various functionalities through a message broker. However, WebSocket provides a communcation channel in a low level and for a simple message sending.

**Why WebSocket with STOMP?**

- WebSocket message based on the frame

What should be mentioned first is that WebSocket messages are on the frame based communication. The data type in the frame could be text, binary, ping/pong, and so on. In the browser environment, however, WebSocket only hanldles text or binary data.

WebSocket message frame does not restrict the message content via its own protocol. As it is a low level without further additional functionalities, it does not control the frame. Here starts the advatanges of using STOMP.

- STOMP advantages

Commands provided by STOMP like CONNECT, SEND, and SUBSCRIBE helps discern the message type. With the null character, STOMP also makes it easier to handle WebSocket message by structuring the start (command) and the end (null character) of the message.

STOMP defines headers with `key:value` pair. They hold meta data of the message. Using headers, WebSocket communication could be configured with annotating the destination, contents type, and priority.

These features let STOMP support the Pub/Sub model in WebSocket. The Pub/Sub architecture loosens coupling between components, assures high scalability, and supports asynchronous event-driven communication. The commands like SUBSCRIBE and SEND in the STOMP fits the model. Headers containing information needed also help implement complicated messaging patterns over the WebSocket.

**Alternatives for STOMP**

The STOMP would and should not be the only one using on the WebSocket. There are other protocols like AMQP(Advancded Message Queueing Protocol), MQTT(Message Queuing Telemetry Transport), XMPP(Extensible Messaging and Presence Protocol), CoAP(Constrained Application Protocol), HTTP/2, WebRTC. 

As STOMP has an upper hand in the text messaging, it would be valid to assume that the Spring Document WebSocket quick start uses STOMP with its efficiency. However, the sub protocols should be highly considered through the purpose of the service.

### References 

https://en.wikipedia.org/wiki/Streaming_Text_Oriented_Messaging_Protocol

https://stackoverflow.com/questions/40988030/what-is-the-difference-between-websocket-and-stomp-protocols

https://ably.com/topic/pub-sub

https://stackoverflow.com/questions/67436517/what-is-a-websocket-subprotocol
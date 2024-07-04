# WebSocket and STOMP (2)

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/04
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

In [the previous article](https://github.com/glenn-syj/TIL/blob/master/WebSocket/240703_Websocket_WebSocket-and-STOMP-(1).md), there was a main concern that why WebSocket is related to STOMP. Saying again, WebSocket is a 

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

What should be mentioned first is that WebSocket messages are on the frame based communication. 





### References 

https://en.wikipedia.org/wiki/Streaming_Text_Oriented_Messaging_Protocol

https://stackoverflow.com/questions/40988030/what-is-the-difference-between-websocket-and-stomp-protocols

https://en.wikipedia.org/wiki/Duplex_(telecommunications)#FULL-DUPLEX
# WebSocket and STOMP (1)

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/03
- Written By: @glenn-syj

## Explanation

### Start Point

> WebSocket is a thin, lightweight layer above TCP. This makes it suitable for using “subprotocols” to embed messages. In this guide, we use STOMP messaging with Spring to create an interactive web application. STOMP is a subprotocol operating on top of the lower-level WebSocket.
>
> [Spring docs](https://spring.io/guides/gs/messaging-stomp-websocket)

The Spring Boot official guide uses WebSocket with STOMP for interaction. I also had a quick-start proejct for WebSocket in the nodeJS environment. However, there was no protocol structurally visible.

As it is said in the quotes above, WebSocket is a network layer above TCP and STOMP is a subprotocol. Here arises a new queston. In what sense WebSocket needs a STOMP protocol?

This article is the first part of the `WebSocket and STOMP`. It features the background TIL started and the brief description of the WebSocket. 

### Tackling Curiosity

**WebSocket: a brief description**

> WebSocket is a computer communications protocol, providing a simultaneous two-way communication channel over a single Transmission Control Protocol (TCP) connection.
> 
> [Wikepedia - WebSocket](https://en.wikipedia.org/wiki/WebSocket)

Here are two important expressions. One is 'a simultaneous two-way communication channel.' The other is 'a single TCP connection.' Let's briefly follow up these definitions.

- a simultaneous two-way communication channel

This definition leads to the core function WebSocket has. The word `simultaneous` is related to the full-duplex communication. It means that the client and the server each can send messages independently and simultaneously. Furthermore, among the browsers the same messages can be shared through a WebSocket server.

- a single TCP connection

The important is that the very single tcp connection keeps alive, once a HTTP handshake communication occurs. The overheads with frequent channel connections and complicated teardowns are reduced in the TCP connection. Also, as the latency becomes lower than HTTP connection, the data exchange becomes continuous.

### References 

https://en.wikipedia.org/wiki/WebSocket

https://stackoverflow.com/questions/40988030/what-is-the-difference-between-websocket-and-stomp-protocols

https://en.wikipedia.org/wiki/Duplex_(telecommunications)#FULL-DUPLEX
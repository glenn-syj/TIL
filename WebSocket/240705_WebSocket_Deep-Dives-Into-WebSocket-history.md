# Deep Dives Into WebSocket: History

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/05
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

In the current project, it is supposed to use Websocket as a real-time communcation protocol. However, apprehending a protocol cannot be done easily and quickly. I found [RFC 6455 websocket protocol article](https://datatracker.ietf.org/doc/html/rfc6455). The IETF(Internet Engineering Task Force) provides and manages RFC(Requests for Comments). The background and history of the websocket emerged would be a good start point.

### Tackling Curiosity

**Before Websocket**

- HTTP polling

Before websocket emerging, the bidriectional communication between a client and a server was fulfilled through polling HTTP calls. In the HTTP polling, the client keeps sending requests each `n` seconds. It had problems like the below.

First, the server had to forcely use mutiple TCP connections. As HTTP is basically request-response model, each message transportation needs to open a new TCP connection.

Second, the wire protocol with an HTTP header leads to a high overhead in communication. Even if a message content is short, the meta data on the HTTP header causes overheads.

Third, client-side script should keep following and tracing each connection. The polling request from the client needs to keep the logic for mapping each HTTP request-response pair.

**After Websocket**

Websocket keeps a single TCP connection for both sides instead of polling.


### References 
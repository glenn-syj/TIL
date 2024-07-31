# Cross Origin Resource Sharing Explained (1)

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/31
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

When building an web application, there is a freuqently met error with CORS(Cross-Origin Resource Sharing). Surely, it could be resolved with configuration. However, just stepping into next step after going under CORS errors would be not enough. It's time to deep dive into CORS.

This article features a basic concept of CORS and origin based on my error cases.

### Tackling Curiosity

**What is CORS**

Before diving into the world of CORS, it would be great to know why it is called "Cross Origin Resource Sharing." It could be thought in a way that some resources are shared through different origins. 

Then, what is an origin and why it is crossed? The mdn web docs defines the CORS like below.

> Cross-Origin Resource Sharing (CORS) is an HTTP-header based mechanism that allows a server to indicate any origins (domain, scheme, or port) other than its own from which a browser should permit loading resources. 

1. an HTTP-header based mechanism

CORS uses headers in a request and response. The server indicates the permissions to load resources through headers. The headers include below.

- Access-Control-Allow-Origin
- Access-Control-Allow-Methods
- Access-Control-Allow-Headers
- Access-Control-Allow-Credentials
- Access-Control-Expose-Headers
- Access-Control-Max-Age

These headers indicates what kind of access is permitted based on origin, methods, headers, credentials, exposed headers, and the max age. 

If the client-side headers don't match to the server-side configuration, CORS errors occur. 

Especially, the `Access-Control-Allow-Methods` would be featured later with preflight request and `OPTION` method.

2. origin (domain, scheme, or port)

An origin defines the location of a specific resource by the scheme(protocol), hostname(domain), port of the URL. `scheme://domain:port` would be the form. These should be matched correctly. Let's figure out it with an example in the local environment. 

`http://localhost:8080/` would be a good example from its familiarness.

- Scheme

Scheme is a protocol to access the resource.  `http` is the scheme here and the `https` could be.

- Domain

Domain is a unique address of the website.  `localhost` is the domain here as `www.github.com` could be.

- Port

Port is a number to access a specific service or an applciation. Basically, HTTP uses port 80 and HTTPS uses port 443. Port numbers can be configured in a way needed.

The origin of the client side should be included in the CORS policy. It means that the scheme, the domain, and the port from the request should be included in the CORS policy and matched exactly.

**Test Case: localhost**

Let's think about these two origins. One is `http://localhost:3000/` and `http://127.0.0.1:3000/`. Those are the origins used as a client side local website address.

The server side configuration has included `http://127.0.0.1:3000` in the `Access-Control-Allow-Origin` header. The client side sends a request from `http://localhost:3000`.

Then, would this result get validated with CORS policy? The answer is NO. 

It's easy to understand when considering basically headers are gotten and set in a string. It means that each side apprehends both origins as different for the domains does not match (`localhost` vs. `127.0.0.1`). 


### References

https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS

https://developer.mozilla.org/en-US/docs/Glossary/Origin
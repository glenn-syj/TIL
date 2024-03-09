## RequestDispatcher.forward() vs HttpServletResponse.sendRedirect()

### Explanation

**Start Point**

There are two ways for a page direction. One is called 'forward', which uses `ReqeustDispatcher.forward().` The other is called 'redirection', `HttpServletResponse.sendRedirect().` Then, what would be the difference between them?

**Tackling Curiosity**

1. Forward

In the EE6 docs, it describes the `RequestDispatcher` as follow.

> Defines an object that receives requests from the client and sends them to any resource (such as a servlet, HTML file, or JSP file) on the server. The servlet container creates the RequestDispatcher object, which is used as a wrapper around a server resource located at a particular path or given by a particular name.

> This interface is intended to wrap servlets, but a servlet container can create RequestDispatcher objects to wrap any type of resource.

Shortly, `RequestDispatcher` is used to transfer a certain resource, especially servlet, to the client. The description on `RequestDispatcher.forward()` directly shows why it is called _RequestDispatcher_. (I would remove the unnecessary repetition.)

> (...) For a RequestDispatcher obtained via getRequestDispatcher(), the ServletRequest object has its path elements and parameters adjusted to match the path of the target resource.

> forward should be called before the response has been committed to the client (before response body output has been flushed). If the response already has been committed, this method throws an IllegalStateException. Uncommitted output in the response buffer is automatically cleared before the forward. (...)

This method should be processed before the response gets to the client. It dispatches the request/response to the same group/server for further processing (not considering the level inside), not sends the completed reponse to the client.

Furthermore, the container is involved in the process, not the client and the browser. As the browser doesn't have its role in the process, the address would not be shown in the browser. Instead, it remains the same.

2. Redirect

`HttpServletResponse` is an interface for providing a "HTTP-specific" features when sending response. Therefore, it has methods `addHeader()`, `getHeader()`, `encodedRedirectURL()`, and so on.

`HttpServletResponse.sendRedirect()` needs a parameter _String location_, which is the redirect location URL. EE6 docs describes it just as below.

> Sends a temporary redirect response to the client using the specified redirect location URL and clears the buffer. The buffer will be replaced with the data set by this method. (...) This method can accept relative URLs;the servlet container must convert the relative URL to an absolute URL before sending the response to the client. If the location is relative without a leading '/' the container interprets it as relative to the current request URI. If the location is relative with a leading '/' the container interprets it as relative to the servlet container root.

> If the response has already been committed, this method throws an IllegalStateException. After using this method, the response should be considered to be committed and should not be written to.

What we need to primarily pay attention is the word 'temporary.' The temporary redirect response is transferred to the client here by the container. Then, the client/browser can notice the new response with the old requset/response being lost. This is why the address bar is renewed in the new URL.

**Furthermore**

If the resource being transferred to a new server, redirect would be adequate. However, when an operation should be repeated or the resource be reused, it would be helpful and efficient to take the forwarding way

### References

https://stackoverflow.com/questions/2047122/requestdispatcher-forward-vs-httpservletresponse-sendredirect
https://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletResponse.html#sendRedirect(java.lang.String)
https://docs.oracle.com/javaee%2F6%2Fapi%2F%2F/javax/servlet/RequestDispatcher.html#forward(javax.servlet.ServletRequest,%20javax.servlet.ServletResponse)
https://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletResponse.html
https://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletResponse.html#sendRedirect(java.lang.String)
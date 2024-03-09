## How is HTML String in the response translated into HTML code?

### Source Code

```java
// write() in PrintWriter
public void write(String s, int off, int len) {
        try {
            synchronized (lock) {
                ensureOpen();
                out.write(s, off, len);
            }
        }
        catch (InterruptedIOException x) {
            Thread.currentThread().interrupt();
        }
        catch (IOException x) {
            trouble = true;
        }
    }
```

### Explanation

**Start Point**

When making a simple website with `Servlet`, I used `PrintWriter` class to write html codes wrapped in String type for passing them as a http response. Then, how are html codes wrapped in String type parsed? Before diving into the broad and deep world of browser, the java servlet code would be helpful.


**Tackling Curiosity**

 I found that it uses `PrintWriter` class inside the `HttpServletResponse` class. It extends the abstract class `Writer`, and it saves the String (which would be html codes String here) in its inner field of `OutputStream`. The content inside the `OutputStream` object equals to the response body.

 However, this body with html codes won't be parsed without setting the content type of the response. This is why _text/html_ should be set. The browser processes HTML parsing through this type and starts to construct a DOM Tree. Then, rendering goes on and users can see screen with parsed html.
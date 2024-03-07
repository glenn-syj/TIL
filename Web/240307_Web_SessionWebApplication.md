## What is Session? (Web Application)

### Explanation

**Start Point**

The term 'session' seems to be used in various contexts even including everyday activities. I have met this word in the context of JSP Web Session. In the context, 'session' becomes a state where variables for checking the condition is stored before executing further codes. Sometimes, its storaging feature makes itself compared to Cookie. However, I would discuss it in the view broader than seeing the session just a storage or a state. It needs more sophisticated approach.

**Tackling Curioisity**

I suggest to comprehend it as a term referring a time-delimited, stateful storage and checkpoint in the middle of the client and the server. It shows that (1) session links each end in two-way with the HTTP request/response. The session can judge if the request or the state is valid and filter the request or any unauthorized action. Here becomes the word 'state' a qualification for a specific action. 

For example, if an user wants to see his/her user information, the action of login should be processed earlier than the action of fetching his/her data. However, the server side does not know the state of logging in. Then, the session plays a part of a checkpoint. It passes back the internal temporary data the client wants or allows the request to approach DB as a result. It ensures a fast, safe, and effective resource control.

(2) A session is a time-delimited state and also storage segmented uniquely by each user or connection. A new session is created in response to a user request inside the server side. The session (just like storage) is allocated with a segmented and unique space in the web server memory. The 'session id' refers the key of a intially stored value related with the address of the session, which would be attached to the response. A cookie which has a key of `JSESSIONID` or `PHPSESSID` is set on the response packet. The cookie is put in the HTTP Request header later. 

It is important that the browser (the client side) only knows the session id, not the data on the session. Hence, the encrypted or hashed value of a specific key can be passed and the action which requires sensitive data would be successfully done without a risk for exposure. The authorization and the authentication key could be good examples.

(3) Another notable feature of a session comes from the fact that the variables it holds are temporary. Not only is it destroyed when the connection is lost, but the state it suggest is also temporary. The data within the session would last only in the session, unless the user confirms an action which affects the DB. It helps DB be more organized for the DB doesn't have to save every data.

The most frequent and familiar exmaples are shown on the E-commerce websites. They show us where we recently visited for checking the product and allow us to store products in the wish list.

### References

**Most helpful**
https://www.bitspedia.com/2012/05/how-session-works-in-web-applications.html

https://medium.com/@llamacorn/computer-science-sessions-7517ec8af766
https://en.wikipedia.org/wiki/Session_(computer_science)
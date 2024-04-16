# Tomcat wtpwebapps structure explained

## Explanation

### Start Point

When running a dynamic web project with Stirng Tool Suite 4, I practiced a file upload funtion with a custom RESTful API in Spring. As it was Spring Legacy Project, the `resources/` folder under `src/main/webapp/` should have been familiar.

However, I found myself having trouble in uploading a file. What I faced was a custom error message. The error was related with the route, `{workspace route}\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\{project}\resources\upload`, not exsiting. It was a returned value from `resource.getFile().getCanonicalPath()`. 

After narrowing down the reason why the path didn't exist, I found that the parent folder of the path above was (1) somehow related with `server` and (2) something temporary from `tmp0`. 

### Tackling Curiosity

1. Why the route includes `org.eclipse.wst.server.core/`

The `org.eclipse.wst.server.core/` folder is created by WTP (Web Tools Platform) using WST (Web Standard Tools). As its name looks like an API or a library name, there was [an eclipse dev site](https://eclipse.dev/webtools/wst/api/org/eclipse/wst/server/core/package-summary.html) summarizing the package.

> ServerCore is the main entry-point and provides access to most of the remaining API. From here, you can get the existing server runtimes and servers, get the available server types, and access interfaces for all extension points.

This gives a cue for tracing the error in the path. `wst` means Web Standard Tool. `server.core` indicates that the folder is for "the main entry-point". Also, the notable is the words, "the existing server runtimes." I suppose that the folder can be thought as **the main entry-point** during the existing server runtimes.

2. What `tmp0` indicates

The more appropriate form of the folder is `tmpX`, where `X` is a number. `tmp1` and `tmp2` can be created either. The number `X` exists for the file lock restriction leads the eclipse to create a new temp folder.

Inside the `tmpX` folder is `wtpwebapps` folder. The `wtpwebapps` is an elipse-specific folder created when a dynamic web project is run. The server's `webapps\` folder is not the very folder above.

Also, we can find the path above in the server configuration window. The path in 'Server Locations' is just same as the `{workspace route}\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\`. 

The `wtpwebapps` folder is **where the eclipse deploys the web application**. Monintoring changes in the source code from the eclipse are renewed and synced after this.

### References

https://eclipse.dev/webtools/wst/api/org/eclipse/wst/server/core/package-summary.html

https://stackoverflow.com/questions/46860523/few-general-questions-about-org-eclipse-wst-server-core-folder-of-a-web-applic

https://stackoverflow.com/questions/12446263/difference-between-wtpwebapps-and-webapps-folder-in-tomcat

https://www.baeldung.com/eclipse-tomcat
# Embedded tomcat exploration

**Disclaimer**
- Last modified: 24/04/17
- Written By: @glenn-syj

## Explanation

### Start Point

Spring Boot, a light weight version of the Spring Framework, has recently deployed its version `3.x.x` which requires Java 17. With learning the Spring Boot, I found that it does not require to set a server for an application. How is that possible? This question leads me to the world of the Spring Boot. An embedded tomcat would be my first topic.

### Tackling Curiosity

1. Goals of Spring Boot

Before the details, the primary goals in the Spring Boot would be heplful.

> Provide a radically faster and widely accessible getting-started experience for all Spring development.
>
> Be opinionated out of the box but get out of the way quickly as requirements start to diverge from the defaults.
>
> Provide a range of non-functional features that are common to large classes of projects (such as embedded servers, security, metrics, health checks, and externalized configuration).
>
> Absolutely no code generation (when not targeting native image) and no requirement for XML configuration.

This article especially focuses on the embedded servers.

2. Dive into the embedded tomcat

**Spring Boot Usage**

Spring Boot can package an application as a `jar` or `war` file. It also enables to use an embedded HTTP server. Here, the word 'embedded' means that a single application and the one entire tomcat server is compressed into a single `jar` or `war` file. Tomcat, Jetty, and Undertow are the possible server candidates. 

**Benfeits of Embedded Tomcat**

How an embedded tomcat improves efficiency and the performance?

The embedded tomcat instance enables inidividual applications to be independently taken. The effects from the application started or restrated are restricted in the very application. Others are not affected. A standalone architecture does not ensure the the state above. 

Also, the workload management in a single application is posibble through using the embedded tomcat. It means that using an embedded tomcat enables individual resource management, which leads to (1) allocation the resources in a only necessary amount (2) without affecting other applications.


3. Tracing the footprints

The `spring-boot-starter-web` dependency shows that it internally provides dependencies related with a tomcat server, which are nested. The below examples are from [javaguides.net](https://www.javaguides.net/2019/04/spring-boot-embedded-servers-tomcat-jetty-and-undertow.html)

```xml
<dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-tomcat</artifactId>
     <scope>compile</scope>
</dependency>
```

Again, the `spring-boot-starter-tomcat` has dependencies about tomcat server. It would be helpful to know that the depencies inlcudes the word `embed`. 

```xml
<dependency>
     <groupId>org.apache.tomcat.embed</groupId>
     <artifactId>tomcat-embed-core</artifactId>
     <version>8.5.23</version>
     <scope>compile</scope>
</dependency>
<dependency>
     <groupId>org.apache.tomcat.embed</groupId>
     <artifactId>tomcat-embed-el</artifactId>
     <version>8.5.23</version>
     <scope>compile</scope>
</dependency>
<dependency>
     <groupId>org.apache.tomcat.embed</groupId>
     <artifactId>tomcat-embed-websocket</artifactId>
     <version>8.5.23</version>
     <scope>compile</scope>
</dependency>
```

### References

https://spring.io/projects/spring-boot

https://www.theserverside.com/definition/embedded-Tomcat

https://stackoverflow.com/questions/23176717/embedded-vs-non-embedded-java-server

https://stackoverflow.com/questions/30080855/difference-between-spring-and-spring-boot
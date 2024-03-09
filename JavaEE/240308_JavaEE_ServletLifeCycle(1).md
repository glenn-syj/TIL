## Lifecycle of Servlet (1): Container

### Explanation

**Start Point**

I’ve found out that the values of fields(member variable) in the servlet file wasn’t destroyed or initialized again. Of course, the variables in the session are gone when the connection ends by closing a browser or the delimited time expires. However, the variables in the fields of a servlet class maintained their values. Why does it happen? It seemed to get involved with the life cycle of servlet. Then, where does servlet work and where is it allocated?

**Tackling Curiosity**

1. What is a container, and why do we use it

The web container of the Java EE service controls the lifecycle of a servlet. Then, what does the term ‘container’ mean? Containers could be regarded as the interface between a component, as *Java EE6* describes. A component is deployed in the container with other components assembled as a Java EE module. The process off deploying after assembling ensures underlying features like security, transaction management, and so on.

The described above could be followed: (1) authorization and access control for the resource, (2) clean and clear methods relationship with one transaction being regarded as a single unit, (3) JDNI(Java Naming and Directory Interface) for naming and directory functionality, and (4) low-level communications using enterprise bean.

However, *Java EE6* specifies that this kind of features can be different with the container where the component is deployed. When one environment allows approach to the specific data base, while other might not.

1. The types of containers

There are Java EE server, EJB container(Enterprise JavaBeans container), Web Container, Application client container, Applet container. These containers construct the deployment process in the Java EE application components. The description below is based on *Java EE6* again. Java EE server, EJB container, web container would be the main interests.

- Java EE server
    
    Java EE server provides EJB and web containers. The lifecycle of JAVA EE product starts here, ends here.
    
- Enterprise JavaBeans container
    
    EJB container manages the execution of enterprise beans for JAVA EE applications. Shortly, it is about business logic of the program. For EJB containers are provided by Java EE server, enterprise beans are also run on the JAVA EE server. 
    
    It performs functionalities with life cycle management, security, transaction management, object pooling.
    
- Web Container
    
    Web container manages the execution of web pages, servlets and some EJB components. It should be awared that a web container is not run on the client machine. Rather, as Web containers are provided by Java EE server, servlets and web pages are also run on the JAVA EE server. 
    
- Application client container
    
    Application client container manages the execution of application client components. It is run on the client machine as its name shows.
    
- Applet container
    
    Applet container manages the execution of applets. A web browser and Java plugins on the client make up this container.
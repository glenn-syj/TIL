## What is Spring IoC Container?

### Explanation

**Start Point**

Getting started with the Spring Framework, I frequently faced words like ‘IoC’ and ‘Container.’ What are they and what are they doing? Container seems to stem from the previous technology, `JavaEE` which includes `servlet` and `JSP` . In the context, containers were the interface between components. Containers in `Spring` would have the similar systemic role but the different features. However, I couldn’t comprehend the word ‘IoC’ after hearing the full form, ‘Inversion of Control.’

**Tackling Curiosity**

1. What is ‘IoC’

The Inversion of Control is a design pattern or principle of which the control of the objects or the components in the program is transferred to the external framework or the portion. In short, its flow of data and the control is inverted compared to the procedural programming. Thus, the external framework calls the custom code in IoC.

The principle ensures the greater modularity, easy testing, and fewer hassles in switching the implementation by decoupling the execution and its implementation. These goals are pursued through various patterns like Service Locator pattern, Factory pattern, or DI(Depedency Injection).

2. Why Spring Container is called IoC

The principle is implemented in the Spring Framework, either. The *Spring Doc* says that the IoC principle embraces ‘Dependency Injection’ in `Spring`, as it is mandatory for objects to define their dependencies using the constructor or the factory method. 

In the `Spring` , what would have the role of ‘the object’ or ‘the external framework?’ There are two packages which consist of the Spring IoC Container. `org.springframework.beans` would be the objects and `org.springframework.context` would be the other. The instantiation, location of the dependencies, and even configuration of the bean (object) are delegated to the container (framework). It means that the container controls the lifecycle of the beans. Don’t forget that the word ‘bean’ refers an object of which lifecycle and status are controlled by the container. Hence, the dependencies among them are the main interest of the Spring IoC container.

3. How Spring Container works

There are three two interfaces directly involved in the work of the container.

- BeanFactory: configuration and basic functionality
    
    `BeanFactory` is the root interface for accessing the bean container, managing the configuration of the beans (or any type of obects), and registering the application components. `BeanFactory` load bean definitions from a configuration source. It also implements the interface with the bean lifecycle: a custom `init-method`, setters for `beanName`, `beanClassLoader`, and so on.
    
- ApplicationContext: enterprise-specific functionality
    
    `ApplicationContext` is a sub-interface of `BeanFactory` . It supports the functionalities related with AOP features, message resource handling, event publication, application-layer specific context, as *spring 4.1.3* says. `WebApplicationContext` would be the special context for web application.
    

**Furthermore**

After writing this article, I found out that those following issues would be helpful in under standing Spring IoC Container and the Spring Framework: (1) the specific features and interfaces of `BeanFactory`, (2) the notion of the context and its importance, and (3) deep dive in the beans and their lifecycle. These topics will lead me to the deeper comprehension of the Spring Framework.

### References

**most helpful**
https://docs.spring.io/spring-framework/reference/core/beans/introduction.html


https://en.wikipedia.org/wiki/Inversion_of_control

[https://www.baeldung.com/inversion-control-and-dependency-injection-in-spring#:~:text=What Is Inversion of Control,context of object-oriented programming](https://www.baeldung.com/inversion-control-and-dependency-injection-in-spring#:~:text=What%20Is%20Inversion%20of%20Control,context%20of%20object%2Doriented%20programming).

https://docs.spring.io/spring-framework/docs/6.1.4/javadoc-api/org/springframework/beans/factory/BeanFactory.html
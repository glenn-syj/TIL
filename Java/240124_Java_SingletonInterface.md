## The interface-type casting of the Singleton instance

### Source Code

### Explanation

```java
// MyInterface.java

public interface MyInterface { 
    void printTheWriter();
}
```
```java
// MyInterfaceImpl.java

public class MyInterfaceImpl implements MyInterface {
    
    private static MyInterface instance = new MyInterfaceImpl();

    private MyInterfaceImpl() {};

    public static MyInterface getInstance() {
        return instance;
    }

    @Override
    public void printTheWriter() {
        System.out.println("Glenn-syj");
    }

}

```


**Start Point**

With the Singleton design pattern, the instance of the interface implemented class (`...Manager`) is fetched by `getInstance()`. The fetched instance is initialized with the type of the implemented interface, why not the concrete class?

**Tackling Curiosity**

Yesterday, I wrote a document about the SOLID principles of the Object-Oriented Programming (`240123_Java_SOLIDprinciples`). The DIP(Dependency Inversion Principle) gave me a hand.

The DIP points that high-level modules should not depend on low-level modules. Rather, depending on interfaces or an abstract class is needed. 

Then, flexibility in the code is assured by casting the type of the instance as the interface. Through this kind of interface-type casting, The code modification or even the replacement of the `...Impl` class which internally constructs instance doesn't affect the main code. 

### Reference

https://stackoverflow.com/questions/39074628/using-singleton-with-interfaces-java
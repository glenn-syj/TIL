
## Native peer explained

**Last Modified: 24-04-03**

**Written By: @glenn-syj**

### Explanation

**Start Point**

1. Background

In reading 'Effective Java', a new and unfamiliar word 'native peer' got my eyes. It was a part describing why destructors like `finalize` (before Java 8), `cleaner` (after Java 9) should not be used to manage a destruction of an object. The main reason behind it is that the issues in the performance, security, uncertainty after the usage. The garbage collector might not collect an object with `finalize`, either. However, the writter says that destructors can be used as (1) a safety line onto closing the resource and (2) a disallocator for native peers.

2. Assumption

Before diving into the world of the native peer, I assumed that (1) a native peer would be an instance which has a resource with no disallocation and (2) the lifecycle of the instance does not follow the normal java instance managed by JVM. Therefore, The main point here would be what 'native' means.

**Tackling Curiosity**

1. What 'native' means

The meaning of the word 'native' is related to the situation when non-java codes are invoked in the java application. The non-java codes usually includes C/C++ and the assembly language. For example, a native method can be a method written in C++, but called from java application. The native method helps improve program performance, platform dependant features, and reusability of written codes.

In the sense of the word 'native' above, 'native peer' becomes an instance which does not allow the JVM to manage, but is used in the java application. The word 'peer' sounds relational as the main java application is called a 'java peer'. A java peer invokes a method for functionalites which the native peer has.

2. Native Peer Examples: usage and destruction 

The codes below are from the Stackoverflow post which describes the native peer in a manner that makes easier to understand it. 

- Native Class (C++)

```C++
//https://stackoverflow.com/questions/4568972/what-is-a-native-object

class print_hello{
public:
    void do_stuff(){std::cout<<"hello"<<std::endl;}
}
```

- Java Peer Class

```java
class PrintHello{
    //Address of the native instance (the native object)
    long pointer;

    //ctor. calls native method to create
    //instance of print_hello
    PrintHello(){pointer = newNative();}

    ////////////////////////////
    //This whole class is for the following method
    //which provides access to the functionality 
    //of the native class
    public void doStuff(){do_stuff(pointer);}

    //Calls a jni wrapper for print_hello.do_stuff()
    //has to pass the address of the instance.
    //the native keyword keeps the compiler from 
    //complaining about the missing method body
    private native void do_stuff(long p);

    //
    //Methods for management of native resources.
    //

    //Native instance creation/destruction
    private native long newNative();
    private native deleteNative(long p);

    //Method for manual disposal of native resources
    public void dispose(){deleteNative(pointer);pointer = 0;}
  }
```

In the code above, (1) `PrintHello()`

### References

Many parts of this article is same as the earilier article of myself written in Korean
https://github.com/Glenn-syj/more-effective-java/blob/glenn-syj/chapter_02/item08_%EC%86%90%EC%98%81%EC%A4%80_%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%ED%94%BC%EC%96%B4%EC%99%80-%EC%83%9D%EB%AA%85-%EC%A3%BC%EA%B8%B0.md
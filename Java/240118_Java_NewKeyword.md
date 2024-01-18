## What does the 'new' Keyword do?

### Java Official Document

**Creating Objects**
> 
> 1. Declaration: The code set in bold are all variable declarations that associate a variable name with an object type.
> 
> 2. Instantiation: The new keyword is a Java operator that creates the object.
> 
> 3. Initialization: The new operator is followed by a call to a constructor, which initializes the new object.
>

- source: https://docs.oracle.com/javase/tutorial/java/javaOO/objectcreation.html

### Explanation

**Start Point**

When creating `Class` (which is directly inherited from `Object`), the `new` keyword is necessary. Although, how this keyword works in JVM or compiler seems mistified to me.

**Tackling Curiosity**

The new keyword is, in fact, an operator which instantiates a class. Then, what happens? The below is how the `new` keyword and object creating works.

```java
Object A; // Declaration Part
A = new Object(); // Instantiation and Initialization Part
```

`Object A` is the declaration part. It allocates the type information(`Object`) and the name(`A`) of the variable in the **stack memory**.

`A = new Object()` is the instantiation and initialization part. After the actual object instance is created in the **heap memory**, the reference is assigned to the variable `A`.

The `new` keyword in this process play roles below.

1. `new` allocates memory for a new object in the heap memory of JVM
2. `new` invokes the object constructor
3. `new` returns reference to the memory

Also, the reference can be directly used without being assigned to a value.

```java
int height = new Rectangle().height
```

### Furthermore
**Java**
```java
Object create() {
    return new Object();
}
```
**Compiler**
```
Method java.lang.Object create()
0   new #1              // Class java.lang.Object
3   dup
4   invokespecial #4    // Method java.lang.Object.<init>()V
7   areturn
```


### Reference

https://docs.oracle.com/javase/tutorial/java/javaOO/objectcreation.html </br>
https://medium.com/culi-tech-viet/stack-and-heap-in-java-b25163f1d14b </br>
https://docs.oracle.com/javase/specs/jvms/se7/html/jvms-3.html </br>
https://stackoverflow.com/questions/4404872/is-there-something-like-malloc-free-in-java/4404894#4404894

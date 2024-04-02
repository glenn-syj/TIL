## Why do we us Mockito and JUnit

**Last Modified: 24-04-02**

**Written By: @glenn-syj**

### Explanation

**Start Point**

In reading 'Effective Java' within a reader group, I had faced a serious but a quite simple question for a starter. "How the unit test using Mockito and JUnit is different from a custom unit test?" It was a part explaining the singleton pattern. Of course, telling the answer would be easy. The answer must be on the same line with the reason why frameworks are used. However, this kind of answer won't be sufficient without research on these frameworks.

**Tackling Curiosity**

1. What is Mockito and JUnit

Mockito is a mocking framework for Java  which allows to verify interactions and stub method calls. The mock object could be created and injected through Mockito.

Annotations like `@Mock`, `@DoNotMock`, `@Spy`, and `@Captor` help users safely mock an object with efficiency. Injecting the mock object can be processed with `@InjectMocks` annotation, either.

JUnit is a testing framework, especially one of the unit testing frameworks for Java. It automates an execution of codes for a test. It reduces the effort and the time devoted to the repetitive exeuction of codes when adding a new code.

Both of them are frequently used together for a unit test. Before a deep dive into each framework, this article only illustrates the precise features.

2. Frameworks over a manual test

Frameworks for mocking and unit testing has many advantages compared to a manual test. They prevent the develpoer from human errors like omitting and forgetting, smelly custom codes with no consideration of maintenance. Also, the environment they serve easily integrated into other tools like IDEs. A simple case is going to be introduced below.

JUnit instantiates the class of the test like the manual test code. The test class has a lifecycle as a test object in the does. However, it seems clean and clear that annotations like `@BeforeClass`, `@BeforeAll` and `@AfterEach` assures more productivity and safety than a manual test by determining the exeuction time. 

```java
// https://stackoverflow.com/questions/68424864/how-does-junit-test-work-in-the-background
class Test{
   private  String hello = "";

   @Test
   void test1() {
      hello = hello + "1";
      System.out.println(hello);
   }
   @Test
   void test2() {
      System.out.println(hello)
   }
}
```

If the code above written, the instance of `Test` would be created. After the creation, a test method within the instance will be called.

```java
// https://stackoverflow.com/questions/68424864/how-does-junit-test-work-in-the-background

Test test = new Test();

test.test1();

...

test = new Test();

test.test2();
```

It must be remembered that the method `test1()` has no priority in the call to the method `test2()`. The importance is in the way JUnit simplifies the test process.

### References

https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html

https://www.baeldung.com/mockito-annotations

https://junit.org/junit5/docs/current/user-guide/

https://en.wikipedia.org/wiki/JUnit

https://stackoverflow.com/questions/5114193/junit-testing-what-makes-it-so-useful-over-manual-testing

https://www.baeldung.com/junit-5

https://www.linkedin.com/pulse/unit-testing-java-aarush-chopra/
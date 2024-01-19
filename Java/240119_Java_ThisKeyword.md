## About This Keyword

### Source Code
```java
public class Main {
  int x;

  // Constructor with a parameter
  public Main(int x) {
    this.x = x;
  }

  // Call the constructor
  public static void main(String[] args) {
    Main myObj = new Main(5);
    System.out.println("Value of x = " + myObj.x);
  }
}
```
source: https://www.w3schools.com/java/ref_keyword_this.asp

### Explanation

**Start Point**

When using 'this' keyword, it refers to the field as `this.field` or the method as `this.method()`, and the constructor as `this()` or `this(Type parameter)`. Then, how about the code with instance?


**Tackling Curiosity**
'this' keyword refers to the current object in the method or the constructor of the class. Also, `this.x` resovles the confusion between member variables and the arguemnt in the constructor. This is how `this` keyword get its importance.
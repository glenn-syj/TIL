## Why `instaceof` throws an error in the code between incompatible types, but not in the `String.equals()`?

### Source Code
```java
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    return (anObject instanceof String aString)
            && (!COMPACT_STRINGS || this.coder == aString.coder)
            && StringLatin1.equals(value, aString.value);
}
```

### Expalanantion

**Start Point**
The `String.equals()` method is frequently used to check and verify that a string equals to specific string. I wondered how it works internally at first. In the process, it was found that the `instanceof` operator checks the type of the parameter. Hence I wrote the test code below to comprehend the procedure. Although the `String.equals()` with the `instanceof` passes the compiler check, my code with `instanceof` throws an error.

```java
public class StringEqualsCheck {
	public static void main(String[] args) {
		
/* The code below uses String.equals().
*  It throws an error, referring the incompatible type between two arguements.
*  However, String.equals() doesn't throw it even if the primitive type, int was passed.
*/ 

		String str = "abcde";
		char[] chars = new char[] { 'a', 'b', 'c', 'd', 'e'};
		String str2 = String.valueOf(chars);
		
		String intStr = "12345";
		int primInt = 12345;
		Integer ObjInt = 12345;
		
		System.out.println("str equals chars: " + str.equals(chars));
//		the code below throws an error
//		System.out.println("chars instaceof String: " + (chars instanceof String));

	
		System.out.println("str equals str2: " + str.equals(str2));
		System.out.println("str2 instaceof String: " + (str2 instanceof String));
		
		System.out.println("intStr equals primInt: " + intStr.equals(primInt));
//		the code below throws an error
//		System.out.println("primInt instaceof String: " + (primInt instanceof String));

		System.out.println("intStr equals ObjInt: " + intStr.equals(ObjInt));
//		the code below throws an error
//		System.out.println("ObjInt instaceof String: " + (ObjInt instanceof String));

// 		However, the custom method newInstanceOf() doesn't throw the error! 
		System.out.println("chars instaceof String: " + newInstanceOf(chars));
		
/* The code below uses Obejct.equals() to see the
*  Object.equals() does not contain the instanceof operator.
*  It passes the compilerPassCheck() which has a parameter of the type Object!
*/ 

		Object A = new Object();
		A.equals(primInt);
//		the code below throws an error
//		System.out.println(primInt instanceof Object);
		System.out.println(compilerPassCheck(primInt));
		
	}
	
	public static boolean compilerPassCheck(Object obj) {
		return true;
	}
	
	public static boolean newInstanceOf(Object obj) {
		return (obj instanceof String);
	}
}
```

**Tackling Curiosity**
The `instanceof` in the `String.equals()` doens't make the error during the compile, even putting arguments of which type is _int_, _Integer_, _char[]_. I knew that `instanceof` operator (1) throws a compile error when those given two arguements are not with the inhertiance, and (2) returns true when the downcasting from the right to left is possible, else false. Then, why does not`compilerPassCheck(Object obj)` and `newInstanceOf(Object obj)` throw the error? 

case argument: _int_

When _int_ type is given, it first gets auto-boxed. The autoboxing means "converting a primitive value into an object of the corresponding wrapper class."(https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html). It happens when the value is "assigned to a variable of the corresponding wrapper class", as `Integer ObjInt = 12345` is. when  After autoboxing, the _Integer_ type argument is casted into _Object_ which is the superclass of _Integer_. Hence the compile error doesn't occur just like the source code of `String.equals(Object obj)` in Java 17. This is also why the parameter type of `String.equals()` is _Object_, not _String_.

Furthermore, `Object.equals(Object obj)` does not use the `instanceof` operator. It has only one return line, `return (this==obj);`. Remembering this would be helpful as the classes which extends _Object_ would have the method generally.


### Reference

https://stackoverflow.com/questions/28022254/how-comparison-object-and-primitive-with-operator-works-in-java
https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html
https://stackoverflow.com/questions/18575294/java-equals-instanceof-subclass-why-not-call-superclass-equals-instead-of-ma
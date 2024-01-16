## How does Arrays.fill() work?

### Source Code
```java
public static void fill(Object[] a, int fromIndex, int toIndex, Object val)
{
	if (fromIndex > toIndex)
		throw new IllegalArgumentException();
	for (int i = fromIndex; i < toIndex; i++)
		a[i] = val;
}
```

### Explanation

**Start Point**

I frequently use the _Arrays.method()s_ in Java Collection Framework. In problem-solving, there's a need to initialize an array with a specific value. Even sometimes, I manually implement the funtion instead of using _Arrays.fill()_. As I wasn't familiar with how it works, I referred to the Java Oracle 8 docs.

**Tackling Curiosity**

_Arrays.fill()_ method is coded like any manual impelementation of initilizing an array with specific value.

If index parameters `int fromIndex` and `int toIndex` are not passed, they are default to `0` and `a.length` respectively.
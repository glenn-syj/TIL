## Difference between primitive type and reference type in arguments passed

### Test Code

```java

public class ArgumentsTestBetweenPrimitiveAndReference {
	
	static class Pair {
		int x;
		int y;
		
		Pair(int x, int y) {
			this.x = x;
			this.y = y;
		}
	}
	
	public static void main(String[] args) {
		
		int primValue = 0;
		Pair refValue = new Pair(0,0);
		int[] refArray = {1, 2, 3, 4};
		
		// Changing the address itself.
		changeAndPrintPrimitiveArgs(0);
		System.out.printf("After the changeAndPrint Method, During the main, value: %d\n", primValue);
		
		changeAndPrintPairArgs(refValue);
		System.out.printf("After the changeAndPrint Method, During the main, value: %d, %d\n", refValue.x, refValue.y);
		modifyReferenceArgs(refValue);
		System.out.printf("After the modify Method, During the main: %d, %d\n", refValue.x, refValue.y);
		System.out.printf("After the modify Method, During the main: %d\n", refValue.hashCode());
		
		changeAndPrintReferenceArgs(refArray);
		System.out.printf("After the changeAndPrint Method, During the main, value: %s\n", Arrays.toString(refArray));
		modifyReferenceArgs(refArray);
		System.out.printf("After the modify Method, During the main: %s\n", Arrays.toString(refArray));
		System.out.printf("After the modify Method, During the main: %d\n", refArray.hashCode());

	}
	
	public static void changeAndPrintPrimitiveArgs(int primValue) {
		System.out.println("---Args: int---");
		primValue = 10;
		System.out.printf("During the Method: %d\n", primValue);
	}
	
	public static void changeAndPrintPairArgs(Pair refValue) {
		System.out.println("---Args: Pair---");
		System.out.printf("Before the Method, hashCode: %d\n", refValue.hashCode());
		refValue = new Pair(10, 10);
		System.out.printf("During the Method, haschode: %d\n", refValue.hashCode());
		System.out.printf("During the Method value: %d, %d\n", refValue.x, refValue.y);
	}
	
	public static void changeAndPrintReferenceArgs(int[] refValue) {
		System.out.println("---Args: int[]---");
		System.out.printf("Before the Method, hashCode: %d\n", refValue.hashCode());
		refValue = new int[4];
		System.out.printf("During the Method, hashCode: %d\n", refValue.hashCode());
		System.out.printf("During the Method: %s\n", Arrays.toString(refValue));
	}
	
	public static void modifyReferenceArgs(int[] refValue) {
		refValue[0] = 100;
	}
	
	public static void modifyReferenceArgs(Pair refValue) {
		refValue.x = 100;
		refValue.y = 100;
	}
}

```

### Explanation

**Start Point**

In solving a problem through backtracking or traversal, I usually include a method which modifies or tells the value in the traversed position. However, trying to assign a different value happens when the code needs to be iterated or recursed. It also means that I forgot the fundamental principle of Dynamic Programming.

**Tackling Curiosity**

When a primitive type argument is passsed, the value cannot be modified. (Also, interesting fact: the hashcode of `Integer` is the value of itself.) When a reference tpye argument is passed, the value it has can be modified. In both, the re-assinging the value to the argument is not permitted.

*Object.hashCode()* will help understand the code above. After re-assinging in the method, the hash code remains just same as the hash code main() does.
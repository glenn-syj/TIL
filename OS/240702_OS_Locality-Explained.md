# Locality Explained

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/03
- Written By: @glenn-syj

## Explanation

### Background

In the world of the sorting algorithm, the quick-sort is one of the efficient sorting algorithms even if it takes O(N^2) time complexity at the worst case. There was a description that its conquer-and-divide structure ensures the locality of reference. Then, what would the locality mean? It seems to be a word based on some kinds of blocks.

### Tackling Curiosity

**What is locality?**

Locality (of reference) is related to a tendency of a processor. A tendency comes from repetitions. Here the repetitions are generally about a time or a space. In a short timeframe, the same data can be accessed again. In a short length of space, the data near the data lately referenced might be likely to get accessed.

1. Temporal locality

> If at one point a particular memory location is referenced, then it is likely that the same location will be referenced again in the near future
>
>  [wikepedia - Locality_of_reference](https://en.wikipedia.org/wiki/Locality_of_reference)

Let’s think about a for loop in an array. A variable for a value could be `val`, and a variable for an index would be `idx` . The whole codes are below.

```java
int[] array = new int[100000];
int val = 5;

for (int idx = 0; idx < array.length; idx++) {
    array[idx] = idx * val;
}

```

On the code above, the `val` gets referenced each time when the value of `array[idx]` is assigned. The memory location of the same data `val` is repetitively accessed.

Thus, the frequency of a variable or a function being referenced in a short time frame is related to the temporal locality.

One of the common examples using temporal locality in the computer system is LRU(Least Recently Used) Cache.

2. Spatial locality

> If a particular storage location is referenced at a particular time, then it is likely that nearby memory locations will be referenced in the near future 
>
>  [wikepedia - Locality_of_reference](https://en.wikipedia.org/wiki/Locality_of_reference)

The spatial locality could be easily thought to be a matter of distance among the data on the cache. Matrix mutlplication when the large elements over 100,000 exist would be an example. The codes below are psuedo-codes of a matrix multiplicaiton.

```java
public class MatrixMultiplication {
    public static void main(String[] args) {
        int n = 100000; // 행렬의 크기
        int[][] A = new int[n][n];
        int[][] B = new int[n][n];
        int[][] C = new int[n][n];

        // Assume that data are already put into A and B

        // Common matrix mutlplicaiton
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                for (int k = 0; k < n; k++) {
                    C[i][j] += A[i][k] * B[k][j];
                }
            }
        }
    }
}
```

This is a common example. The array `C` would be a result array of the matrix multiplication `A product B`. 

The modified code with efficiency changes, alters the procedure executed between `j` and `k`.

```java
public class MatrixMultiplicationOptimized {
    public static void main(String[] args) {
        int n = 100000;
        int[][] A = new int[n][n];
        int[][] B = new int[n][n];
        int[][] C = new int[n][n];

        // Assume that data are already put into A and B 

        // Improved matrix mutlplicaiton
        for (int i = 0; i < n; i++) {
            for (int k = 0; k < n; k++) { // alter the position of the diemensions between k and j
                for (int j = 0; j < n; j++) {
                    C[i][j] += A[i][k] * B[k][j];
                }
            }
        }
    }
}
```

In the code above, `A[i][k]` stays the same and `B[k][j]` only changes in the dimension of the `k`. This improvement stems from using the spatial locality. 

The common examples considering spatial locality in the computer system is the array data structure and cache CPU.

### References 

https://en.wikipedia.org/wiki/Locality_of_reference

https://www.geeksforgeeks.org/locality-of-reference-and-cache-operation-in-cache-memory/


# Locality Explained

**Disclaimer**

- Last modified(yy/mm/dd): 24/06/01
- Written By: @glenn-syj

## Explanation

### Background

In the world of the sorting algorithm, the quick-sort is one of the efficient sorting algorithms even if it takes O(N^2) time complexity at the worst case. There was a description that its conquer-and-divide structure ensures the locality of reference. Then, what would the locality mean? It seems to be a word based on some kinds of blocks.

### Tackling Curiosity

**What is locality?**

Locality (of reference) is related to a tendency of a processor. A tendency comes from repetitions. Here the repetitions are generally about a time or a space. In a short timeframe, the same data can be accessed again. In a short length of space, the data near the data lately referenced might be likely to get accessed.

1. Temporal locality

Let’s think about a for loop in an array. A variable for a value could be `val`, and a variable for an index would be `idx` . The whole codes are below.

```java
int[] array = new int[1000000];
Integer val = 5;

for (int idx = 0; idx < array.length; idx++) {
    array[idx] = idx * val;
}

```

On the code above, the `val` gets referenced each time when the value of `array[idx]` is assigned. The memory location of the same data `val` is repetitively accessed.

2. Spatial locality

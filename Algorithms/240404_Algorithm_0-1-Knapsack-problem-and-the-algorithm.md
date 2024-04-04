## 0-1 Knapsack problem and the algorithm

### Pseudo code

- Knapsack problem resolving psuedo code
// https://en.wikipedia.org/wiki/Knapsack_problem

```
// Input:
// Values (stored in array v)
// Weights (stored in array w)
// Number of distinct items (n)
// Knapsack capacity (W)
// NOTE: The array "v" and array "w" are assumed to store all relevant values starting at index 1.

array m[0..n, 0..W];
for j from 0 to W do:
    m[0, j] := 0
for i from 1 to n do:
    m[i, 0] := 0

for i from 1 to n do:
    for j from 1 to W do:
        if w[i] > j then:
            m[i, j] := m[i-1, j]
        else:
            m[i, j] := max(m[i-1, j], m[i-1, j-w[i]] + v[i])
```

### Explanation

**Start Point**

The knapsack problem is one of the best problems to practice DP(Dynamic Programming). It has variable types as how the condition and the input dataset of the problem is determined. UKP(unbounded knapsack problem), 0-1 knapsack problem, fragment knapsack problem would be the exmemplar types.

Facing the 0-1 knapsack problem, I figured out the main feature that an item can be put into the knapsack or not. All the items has their own branches by choosing the item or not. What matters is how can we resolve the problem and get solution without tracking all. Checking all possible routes would lead the program to be executed in `O(2^N)` time complexity. It was not easy for me to get the total solution from zero.

**Tackling Curiosity**

1. What `0-1 Knapsack problem` is

The problem suggests the question about a decision-making process. The problem is in the way to get the maximum value while putting items into a knapsack within a weight restriction. How can it be resolved? What to be put and not?

Whta is important in the 0-1 Knapsack is that it cannot be resolved through a greedy approach. Choosing the least efficient item in the view of `value/weight` might be needed. Instead of a greedy algorithm, this binary knapsack problem require to consider DP.

2. Dynamic Programming Solution

The principle resolving 0-1 Knapsack Problem lies in the fact that a maximum value in the moment is used repetitively in the next item. The code below is the java implementation of the pseudo code at the top.

```java
// N: total amount of items
// K: the weight that a knapsack can hold
// when row==0 || col==0: initialized to 0
int[][] dp = new int[N+1][K+1];
		
// allocation for the items before iteration
int[] item;
int valChosen, valNeglect;
int weight, value;

for (int index=1; index<=N; index++) {
    // items: int[N+1][2]
    item = items[index];
    weight = item[0];
    value = item[1];
    
    // currWeight indicates a current weight in the array dp
    for (int currWeight=1; currWeight<=K; currWeight++) {
        
        // when the weight of the item is larger than the given
        if (weight > currWeight) {
            dp[index][currWeight] = dp[index-1][currWeight];
        // when the item can be put into the knapsack
        } else {
            // to compare the two cases: chosen and not chosen
            valAdd = dp[index-1][currWeight-weight] + value;
            valNeglect = dp[index-1][currWeight];
            
            // the optimal value gets used
            dp[index][currWeight] = Math.max(valAdd, valNeglect);
        }
    }
}
```

This approach has the `O(NW)` time complexity and the `O(NW)` space complexity. In the code, it would be noticed that the current choice is branched into two case. 

When an item weighs over the current weight, it should be passed. So the current value is same as the value of the last item before.

When an item can be put into the knapsack, there are two values which need camparison. One is when it is selected, and the other not. Selecting an item means adding a value and subtracting a current weight left in the knapsack. Larger value should be picked. 

3. Further Improvement: Considering the worst case

Even if the time complexity of the code above was told `O(NW)`, the run time is between `O(NW)` and `O(2^N)`. Why the time complexity becomes exponentional in the worst case? Before getting into the worst case, the asymptotic analysis should be done.

Asymptotical approach analyzes the input size, `n` item weights (totally `S`), `n` item values (totally `V`). After the `n` is given, the weight and value of the item either. Here, total item numbers uses `O(log n)` bits.

If the weight of an item exceeds the weight capacity of the knapsack, the item doesn't have to be considered as a candidate.

### References

https://courses.csail.mit.edu/6.006/fall11/rec/rec21_knapsack.pdf

https://en.wikipedia.org/wiki/Knapsack_problem

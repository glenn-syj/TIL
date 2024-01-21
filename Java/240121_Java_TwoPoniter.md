## About Two-Pointer Algorithms

### Source Code


### Explanation

**Start Point**

In LeetCode, there is a tag called _Two Poniter_. It seemed like a simple but effective way to check the subarray or the positions which fit the condition. The O(N^2) time complexity would be down-sized to O(N) time complexity with this techniuqe. Before diving into the LeetCode, I thought I should learn what it is.

**Tackling Curiosity**

The Two-Pointer Algorithm has three paces.

1. Pointer Initialziatoin
They both can be initially placed in the same position like the starting point of the array, or they either can be placed in different positions like the each side of the array.

2. Pointer Movement
If they started movement from the first position(=index 0 of the array), one pointer moves and another remains still. They can move to the middle from the each end too. Also, they can have different offsets for moving.

3. Termination Condition
The termination condition would be reaching the last position of the array or getting the two pointers to face each other. Finding the max/min value or a specific value will be continued till the terminatino condition. 
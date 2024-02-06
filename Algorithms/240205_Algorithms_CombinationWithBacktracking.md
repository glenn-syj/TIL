## Java Code Snippet for Combination

### Source Code

```java

import java.util.ArrayList;
import java.util.List;

public class Combinations {
	
	List<List<Integer>> res = new ArrayList<>();
	
	public static void main(String[] args) {
        Combinations combinations = new Combinations();
        // Here the code means 10_C_4
        List<List<Integer>> result = combinations.combine(10, 4);

        // Code Printing
        for (List<Integer> combination : result) {
            System.out.println(combination);
        }
    }
    

    public List<List<Integer>> combine(int n, int k) {
        if (k <= 0 || n <= 0) return res;
        List<Integer> track = new ArrayList<>();
        backtrack(n, k, 3, track);
        return res;
    }

    private void backtrack(int n, int k, int start, List<Integer> track) {
        // it gets tracked!
        if (k == track.size()) {
            res.add(new ArrayList<>(track));
            return;
        }
        // here the backtracing is applied 
        for (int i = start; i <= n; i++) {
            // element getting selected
            track.add(i);
            backtrack(n, k, i + 1, track);
            // element getting unselected
            track.remove(track.size() - 1);
        }
    }

    
}

```
Code converted to Java From: 
https://labuladong.gitbook.io/algo-en/iii.-algorithmic-thinking/subset_permutation_combination

### Explanation

**Start Point**

During solving a problem using Combinations, I've found out that my appreciation was not perfect. I tried my own version of Combination, however it didn't really fit.

**Tackling Curioisity**

In Combination, the `r` items are chosen from `n` total items. The code above is an implementation of `Combinations` using `Backtracking`. Backtracking is a systematic techniuqe which searched every possible combination.

Backtracking techniuqe is just same as "a traversal process of a decision tree". 

```
result = []
def backtrack(Path, Seletion List):
    if meet the End Conditon:
        result.add(Path)
        return
    
    for seletion in Seletion List:
        select
        backtrack(Path, Seletion List)
        deselect
```

The recursion in the code leads the selection and undoes it after recursion. It would be easy to understand when remembering the flow of method calls. A `backtrack(Path, Selection List)` will make two backtrack again, as long as the end condition is meet.


### Reference

https://www.baeldung.com/cs/k-combinations-recursive-iterative-enumeration

https://nicksma.medium.com/combinations-and-permutations-with-an-intro-to-backtracking-d940683ea9de

https://labuladong.gitbook.io/algo-en/iii.-algorithmic-thinking/subset_permutation_combination

https://www.geeksforgeeks.org/introduction-to-backtracking-data-structure-and-algorithm-tutorials/

https://en.wikipedia.org/wiki/Backtracking
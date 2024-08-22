# Comparator Deep Dive (1): 

**Disclaimer**

- Last modified(yy/mm/dd): 24/08/21
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

Sorting in Java ensures flexibility with Comparator Interface. This interface allows custom sophisticated sorting in OOP. With Java 8 when the Stream API and the lambda expression was introduced, Comparator Interface became much more easy to use. Diving into the world of Comparator would provide chances to core concepts of sorting in Java. Let's start from the Java doc. 

### Tackling Curiosity

#### Comparator, Officially.

Comparator is a functional interface which allows comparation among some collectio of objects. It can be passed to a sort method with a implemented instance. Comparators play an important role in controlling the data structure with natural ordering or without. 

#### Natural Ordering

The natural ordering is a ordering consitent with equals. It means that if and only if `e1.compareTo(e2) == 0` has the same boolean value as `e1.equals(e2)` for every `e1` and `e2`. This ordering could be imposed by implementing `Comparable` interface.

As data structures interface or class like SortedSet and TreeMap is based on the natural ordering, the inconsistent between `compareTo()` method and `equals()` results to an unintentional affect. 

With adding two elements `a` and `b` which are `!a.equals(b) && a.compareTo(b) == 0` to natural order based data strucutres, the latter `add()` would not be successfully increase the size. They are equivalent from their comparator.

How about `a.equals(b) && c.compare(a, b) != 0` with comparator `c`? It results to returning true and increasing the size. They are not equivalent from their comparator.

Also, Java core classes that implements `Comparable` could be said they have natural ordering except `BigDecimal`. Furthermore, even if `Comparable` interface throws NPE with null value, using comparator make it possible to sort with null.

### References

https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Comparator.html

https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Comparable.html

https://stackoverflow.com/questions/9176643/difference-between-natural-ordering-and-total-ordering


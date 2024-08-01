# What is Redis? (1)

**Disclaimer**

- Last modified(yy/mm/dd): 24/08/01
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

In the current project, Redis is used as a cache. The number of view counts and liked counts are managed prirorly in Redis. These data need a fast access and frequent updates.

Although My team have already discussed the pros and the cons of Redis among specific use cases, starting from the bottom would be a great chance to retrospect.

### Tackling Curiosity

**What is Redis?**

What is Redis? This question should be modified when given a specific and a possible failure point. Why Redis must be used in the project? In what way you need Redis? Some posts call Redis a NoSQL DBMS, others an in-memmory database. Also Cache, key-value store, event stream, ...

All these names around Redis are valid from its technical architecture and the usage. Then, it would be reasonable that the architectural features should be pointed priorly.

### References

https://docs.spring.io/spring-security/reference/servlet/authorization/architecture.html

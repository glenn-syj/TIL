# What is Cache? (1)

**Disclaimer**

- Last modified(yy/mm/dd): 24/08/26
- Written By: @glenn-syj

## Explanation

### Background

Cache is a familiar and frequently used word in the Computer Science. When reading Redis docs, it says that Redis can be used as a cache. NginX also describes one of its features to caching a static resource. Then, what is cache? It sounds like a magic word for storing and fetching data. Then, it would be a time to deep dive into the world of cache.

### Tackling Curiosity

#### The basic concept

Let's start with a basic concept of cache. Wikipedia describes cache in computing.

> a hardware or software component that stores data so that future requests for that data can be served faster

This description shows important features of cache. First, it stores data. Second, it assumes the future requests which could be repetitive. Third, cache itself serves data (in a faster way).

Cache plays a role of a data storage. Above the fact that there are lots of caches level by level and purpose by purpose, the caches always aim to enhance the system performance. Reducing the latency from accessing data is the most important key. Another important thing to notice here is that caching repetitive data would be only a kind of caching. This is called Hot Data Caching or Frequency Based Caching. There are also strategies based on other criteria like time-based caching, priority-based caching, pre-caching, and context-aware caching.

#### The trade-off in Cache

### References

https://learn.microsoft.com/en-us/dotnet/framework/network-programming/time-based-cache-policies

# What is Cache?

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

Caching is not the silver bullet for sure. While dramatically improving system performance, introducing cache has a potential complexity and trade-offs. It means that caching strategies should be considered in a sophisticated way. These are the kinds of trade-ofss in cache.

- Memory Usage vs. Performance

Caching frequently accessed data comes with consuming memory resources. For Example, an environment which has a limited memory may cause suffering to other parts for a resource contention. It affects the whole system, harming the system performance.

- Data Freshness vs. Speed

Cached data might be stale compared to the latest information in the primary data storage. When real-time data is crucial, the trade-off should be adjusted to fulfill the own purpose. It means that how much data inconsistency the service can endure should be considered.

- Cache Size vs. Cache Misses

A smaller cache results to more cache misses, while a larger one more memory usage. When there is no requested data in cache, the data should be fetched from the original data sources. However, the more memory usage it needs, the more expensive cost it requires.

### References

https://learn.microsoft.com/en-us/dotnet/framework/network-programming/time-based-cache-policies

https://stackoverflow.com/questions/48589218/what-are-the-trade-offs-of-larger-cache-memories-could-we-use-one-to-replace-s

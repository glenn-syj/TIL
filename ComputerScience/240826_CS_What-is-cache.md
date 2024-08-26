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

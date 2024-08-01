# What is Redis? (1): The Concept

**Disclaimer**

- Last modified(yy/mm/dd): 24/08/01
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

In the current project, Redis is used as a cache. The number of view counts and liked counts are managed prirorly in Redis. These data need a fast access and frequent updates.

Although My team have already discussed the pros and the cons of Redis among specific use cases, starting from the bottom would be a great chance to retrospect.

### Tackling Curiosity

**What is Redis?**

What is Redis? REmote DIctionary Server? This question should be modified when given a specific and a possible failure point. Why Redis must be used in the project? In what way you need Redis? Some posts call Redis a NoSQL DBMS, others an in-memmory database. Also Cache, key-value store, event stream, message broker, ...

All these names around Redis are valid from its technical architecture and the usage. Then, it would be reasonable that the architectural purpose should be pointed priorly.

**Redis from What?**

Redis docs introduce three purposes of using Redis in Quick Starts part. One is the data structure store, another is a document database, and the other is a vector database. Despite of the kindful addresses, I want to start from the questions in FAQ session.

_Question 1_

> Why does Redis keep its entire dataset in memory?

_Answer 1_

> In the past the Redis developers experimented with Virtual Memory and other systems in order to allow larger than RAM datasets, but after all we are very happy if we can do one thing well: data served from memory, disk used for storage. So for now there are no plans to create an on disk backend for Redis. Most of what Redis is, after all, a direct result of its current design. (...)

Redis is defenitely an in-memory databas here. Redis draws a picture of "data served from memory, disk used for storage." It ensures a low latency and a high throughput for real-time data processing. To , RDB(Redis Database) and AOF(Append Only File) supports data restoration and consistency. These features seem to aim the real-time application. Let's move on to the next FAQ.

_Question 2_

> Why did Salvatore Sanfilippo start the Redis project?

_Answer 2_

> Salvatore originally created Redis to scale [LLOOGG](https://github.com/antirez/lloogg), a real-time log analysis tool. But after getting the basic Redis server working, he decided to share the work with other people and turn Redis into an open source project.

On the README of [LLOOGG](https://github.com/antirez/lloogg), the project was described as a realtime log analyzer web app for displaying the accesses on the website. Its main features turned to tracking adsense clicks (they were removed later, as Sanfilippo said). In the tracking, the user patterns got captured and aggreagted. The story behind Redis sounds quite interesting.

Now I see why it had served as a Redis test bed. From the first time, Redis seems to get developed in serving a low-latency real-time web application. `Hyperloglog`, a probabilistic data structure in Redis commonly used for a website analytics is not far from this viewpoint.

### References

https://redis.io/docs/latest/develop/get-started/faq/
https://github.com/antirez/lloogg
https://www.ibm.com/topics/redis

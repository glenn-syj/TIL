# Auto Increment versus UUID (1)

**Disclaimer**

- Last modified(yy/mm/dd): 24/05/26
- Written By: @glenn-syj


## Expalanation

### Start Point

In my project, I chose to assign a surrogate key as a primary key to entities. Advantages of the surrogate key was proper to the project interface. Then, what kind of surrogate key should I take? The auto increment provided by MySQL was familiar. It was a candidate. The other is UUID. MySQL also serves a function for creating UUID. Although there were other alternatives like ULID, TSID or Snowflake, it would be a better start to dive into the world of these popular ones. The convenience of these was also considered.

### Tackling Curioisity

When learning MySQL, the PK is usually set to the int and given the `AUTO_INCREMENT` attribute. This attribute lets MySQL assign sequential numbers automatically in the table creation and insertion. This article would not explain how to use it or any other tutorial. Instead, the more theoretical exploration would be needed. Of course, the benefits within the surrogate key cannot be the main point here.

**AUTO_INCREMENT**

- Advantages

1. Performance with the InnoDB Engine

  In MySQL, the InnoDB engine is implemented since version 5.5 instead of MyISAM. It is now the default engine in verison 8. The most notable part is the B-tree Indexes feature being provided.

  B-tree Index is a self-balancing tree sturucture of which every  length from the root to the leaf node is same. Any last record from the auto increment insertion would be placed in the last part of the table. It ensures the great performance in the insertion and I/O speed.

  The records in MySQL with the B-tree Index are stored and ordered by the PK. It means that (1) it shows better performance and (2) ouccupies less storage with INT or BIGINT compared to UUID.

- Disadvantages

1. Cannot be used as an access path

  Auto increment keys are easily predicted. It means a vulnerability from any threaten from crackers or other competitive companies.

  Imagine a service has assigned an auto increment id 100 to a latest post. What would be next? It would be 101. It is so predictable enough to catch the flow and the usage of the service.

2. Deadlock

  MySQL uses a mechanism called Auto-increment lock. It is introudced to safely generate the auto-increment values. InnoDB provides row-level locking. While table-level locking does not allow approaches to the table itself being used, row-level lock allow approaches to the other rows not being used in the same table. 

  The row-level lock could lead to a deadlcok. It is a situation the multiple transactions waits for one another being finished to access the locked resource in the row-level lock. The table-lock does not cause the deadlock in the same situation.

3. Replication Orphans

  Replications in databses are supposed to happen in a multi-server environment. Replication suggests that changes in the primary master server are propagted to the secondary replica servers which are basically read-only for load balancing, backup or select.

  Replicaiton orphans are created when the connetion between those are lost. The replica would not be synchronized and  it get to overwrite itself. It compromises data consistency.

  If the replica table uses auto-increment, the auto-increment keys are still generated after the connection lost. When reconnected and synced, the auto-increment keys between these would be conflicted.  

  This might be mitigated through offset. It divides the offset among the servers. Server1 might have values 1, 4, 7, ... and Server2 might have 2, 5, 8, ... However, this strategy does not ensure the scalability.

4. Not unique when sharding

  Roughly speaking, sharding is a kind of horizontal partitioning data architecture. A shard means a partition seperated. While horizontal partitioning splits tables within a single instance of a schema, sharding does the same thing across multiple schemas. It is useful when a large traffic occurs.

  With auto-increment, merging shards would be error-prone due to their unique keys not being unique anymore. Yet the offset strategy might be imlemented here, it does not seem to ensure the scalability again. 

### Conclusion

The auto-increment key defenitely occupies an advantageous position when considering performance. However, would the peformance signficantly matters compared to UUID? This question needs to be resolved.

Furthermore, its usage seems to be restricted the predictable feature and the problems from the distributed server environment.

### References

https://dev.mysql.com/doc/refman/8.0/en/example-auto-increment.html

https://dev.mysql.com/doc/refman/8.0/en/innodb-introduction.html

https://en.wikipedia.org/wiki/B-tree

https://www.pythian.com/blog/business-insights/case-auto-increment-mysql

https://news.ycombinator.com/item?id=10632880

https://dev.mysql.com/doc/refman/8.0/en/innodb-locking.html#innodb-auto-inc-locks

https://dev.mysql.com/doc/refman/8.0/en/innodb-deadlocks.html

https://medium.com/@sandeep4.verma/system-design-distributed-global-unique-id-generation-d6a440cc8e5

https://en.wikipedia.org/wiki/Shard_(database_architecture)

https://hazelcast.com/glossary/sharding/
# Auto Increment versus UUID (2)

**Disclaimer**

- Last modified(yy/mm/dd): 24/05/29
- Written By: @glenn-syj


## Expalanation

### Start Point

In the last article `Auto Increment versus UUID (1)`, the benfits and drawbacks of the auto-increment primary key were explored. Then, it's time to dive into the world of UUID. It would be an explain for why my project chose UUID as a primary key of entities.

### Tackling Curioisity

What is an UUID? The benefits UUID has come from its own definition and structure. UUID means for Universally Unique IDentifier. It usually consists of 128 bits string. Although there are many versions of UUID known, the main candidates were UUID-v1 and UUID-v4. The UUID-v1 is based on the current time and MAC address or the node. The UUID v-4 is a randomly generated UUID. The latter sounds better when considering the security. However, I chose UUID-v1 as the project was run in the local dev environment, without deployment. However,  Lines below would be the reason why I chose.

**UUID**

- Advantages

1. Ensured Uniqueness

  UUIDs are so unique that it is scarce for several IDs to have same value and collide one another. The uniqueness ensured leads to the efficiency and the scalability in the merging schemas splitted. These features let UUID become a efficient candidate for distributed systems like sharding.

2. No Buisness Data Disclosed

  As UUIDs also makes it almost impossible to predict the next value, they do not reveal the information business related. This prevents the service from being attacked by malicious trials and other buisness threaten.

3. Removing bottlneck

  UUID would be helpful in the aspect of removing bottlenecks made from sequence generations. Sequential IDs might have a bottleneck under high load or distributed envirionments. However, UUID can be generated seperately. Also, it means that there would be no table locks when using UUID.

- Disadvantages

1. Overheads from Indexing

  When UUID being not well sequenced, the database performance in MySQL would be harmed. The UUID v-1 and The UUID v-4 cannot avoid this drawback. This stems from the B-Tree Index feature of MySQL. However, this could be mitigated with handling and reordering the UUID v-1.

2. Requirements for large space

  UUID requires a space of 128 bit, therefore 16 byte size, 36 Characters. This is sigificantly larger than INT or even BIGINT type. These are usually mentioned as a defect when using UUID as a primary key. However, it can be stored as 16 byte binary type.

3. Readability

  The complexity from UUID generation leads to the poor human readability. It makes debugging and logging in the development challenging. Even though this seems like a little defect, a little difference might take a large time when trouble shooting. 

### Conclusion

UUID also has pros and cons. There are no silver bullet in deciding the PK. The important relys on the environment and the schema. However, the sync with distributed environments which stems from the uniqueness should be mentioned. Therefore, what's important is that the UUID ensures the scalability in my view. In the next article, I would like to explain my PK plan when using UUID.

### References

https://en.wikipedia.org/wiki/Universally_unique_identifier#:~:text=A%20Universally%20Unique%20Identifier%20(UUID,Acronym

https://www.uuidtools.com/uuid-versions-explained

https://dev.mysql.com/doc/refman/8.0/en/innodb-introduction.html

https://en.wikipedia.org/wiki/B-tree

https://www.pythian.com/blog/business-insights/case-auto-increment-mysql

https://news.ycombinator.com/item?id=10632880

https://www.baeldung.com/uuid-vs-sequential-id-as-primary-key

https://dev.mysql.com/doc/refman/8.0/en/innodb-deadlocks.html

https://medium.com/@sandeep4.verma/system-design-distributed-global-unique-id-generation-d6a440cc8e5

https://tomharrisonjr.com/uuid-or-guid-as-primary-keys-be-careful-7b2aa3dcb439

https://en.wikipedia.org/wiki/Shard_(database_architecture)

https://hazelcast.com/glossary/sharding/

https://medium.com/@hkhantanoli/the-problem-with-using-a-uuid-primary-key-in-mysql-ea2c1bd44269
# UUID Strategies

**Disclaimer**

- Last modified(yy/mm/dd): 24/06/01
- Written By: @glenn-syj


## Expalanation

### Start Point

In my articles related to deciding the primary key type, there were much more advantages in the UUID over the auto-increment. However, UUIDs also have disadvantages like overheads from indexing and requirements for storage. As MySQL with InnoDB engine uses B-Tree Index, the overheads might affect the write performance signficantly when the large data exist. Then, how can UUID become more effective in MySQL?

### Tackling Curioisity

What to remember is two things. First, make UUIDs sequential. Second, lower the size of data each column with UUID in the record. These strategies fulfills the goal where the improvements of a better performance and lower storage size.

**Strategies**

1. BINARY(16) instead of CHAR(36)

Any version of the UUID occupies 36 bytes of space when stored in char type. It consumes 28 bytes more than the BIGINT type. However, BINARY(16) needs only 8 bytes more. Even though the gap is still not small, each storage with the PK got 20 bytes saved. The change in the type also affects performances in indexing and searching.

2. Handling UUID v-1

UUID v-1 generates a unique ID from the MAC address and current timestamp with a monotonic counter. The UUID v-1 value consists of five parts, `TimeStamp (low time) - TimeStamp (mid time) - TimeStamp (high time) & UUID Version - Clock sequence - Node Identifier`. As the low time timestamp is sequentially countered first, it should be in the last position among the timestamps. So, the ordered UUID v-1 would be `Timestamp (high time) - Timestamp (mid time) - Timestamp (low time) - ...`.

As the node identifier is decided by the network and MAC address, the security issues occur. However, this project had more importance on comprehending UUID and MySQL. This issues would be featured in my articles later.

### Conclusion

### References

https://stackoverflow.com/questions/28251144/inserting-and-selecting-uuids-as-binary16

https://stackoverflow.com/questions/20342058/which-uuid-version-to-use

https://www.percona.com/blog/store-uuid-optimized-way/
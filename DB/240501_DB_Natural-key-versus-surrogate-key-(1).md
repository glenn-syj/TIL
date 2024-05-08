# Natural Key vs. Surrogate Key (1)

**Disclaimer**

- Last modified: 24/05/08
- Written By: @glenn-syj


## Expalanation

### Start Point

On writing an E-R Diagram during a project, there was a consistent problem with deciding what should be a primary key for identifying. As the `user` table includes the `email` column which should not be dupulicated, the first approach was to use the email as a primary key. However, what about email being changed or deprecated? As an email is related to other platforms, it has a vulnerability which stems from the original email. It could be deleted, modified, and lost in the original website. Then, what would be the alternative?

### Tackling Curioisity

My concern was a major and long-last topic in the database section. There were two kinds of primary key in the view of the meaning. One is natural key, and the other is a surrogate key.

**Natural Key**

A natural key is a unique key formed of meaningful attributes related in the external world business outisde the database. It serves a unique identification and imposes a unique constraint to the database. 

- Advantages

1. Save disk space

As key values have business meaning and already in the data, no extra value is required to make a extra key as a primary key. This leads to a less disk space it occupies.

2. Enforcement of data quality

The already-exist feature of natural key ensures the data quality to be simplified. The uniqueness could be easily achieved just with the attributes the entity has either.

3. Join Efficiency

As join columns have meaning, the disk I/O join statement can be reduced either. It does not have to perform extra reads.

- Disadvantages

1. Cost on the changeability

The natural key is changeable even if it looks consistent. When the primary key needs to be modified or replaced, data consistency and referential integrity can be threatend. The change might lead the whole system to be reconsidered. 

2. Difficulty in mutiple attributes

What if a single natural attribute is not enough to identify an entity? Then, the key should be composited. A natural composite key consists of mulitple meaningful attributes. However, this 

### References

https://en.wikipedia.org/wiki/Natural_key#:~:text=A%20natural%20key%20(also%20known,domain%20or%20domain%20of%20discourse).

https://www.ibm.com/docs/en/db2/10.5?topic=operators-natural-keys

https://www.sqlservercentral.com/articles/using-a-surrogate-vs-natural-key

https://stackoverflow.com/questions/63090/surrogate-vs-natural-business-keys
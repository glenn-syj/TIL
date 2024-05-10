# Natural Key vs. Surrogate Key (2)

**Disclaimer**

- Last modified: 24/05/10
- Written By: @glenn-syj


## Expalanation

### Start Point

In the previous article, I have researched what natrual key is. The benfits and drawbacks of the natural key was due to its business or entity related features. Then what about the surrogate key? This article features the advantages and disadvantages from using surrogate key. Furthermore, it would be an explanation for why I decided to use a surrogate key as a primary key. Before reading, it has to be disclaimed that an ongoing project with a team mate is in the agile with daily scrums. Also, the databsae environment is `MySQL` with `InnoDB`.

Then, what made me to draw the ERD table entity with the surrogate primary key instead of natural (compound) primary key? Let's dive into the topic.

### Tackling Curioisity

On deciding the type of the primary key, I considered the entity realtionship like 1:1, N:1, N:M. The primary goals on the backend were to provide CRUD REST API, searching which includes the tag search, and managing users. The secondary goal was to develop the functions related in those. My main concern was flexibility in the table, as I hoped to develop the project or to make a project from it continously. Using surrogate key effectively fulfills the goals.

**Surrogate Key**

A surrogate key is a unique key identifying the entity in the modeling. While a natural key data is derived from the data related in an entity, a surrogate key itself is not meaningful. This is why it is also called technical key or synthetic key.

- Advantages

1. Stability

Surrogate keys do not change or modified. A natural key data always has a risk to be replaced even in the most ensurable case. This feature becomes more important in the view of a foreign key. When the primary key used as a foreing key in other tables has a change, the cascading updates would be needed. This could be expensive.

2. Performance

The performance in using a surrogate key would rely on, of course, its data type. Using a compact data type as a single surrogate key enhances the performance compared to a compound key. A primary key in many records would be checked when inserting happens.

3. Compatiblity

Object-relational mapping systems like Hibernate are compatible with a surrogate key like `GUID` or integer. Database application development systems and drivers, either.

- Disadvantages

1. Disassociation

A surrogate key has no relationship to the real world data. It means that the surrogate key value is disassociated. Also, the referential integrity will be compromised. To prevent, the combinatnion of the natural key for identification should be considered. 

2. Wasted space

A surrogate key requires extra storage space as it neeeds an extra column. It also means that the surrogate key increases the cost of scanning and inserting. The join operations would make more wasted disk space, either.

3. Data transfer to other systems

Although the difficulty in the database transfer relys on the database schema, a surrogate key might make suffer in data migration to other systems.

The first disadvantage, the disassociation actually affects this disadvantage. The identical schemas can have different records only diffrent in a surrogate key, but not in a business sense. The develop system and the test system would be a appropriate exmaple. Here, the mitigation through not exporting the surrogate keys is needed here. 

### Conclusion

As my ongoing project is expected to go through lots of changes during the development, I chose to use a surrogate key as a primary key. Also when thinking about developing projects further, handling surrogate keys would be a great experience. 

Then, considering and deciding the surrogate key types like `UUID`, `ULID`, `Snowflake id` and auto_increment in MySQL with optimization is going to be my next step.

### References

https://en.wikipedia.org/wiki/Surrogate_key#:~:text=A%20surrogate%20key%20(or%20synthetic,natural%20(or%20business)%20key.

https://www.ibm.com/docs/en/db2/10.5?topic=operators-surrogate-keys

https://www.sqlservercentral.com/articles/using-a-surrogate-vs-natural-key

https://community.spiceworks.com/t/drawbacks-of-generated-surrogate-keys/928815

https://stackoverflow.com/questions/63090/surrogate-vs-natural-business-keys
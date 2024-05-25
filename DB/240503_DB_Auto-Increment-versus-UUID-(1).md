# Auto Increment versus UUID (1)

**Disclaimer**

- Last modified(yy/mm/dd): 24/05/25
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

  B-tree Index is a balanced tree sturucture of which every  length from the root to the leaf node is same. Any last record from the auto increment insertion would be placed in the last part of the table. It assures the performance in the insertion and I/O speed.

  The records in MySQL with the B-tree Index  are stored ordered by the PK.


### Conclusion


### References

https://dev.mysql.com/doc/refman/8.0/en/example-auto-increment.html

https://dev.mysql.com/doc/refman/8.0/en/innodb-introduction.html

https://news.ycombinator.com/item?id=10632880

https://medium.com/@sandeep4.verma/system-design-distributed-global-unique-id-generation-d6a440cc8e5
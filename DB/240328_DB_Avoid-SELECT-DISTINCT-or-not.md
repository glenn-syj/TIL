## Avoid SELECT DISTINCT or not

**Last Modified: 2024-03-29**
**Written By: @glenn-syj**

### Source Code

```sql
https://stackoverflow.com/questions/581521/whats-faster-select-distinct-or-group-by-in-mysql
CREATE TABLE users (
  id int(10) unsigned NOT NULL auto_increment,
  name varchar(255) NOT NULL,
  profession varchar(255) NOT NULL,
  employer varchar(255) NOT NULL,
  PRIMARY KEY  (id)
)

SELECT DISTINCT u.profession FROM users u;
SELECT u.profession FROM users u GROUP BY u.profession;
```

### Explanation

**Start Point**

As writing the query for fetching dummy data, I frequently used `SELECT DISTINCT` query. Lots of starters of the RDBMS learner would be in the same shoes. Learning through MySQL official guide and Stack Overflow leads them to the mystic conclusion, which says that we should avoid using `SELECT DISTINCT`. Even though I said it “mystic” for the ignorance of inner mechanisms, the performance being slowed seems to support the saying. Then, what kinds of overheads does it make?

**Curiosity Tackled**

1. `DISTINCT` and `GROUP BY`

The MySQL official guide devote a page of `SELECT`  optimization chapter into a `DISTINCT` optimization. It says that a `DISTNCT` clause is essentially equivalent to `GROUP BY` , and this clause is the special case of that. It implies that (1) `DISTINCT` is similar to `GROUP BY` clause and (2) `DISTINCT` clause acts differently in the specific cases. What would be faster then?

The tedious but always important answer is needed. The situation and the data decides the performance. If there is column selected, the `DISTINCT` would be faster. With the single column select query, it would be the same when there is an index on the table. However, selecting more than one column would be processed much faster in `GROUP BY` queries. Here the `DISTINCT` becomes computationally expensive.

The commonality, which seems to eliminate duplication always haunts the RDBMS starters. Although It won’t be necessary to say that `GROUP BY` is used to do aggregation and `DISTINCT` is used to retrieve distinct records, those are used in the wish for removing duplicates from the result. 

2. Reconsider `DISTINCT`

A mere comparison between `DISTINCT` and `GROUP BY` is only a half-baked approach without considering the circumstances. Using `DISTINCT` with no consideration of its pros and cons doesn’t make sense too.

The most important point that discussions around `DISTINCT` suggest is about the data model itself. If there is a frequent needs to write select query with `DISTINCT` , it might be the sign of the data integrity being damaged. The probability that join conditions are not optimized or the database design is structured not in the way efficient.

Thus, it would not make sense that `DISTINCT` itself is avoided. The problem happens or lies in the circumstance which demands queries with `DISTINCT`.

### Reference

https://dev.mysql.com/doc/refman/8.0/en/distinct-optimization.html

https://stackoverflow.com/questions/33651429/should-i-use-distinct-in-my-queries

https://stackoverflow.com/questions/5341276/sql-distinct-keyword-bogs-down-performance

https://www.linkedin.com/pulse/hidden-costs-using-select-distinct-unnecessarily-james-shelley/
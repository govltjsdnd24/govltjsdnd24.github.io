---
categories: [ Study, PostgreSQL ]
tags: [ rdbms ] 
---

This post, I would like to talk about PostgreSQL, a popular RDBMS used alongside MySQL, MSSQL, and Oracle. Do keep in mind that 
the latter are commercial softwares and therefore have to be paid for prior to usage. PostgreSQL, if put in contrast with MySQL, are more suitable for projects wherein there exists multple writes and relatively more complex queries. MySQL is better for general purpose, as it has a simpler syntax and are fit for beginners. 

## Difference between MySQL and PostgreSQL

Apart from the one I explained in the introduction, there are even more differences between the two RDBMS.

1.  MySQL is purely a relation-based DB whilst in PostgreSQL, entries can be saved in Object format. Like Objects in java, there exists Parent-Child relations and concept of inheritance here.

2.  The layout of these two RDBMS are different. MySQL has a merged concept of database and schema, and use the two terms interchangeably; PostgreSQL, like Oracle, consider the two terms distinguishable, and has a such nested structure: Database as a parent, Schema as children, Tables as grand-children.
This means that, although in MySQL, a user must type the "USE" keyword to select the database within the SQL editor, in PostgreSQL, a direct connection is made with a specific database when establishing link. So, if you are using psql command-line tool, then you would be using a command like this:
```r
\c database_name
```

3. There is a contrast in the 'depth' of the database features that they provide. For example, in MySQL, only a reqular View is available, while PostgreSQL supplies a more advanced View option; for example, one could compute calculations of some columns beforehand to improve the overall efficiency. 
This kind of freedom is also true for stored procedures and triggers. MySQL's stored procedures are just replicas of sql queries or codes while PostgreSQL's stored procedures support language other than SQL. MySQL enables BEFORE and AFTER TRIGGERS for INSERT, UPDATE, and DELETE while PostgreSQL allows a more complex function execution through PostgreSQL's versatile INSTEAD OF keyword.

Other than these concrete differences, there are even more conceptual dissimilarity. Performance-wise, MySQL offers better effectiveness for simple read activities while PostgreSQL is more suitable for high-volume write actions. PostgreSQL also provides a wider variety of Data Types than its counterpart. 

However, with almost all of the differences favoring PostgreSQL, what would be the reason for MySQL's dominance in the non-commercial RDBMS market? The answer is simple: ease of use. Developers who don't want to go in details about the database would choose to use MySQL which provides similar performance for a simpler grammar. However, with so many advantages PostgreSQL flaunts, there is no reason to refrain from using it for developers who wish to acquaint themselves with DBs.

## Difference in their syntax

Although the syntax of MySQL and PostgreSQL are quite similar there are differences that reside in even the simplest procecures. We will go over them with haste.

### AUTO_INCREMENT

When creating tables, MySQL uses AUTO_INCREMENT property to make the int value increase by 1 each time a row is added. However, PostgreSQL takes this to another step by allowing two features: SERIAL and SEQUENCE.

SERIAL is used in the place of data type. It is not necessarily a data type by itself, but rather a derivative of INTEGER. It does exactly what AUTO_INCREMENT does.

SEQUENCE on the other hand is a database object dedicated to implement extensive increment functionality.
Let's first look at the syntax:

```SQL
CREATE SEQUENCE "SEQUENCE_ID"
    INCREMENT #
    START #
    MINVALUE #
    MAXVALUE #
    CACHE #;
```

As you can see, an overwhelming number of options--which is self explanatory--are available for SEQUENCE. In case you are curious, CACHE allows certain number of sequence values to be allocated prior to actual assignment. 

### OFFSET, LIMIT

OFFSET and LIMIT are often used together. The former defines the starting point and the latter the ending iteration. While in MySQL, LIMIT comes in front of OFFSET, in PostgreSQL, OFFSET comes before LIMIT.
```SQL
OFFSET "VALUE" LIMIT "VALUE"
```

###  Modification

There are also some differences present in the ALTER TABLE command as well.

1. Column Type Modification

MySQL
``` SQL
ALTER TABLE "TABLE" MODIFY "COLUMN" "DATA_TYPE";
```
PostgreSQL
``` SQL
ALTER TABLE "table_name" ALTER COLUMN "COLUMN" TYPE "DATA_TYPE";
```

2. Column Renaming

MySQL
``` SQL
ALTER TABLE "TABLE" CHANGE "OLD_COLUMN" "NEW_COLUMN" "DATA_TYPE";
```
PostgreSQL
``` SQL
ALTER TABLE "TABLE" RENAME COLUMN "OLD_COLUMN" TO "NEW_COLUMN";
```

There are much to cover, but for this post I will be stopping here, for the topic is way to vast to summarize in a single article.

## Conclusion

Because of its ease of use, MySQL has secured its place in the RDBMS ranking for a long time. However, nowadays, PostgreSQL is slowly gaining a noticeable amount of increase in its usage. This is due to its expanding sets of usability. A good example of this is Aurora PostgreSQL in AWS RDS; Aurora PostgreSQL has recently attained the capability of being used as a knowledge base for the generative AI available in AWS. The popularity of PostgreSQL is steadily increasing, and will be able to secure its place in the top tier of RDBMS in a near future.

## Reference

[https://www.postgresql.org/docs/](https://www.postgresql.org/docs/)




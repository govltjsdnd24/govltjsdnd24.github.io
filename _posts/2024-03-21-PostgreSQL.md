---
categories: [ Study, PostgreSQL]
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

3. 


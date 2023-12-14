# DBMS

1)  What are databases?
Collection of related data.
    - It helps to solve the problem of redundancy and inconsistency
    - Easy app integration
     
2) What is DBMS?
- DBMS is a `Management system software` that gives us the functionality to easily query, access, process some data in the  databases. 
- The goal of DBMS is that the retrieval and the storage of the data from the user to the stored database is as smooth as possible.
- MySQL, PgSQL, SQLlite are examples of DMBS, using this we can add, delete, retrive anything with the data. All these software understand one common language i.e *SQL*. So all DBMS can be interacted using SQL
Note: There are few DBMS which doesn't understand SQL, that we will discuss later

3) What is SQL?
- Structured Query Language, is taken as a specs to all the DBMS and they implement all of the sql queries with some pinch of salt. For exmaple: There are few features that are given in the official documentation of SQL but the DBMS might not follow every single the standards. 

4) Features of DBMS:
- Data sharing is easy 
- We can put *constrains* on the type of data that needs to be put in, for example if we expect integer and it gets string it'll throw error or let's say we expect string but of 20 characters or less we achieve this using DBMS

5) RDBMS:
- In RDBMS we store our data in form of tables.
        - the entire table represent entities
        - the columns actually represent the property of the entities
        - the rows represent represent actual data of an entity. 
So, whenever we store any data it creates a new row and whenever we store a new property we create a column, and whenever we create a new set of entities we create a new table


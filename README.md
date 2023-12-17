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
    - It's a declarative language.
    - Case in-sensetive

4) Features of DBMS:
    - Data sharing is easy 
    - We can put `constrains` on the type of data that needs to be put in, for example if we expect integer and it gets string it'll throw error or let's say we expect string but of 20 characters or less we achieve this using DBMS

5) RDBMS:

    In RDBMS we store our data in form of tables.
    - the entire table represent entities
    - the columns actually represent the property of the entities
    - the rows represent represent actual data of an entity. So, whenever we store any data it creates a new row and whenever we store a new property we create a column, and whenever we create a new set of entities we create a new table.


- To Install MYSQL in your local machine (in windows) you follow this [tutorial](https://www.youtube.com/watch?v=hbNRULz6GFA)

### **SQL Queruies**
----
*Note* Every Valid MySQL command ends with semicolon`;`
- To show all the databases present in your system

```sql
SHOW DATABASES;
```

- To clear console
```sql
\! clear;
```

- To create a Database
```sql
CREATE DATABASE NameOfDatabase;
ex: CREATE DATABASE MovieDB;
```
- To delete a Database
```sql
DROP DATABASE NameOfDatabase;
ex: DROP DATABASE MovieDB
```

- To add a Table in a particular Database
```sql
  USE NameOfDatabase
  CREATE TABLE TableName (ColumnName1 Datatype1(sizeOfDatatype1), ColumnName2 Datatype2(sizeOfDatatype2), ColumnName3 Datatype3(sizeOfDatatype3));

  ex: USE MovieDB;
  CREATE TABLE Movies (MovieName VARCHAR(50), Rating INT(10), RELEASE_DATE DATE);
```

- To see the table attributes
```
desc TableName;
ex: desc Movies;
```

- Add data in the table.
```sql
INSERT INTO TableName (ColumnName1, ColumnName2, ColumnName3) (ValueForColumn1, ValueForColumn2, ValueForColumn2);
ex: INSERT INTO Movies (MovieName, Rating, Release_date) Values ("Avengers", 4, "2023-12-16");
//To insert multiple rows together:
INSERT INTO Movies (MovieName, Rating, Release_date) Values ("Avengers", 4, "2023-12-16"), ("Thor the dark side", 3, "2020-11-06"), ("War", 4, "2020-05-04");
```

- To see all the columns data in the table
```sql
 select * from movies;
```
- To see data of a particular column
```sql
 select columnName from tablename;
 example: select rating from movies;
```

- To see data based on condition
```sql
SELECT * FROM TableName WHERE COLUMNNAME{LogicalOperator}{CONDITION}
SELECT * from Movies where Rating>4;
```

- Delete any entry from table
```sql
Delete FROM TableName WHERE COLUMNNAME = "Value";
Ex: Delete FROM Movies WHERE MovieName = "WAR";
```

- Update any entry in the table
```sql
UPDATE TableName set ColumnName = Value  WHERE COLUMNNAME = "Value";
Ex: UPDATE Movies set rating = 5  WHERE MOvieName = "Avengers";
```

- Delete the entire table

```sql
DROP Table TableName  
Ex: DROP Table Movies;  
```

- To see all the tables in a database 

```sql
Show tables; 
```

### **Normalisation and DB Design**
----

- What is database schema?
    - Schema as a term stands for *blueprint*.
    - So, database schema is a *blueprint* of an actual database that we will create. How we will store data, structures of table etc is defined inside it.
    - In the database schema when we are actually designing it we don't just tell the tables, we also explain how the tables are connected, what's the relation between different tables.
    - These schema are first of all designed in pen and paper to understand all the nuances that needs to be handled.
    - In modern backend framework(ex: RubyOnrails, expressJs), generally there's a feature where we can define a schema in our backend code and the framework will automatically helps us to create a database out of it, so we manually don't have to go and create database, tables etc.

*Note: In RDBMS we refer column as attributes and rows as tuples*

- What is functional dependency?
    - Functional dependency defines relationship between two attributes. To denote functional dependency between two attributes we use `->`. So, if we write X -> Y that means Y is functionally dependent on X and for every value of X we can uniquely identify Y.

    - Is there any way in dbms that we can verify the functional dependency without making any attribute as the primary key? `Ans:` There doesn't exist any way.

    - Now there's an keyword as `ASSERTION` that means *validation* that exist in SQL documentation which helps us in understanding functional dependency but most of the dbms doesn't support it. So, there's no way after we have a bunch of data in a table to know whether a particular table is following functional dependency or not. 
    
    And if we can't programmatically check functional dependencies, then what's the use of this?
    Well, although dbms doesn't functional dependency, but it help us to reach a better database design termed as *Normalisation*, as in functional dependency we have already learned to identify *keys of a table* and we can *identify a bunch of anamolies(meaning: irregularity)* that we have created

    
    
- Axioms or properties (Basic set of rules exist for rdbms, they follow a lot of things around functional dependencies):

Let's consider a real-life scenario involving a database of employees in a company. We'll use the following attributes:

*EmployeeID*
*EmployeeName*
*Department*
*ManagerID*

   - Reflexivity or Identity:

        - If Y is a subset of X, then X → Y. This axiom reflects the idea that a set of attributes functionally determines itself.

        - If we have the attribute EmployeeID, then EmployeeID → EmployeeID is a reflexive functional dependency. This is evident because the EmployeeID uniquely identifies itself.
 - Augmentation (or Additivity/ Partial Dependency):

     - If X → Y, then for any set of attributes Z, XZ → YZ. This axiom indicates that if a set of attributes functionally determines another set, adding more attributes to both sides does not change the functional dependency.
        
     - If EmployeeID → EmployeeName, then for any set of attributes Department, EmployeeID Department → EmployeeName Department. This reflects the idea that adding more attributes to both sides does not change the functional dependency.

 - Transitivity:

     - If X → Y and Y → Z, then X → Z. This axiom implies that if there is a chain of functional dependencies, you can infer a transitive dependency.

     - If EmployeeID → ManagerID and ManagerID → Department, then EmployeeID → Department. This transitive dependency allows us to infer that the employee's ID determines their department indirectly through the manager.

 - Union (or Decomposition):

    - If X → Y and X → Z, then X → YZ. This axiom states that if a set of attributes functionally determines two other sets independently, it also determines their union.

    - If EmployeeID → EmployeeName and EmployeeID → Department, then EmployeeID → EmployeeName Department. This is the union axiom in action, showing that the employee's ID determines both their name and department.
 - Pseudotransitivity:

    - If X → Y and WY → Z, then WX → Z. This is a generalized form of transitivity, allowing indirect dependencies to be used in certain cases.

   - If EmployeeID → Department and Department ManagerID → EmployeeName, then EmployeeID ManagerID → EmployeeName. This pseudotransitivity allows for indirect dependencies to be used, where the employee's ID and manager's ID together determine the employee's name.

   
These axioms provide a foundation for reasoning about functional dependencies and are used to ensure the consistency and integrity of a relational database schema. They guide the normalization process, helping to design databases with minimal redundancy and logical coherence.

- DB Keys:
Keys are set of attributes that helps us to uniquely identify a record in different situation.
     - Super 
     - Composite
     - Candidate
     - Primary Key
     - Alternate Key
     - Foreign Key

- `Super Key`: A set of attributes within a table that can uniquely identify a record. 
```sql
CREATE TABLE Product (
    ProductID INT,
    ProductCode VARCHAR(20),
    Description VARCHAR(255),
    PRIMARY KEY (ProductID),
    -- Super key: (ProductID, ProductCode)
);
```

- `Candidate Key`: The minimum set of attributes that can uniquely identify a record.

```sql
CREATE TABLE Customers (
    CustomerID INT,
    Email VARCHAR(100) UNIQUE,
    Phone VARCHAR(15) UNIQUE,
    -- other attributes
    PRIMARY KEY (CustomerID)
);
```

- `Composite Keys`: This is a key that consist of 2 or more than 3 attributes, that together uniquely identify a record. 
```sql
CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    Semester VARCHAR(10),
    PRIMARY KEY (StudentID, CourseID)
);
```
*Difference b/w composite and candidate key?*

| Composite keys   | Candidate key  
|------------------| ------------------
| Candidate keys can be either single attributes or composite keys. | Composite keys consist of multiple attributes working together to uniquely identify a record. | 
| A candidate key is a candidate for the primary key, and the database designer selects one of the candidate keys to be the primary key. |   A composite key may or may not be chosen as the primary key for a table.   |  

    

- `Primary Key` : Most important key, there can be more than one candidate key we can choose any one *non-null* candidate key to become primary key.
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    -- other attributes
);
```
- `Alternate Key` : All candidate key apart from primary key are alternate keys
```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    AlternateID INT UNIQUE,
    -- other attributes
);
```
- `Foreign Key` : An attribute which is primary key in some other table
```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    -- other attributes
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

```
- What is *NORMALISATION*?
It is the process of determining how much redundancy exist in a table and  it gives us techniques to reduce it. There are multiple NF(Normal forms) which help us to understand what level of redundancy we have and every NF is a technique to reduce the redundancy at some position.
    - 1NF
    - 2NF
    - 3NF
    - BCNF

 Every NF is dependent on other NF's
    
- `First Normal Form (1NF)`:
    - Most simplest NF, it say's only one simple thing that any attribute must only contain *atomic* values(indivisible values).

    - All entries in a column must be of the same data type.
    - Each column must have a unique name.
    - The order in which data is stored does not matter.
*ex:*
```sql

CREATE TABLE StudentCourses (
    StudentID INT,
    StudentName VARCHAR(50),
    Courses VARCHAR(100)
);
```
### **Original Table:**
| StudentID | StudentName | Courses                        |
|-----------|-------------|--------------------------------|
| 1         | Mohini       | DSA, DBMS, OOPS                 |
| 2         | Punit         | OOPS, DSA, NodeJS    |
| 3         | Milind       | NodeJS, DBMS, DSA               |

*This table is not in 1NF because the "Courses" column contains multiple values separated by commas. To bring it into 1NF, we can create a new table to represent the many-to-many relationship between students and courses:*

```sql
-- Table for Students
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(50)
);

-- Table for Courses
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(50)
);

-- Table for StudentCourses (in 1NF)
CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);

```
*Now, the data is distributed across three tables, and each table satisfies the criteria of 1NF:*

### **Students Table:**
| StudentID | StudentName |
|-----------|-------------|
| 1         | Mohini      |
| 2         | Punit       |
| 3         | Milind      |

### **Courses Table:**
| CourseID | CourseName |
|----------|------------|
| 1        | DSA        |
| 2        | DBMS       |
| 3        | OOPS       |
| 4        | NodeJS     |


### **StudentCourses Table (in 1NF)**
| StudentID | CourseID |
|-----------|----------|
| 1         | 1        |
| 1         | 2        |
| 1         | 3        |
| 2         | 3        |
| 2         | 1        |
| 2         | 4        |
| 3         | 4        |
| 3         | 2        |
| 3         | 1        |

*This representation shows the data distributed across three tables: Students, Courses, and StudentCourses (in 1NF), satisfying the criteria of the first normal form.*

ALthough this isn't the best way, but it's better than first table shown above. Moving to the other NF's now

- `Second Normal Form (2NF)`:
    - The tables shouldn't have partial dependencies, if there's any we need to resolve it.
    - The table should already be 1NF.
    - One of the most important NF's and it reduces the redundancy at a very extreme level
    - 

### **Original Table:**
| StudentID | StudentName | Courses                        |
|-----------|-------------|--------------------------------|
| 1         | Mohini       | DSA, DBMS, OOPS                 |
| 2         | Punit         | OOPS, DSA, NodeJS    |
| 3         | Milind       | NodeJS, DBMS, DSA               |
       
In this table:
- The primary key could be a composite key (StudentID, Courses).
- The non-prime attributes are StudentName and Courses.

### **Breaking it down into 2NF:**
To achieve 2NF, we need to create separate tables for student information and course information. This way, we ensure that non-prime attributes are fully dependent on the primary key.

#### **Students Table:**
| StudentID | StudentName |
|-----------|-------------|
| 1         | Mohini      |
| 2         | Punit       |
| 3         | Milind      |

#### **Courses Table:**
| CourseID | CourseName |
|----------|------------|
| 1        | DSA        |
| 2        | DBMS       |
| 3        | OOPS       |
| 4        | NodeJS     |

#### **StudentCourses Table (in 2NF):**
| StudentID | CourseID |
|-----------|----------|
| 1         | 1        |
| 1         | 2        |
| 1         | 3        |
| 2         | 3        |
| 2         | 1        |
| 2         | 4        |
| 3         | 4        |
| 3         | 2        |
| 3         | 1        |

We can also add marks column in the student course table

| StudentID | CourseID | Marks |
|-----------|----------|-------|
| 1         | 1        | 85    |
| 1         | 2        | 92    |
| 1         | 3        | 78    |
| 2         | 3        | 88    |
| 2         | 1        | 95    |
| 2         | 4        | 90    |
| 3         | 4        | 87    |
| 3         | 2        | 82    |
| 3         | 1        | 91    |

Now, each non-prime attribute (StudentName) is fully functionally dependent on the primary key (StudentID, CourseID). The data is distributed across three tables in a way that satisfies the criteria of 2NF.

- `Third Normal Form (3NF)`:
    - The table should be in 2NF
    - It should not have transitive dependency(*Whenever some indirect relationship happens to cause functional dependency*).
    - 
### **Original Table:**
| EmployeeID | EmployeeName | Department   | ManagerID | ManagerName   |
|------------|--------------|--------------|-----------|---------------|
| 1          | Mohini       | HR           | 2         | Punit         |
| 2          | Punit        | IT           | 3         | Milind        |
| 3          | Milind       | Finance      | 2         | Punit         |

- Primary Key:
The primary key could be EmployeeID because it uniquely identifies each employee.
- 1NF and 2NF:
The table is already in 1NF and 2NF because it has a primary key, and there are no repeating groups or partial dependencies.
- In this example, we observe a transitive dependency:
ManagerName depends on ManagerID, which is not part of the primary key.

### **Bringing it into 3NF:**
To remove the transitive dependency, we create a new table for the managerial relationships:

#### **Employees Table:**
| EmployeeID | EmployeeName | Department   | ManagerID |
|------------|--------------|--------------|-----------|
| 1          | Mohini       | HR           | 2         |
| 2          | Punit        | IT           | 3         |
| 3          | Milind       | Finance      | 2         |

#### **Managers Table:**
| ManagerID | ManagerName   |
|-----------|---------------|
| 2         | Punit         |
| 3         | Milind        |

In this representation, we've separated the data into two tables to eliminate the transitive dependency. The ManagerName is now stored in the Managers table, and the EmployeeDetails table only contains the ManagerID, which is the primary key of the Managers table.
# SQL CREATE TABLE, DROP TABLE

## Learning Goals

- Create a new database
- Create a new table
- Drop a table

## Introduction

The SQL `CREATE TABLE` statement creates a new table
by specifying the table name and the column details, including
column name and data type.    The `DROP TABLE` statement deletes a table
from the database.

## Create A New Database (Code-along)

We will create a new database to store information about pets and their owners.

1. Launch the **pgAdmin** tool.
2. Enter the password for the **postgres** user.
3. You should see a default server **PostgreSQL 15** along with a database named **postgres**:   
  
![pgadmin default server](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/pgadmin.png)
    
4. Right-click on the `Databases` icon and select Create > Database:      
  
![new database](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/newdb.png)
    
5. Name the new databases "pets" and press Save.    
     
![name pet database](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/namepetsdb.png)
    
6. Confirm the new database named `pets` appears in the server view:    
     
![new pet database](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/newpetdb.png)


We will use the **Query Tool** to execute SQL statements.

1. Click on the `pets` database to select the database.
2. Click on the `query tool` icon.
 
![open query tool](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/openquerytool.png)

The query tool opens a panel where we can write SQL statements.
Confirm the connection is for  "pets/postgres@PostgreSQL 15". 

![query tool](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/querytool.png)



## CREATE TABLE

The `CREATE TABLE` statement creates a new table
by specifying the table name and the column details.
Each column is assigned a name and data type, along with other optional attributes.

While PostgreSQL supports dozens of data types, we will primarily work with the following:

- INTEGER stores integer values
- DECIMAL stores fractional numeric values
- TEXT stores textual values
- DATE stores year, month, and day with a recommended format of YYYY-MM-DD. 
- BOOLEAN represents a boolean value.

To explore more data types, please see [PostgreSQL Data Types](https://www.postgresql.org/docs/current/datatype.html).

#### Coding Conventions

1. Use uppercase for SQL keywords such as CREATE, TABLE, INTEGER, PRIMARY KEY, etc.
   SQL is case insensitive, but it is a convention
   to uppercase SQL keywords to separate them from table names and columns.
2. Use lowercase letters for table and column names such as `pet`, `species`, etc.
3. When we have multiple words in a table or column name,
   link them together using underscores rather than spaces or camelcase.
4. There is some debate whether table names should be singular or plural.
   Whether you choose singular or plural names, be consistent across all tables
   within a database. The lessons will use singular nouns for tables names.  

The `CREATE TABLE` statement for the `pet` table is shown below:

```code
CREATE TABLE pet (
	id  INTEGER PRIMARY KEY,
	name TEXT NOT NULL,
	species TEXT NOT NULL,
	breed TEXT,
	age INTEGER
);
```

Let's break down the above code:

1. The `CREATE TABLE` statement specifies the table name `pet`.
2. The `pet` table has 5 columns:
   - `id` will hold a unique integer value to reference each pet.
     - every table should have a primary key to ensure each row is unique.
   - `name` and `species` are required fields that can't be null.
   - `breed` and `age` allow null values as the breed and age of a pet may be unknown.

We will use the query tool to execute the CREATE statement:

1. Enter the `CREATE TABLE` statement into the query panel.
2. Press the execute button.
3. A message should display indicating the query was successful.

![create table](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/createtable.png)

A database **schema** is the structure that represents the logical view
of the database. It defines how the data is organized into tables,
how the tables are related, and other functional and structural
constraints on the data.

We can confirm the `pet` table was added to the `pets` database
by expanding the database tree structure (i.e. schema) as shown below:

![pet structure](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/confirmnewtable.png
)

Expand the `pet` table to display the columns:

![pet table](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/pettablecolumns.png)


## DROP TABLE 

We may want to recreate an existing table.  The `DROP TABLE` statement deletes
a table from a database.  If the table does not exist, the statement will
result in an error.  It is a good idea to use `DROP TABLE IF EXISTS`
to avoid the error.  In general, we will always include a `DROP TABLE`
statement before a `CREATE TABLE` statement in case the database already
has a table with that name.



```sql
DROP TABLE IF EXISTS pet;

CREATE TABLE pet (
	id  INTEGER PRIMARY KEY,
	name TEXT NOT NULL,
	species TEXT NOT NULL,
	breed TEXT,
	age INTEGER
);
```

1. Edit the query panel to drop the `pet` table prior to creating it.
2. Execute the query.

![drop table](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/droptable.png)





## SELECT

The CREATE statement results in a new table `pet` containing 0 rows of data.

The SELECT statement is used to query and retrieve rows from one or more tables.

The basic syntax of a SELECT statement is:

```code
SELECT [comma-separated column names] 
FROM [table name]
WHERE [row selection predicate];
```

We will select all columns from the `pet` table using the `*` character.
Omitting the `WHERE` clause results in the selection of all table rows.

```sql
SELECT *
FROM pet;
```

1. Enter the SELECT statement into the query panel.
2. Press the execute button.
3. The result should display one row containing the table column headings, followed by 0 rows of data.

![emptytableresult](https://curriculum-content.s3.amazonaws.com/6002/sql-create-statement/selectstarpet.png)


## Conclusion

The **pgAdmin** tool can be used to create a new database.
SQL statements can be executed using the **query tool**.  

- The `CREATE TABLE` statement adds a new table in the database.
- The `DROP TABLE` statement deletes a table from the database.
- The `SELECT` statement retrieves rows from a table.

## Resources

- [PostgreSQL CREATE TABLE](https://www.postgresql.org/docs/current/sql-createtable.html)    
- [PostgreSQL DROP TABLE](https://www.postgresql.org/docs/current/sql-droptable.html)   
- [PostgreSQL SELECT](https://www.postgresql.org/docs/current/sql-select.html)   

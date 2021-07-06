# **Basic Commands:**
    - Show Database;        Shows all the Database present in the system
    - use Database_Name;    We select the Database which we have to work on
    - show tables;          Shows the tables present in the Database_Name
    - describe table_Name;  describes the table contents(Specifically the table columns) present in the "table_Name"

# **Create and Insert:**
### Creating a new table in current database:
    - create table Student(
        ID int, 
        Name varchar(100),
        Age int
    );                       
    - describe Student;

### Adding Constraints to the Table:
    1. Faculty_ID: Should be the Primary Key.
    2. Name
    3. Course: Should not contain the NULL values.
    4. Salary: Default should be 10000

    - create table Faculty(
        Faculty_ID int Primary Key,
        Name varchar(100),
        Course varchar(100) Not NULL, 
        Salary int Default 10000
        );

### Inserting Values to the table: 
    - show databases;
    - use school;
    - show tables;
    - insert into Student values(101, "Mohit", 20); (The order should match with the column names)
    - insert into Student values(102, "Amit", 15);  (The order should match with the column names)
    - insert into Student (ID, Name) values(103, "Nikhil"); (we specified the order)
    - insert into Faculty (Faculty_ID, Name) values(102, "Prof"); This will show an error as Course needs to be filled. It cannot have a NULL value.

### Looking at the table:
    - select * from Students; 
    - desc Students

# **Update Table:**
### Adding Columns with/ without constraints:
    - alter table Student add(Address varchar(100));
    - alter table Student add(Email_ID varchar(100), ContactNo varchar(100));
    - alter table Student add(Test int default 100);

### Changing the data type of existing column:
    - alter table student modify ContactNo int;
We can also change the type of a column to "Year": eg: for Date of birth

### Renaming a column:
    - alter table student change Address Location varchar(100);

### Deleting a column:
    - alter table student drop column Test;
    - alter table student drop column Email_ID, drop column ContactNo;
 
# **Retrieve Data:**
### SELECT:
    1. This command allows us to retrieve the specific information as per our requirement from a relational database. It returns a result set of records from one or more tables.
    2. Different Variations of SELECT:
        - SELECT * from Student;
        - SELECT Name from Student;
        - SELECT Name, ID from Student; This will show the columns in exact order which we have provided.

### Loading Data from a source:
    1. Dataset source : http://www.mysqltutorial.org/mysql-sample-database.aspx
    2. Load data from file:
        - source ‘file_name.sql’
        - source C:\Users\Akhil\Desktop/mysqlsampledatabase.sql;
    3. Note: Copy and paste the path from: right click on the file -> properties -> location.
        - show databases;
        - desc payments;


### Restrict result set:
    1. Limit: will set the limit on the number of rows to be displayed. (Similar to head(10) in pandas)
    2. Distinct: Will show only unique values from a particular column.
        - select * from payments limit 10;
        - select distinct customerNumber from payments; 

# **Filter Results:**
### Where Clause:
    1. Using this WHERE clause, we can specify a selection criteria to select the 
    required records from a table.
    2. The WHERE clause works like an if condition in any programming language.
    3. You can specify any condition using different operators - 
        a. Relational operators
            >, <, =, <=, >=
        b. Logical operators
            AND, OR
        c. Is Null and is not Null
    4. We are going to use "orders" table for this clause.
        - show tables;
        - desc orders;
        - show * from orders;
    5. Here we can see that shipped are of the type: Disputed, Shipped, In process, etc. Let's try to fetch data where status is In process
        - select * from orders where status = In Process;
        - select * from orders where orderdate >= '2005-05-01' and orderdate <= '2005-05-15';
        - select * from orders where ordernumber >= 10420 and ordernumber < 10424;
        - select * from orders where ordernumber >= 10420;
        - select * from orders where comments is null limit 10;
        - select * from orders where comments is not null limit 10;

# **Aggregate Functions:**
### Aggregate functions perform a calculation on a set of values and return a single value.
### Different functions:
    - Count:
        - count(*)
        - count(column_name)
        - count(distinct column_name)
    - AVG
    - MAX 
    - MIN
    - SUM
### Orders table:
    - select count(*) from orders;                              Number of rows in a table: will return 326
    - select count(comments) from orders;                       will return 80
    - select count(*) from orders where comments is not null;
    - select count(distinct status) from orders;
### Payments Table:
    - select count(distinct status) from orders;
    - select avg(amount) from payments where amount > 20000;
    - select avg(customer name) from payments;                  This will return 0 as it doesn't exist
    - select max(amount) from payments;
                
# **Update and Delete:**
### Update row of a table
    - UPDATE table_name set column_name = 'column_value';
    - UPDATE table-name set column_name = 'column_value' where condition;
    - show databases;
    - use faculty;
    - select * from faculty;
    - update faculty set salary = 50000;
    - update faculty set salary = 10000 where faculty_ID = 101;

### Delete 
    - DELETE from table_name where condition;
    - delete from faculty;              will delete all the rows from the table
    - delete from faculty where salary = 10000;
### Truncate
    - TRUNCATE table_name
    - Truncate faculty;                 will delete all the rows from the table
### Drop
    - DROP table table_name
    - Drop table Faculty;               Will delete the table from the given list of tables
    - show tables                       Now it will not show the table faculty
    - Drop Databases School;            Will delete the whole database
    - show databases;                   List will not contain the database school

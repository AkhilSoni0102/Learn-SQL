# Basic Commands:
    - Show Database;        Shows all the Database present in the system
    - use Database_Name;    We select the Database which we have to work on
    - show tables;          Shows the tables present in the Database_Name
    - describe table_Name;  describes the table contents(Specifically the table columns) present in the "table_Name"

# Create and Insert:
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

# Update Table:
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
 
# Retrieve Data:
### SELECT:
1. This command allows us to retrieve the specific information as per our requirement from a relational database. It returns a result set of records from one or more tables.
2. Different Variations of SELECT:
    - SELECT * from Student;
    - SELECT Name from Student;
    - SELECT Name, ID from Student; This will show the columns in exact order which we have provided.




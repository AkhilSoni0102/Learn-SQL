# Advanced SQL:
# **Group by:**
### Group By Based on 1 column:
    1. Used to group rows that have the same values.
    2. It summarizes data from the database.
    3. The GROUP BY clause returns one row for each group.

    - show databases;
    - use classicmodels;
    - show tables;
    - desc customers;
    - select customerNumber, contactFirstName, city, state, country, creditlimit from customers;
    - select customerName, country from customers;
### This will group on the basis of countries and the first name for each country will be returned:
    - select CustomerName, country from customers group by country;             
### Count of total number of rows:
    - select count(**) from customers;  
    - select count(**) from customers where country = 'USA';
### Grouping customers based on country and state:
    - select count(**) from customers group by country;
    - select country, count(**) from customers group by country;
    - select state, count(**) from customers group by state;
    - select state, country, count(**) from customers group by country;

### Count of the number of countries where state is not null:
    - select count(**) from customers where state is not null;
    - select count(**) from customers where state is not null group by country;
    - select country,count(**) from customers where state is not null group by country;

### Sum of credit limit for each possible country:
    - select country, sum(creditlimit) from customers group by country;
    - select country, sum(creditlimit) from customers where creditlimit > 50000 group by country;

### Grouping our result based on two columns:
    - select country, state, count(**) from customers group by country, state;
    - select distinct state from customers where country = 'USA';

# **Having and order by:**
    1. WHERE keyword cannot be used with group functions.
    2. We have to use HAVING clause in SELECT statement to specify filter conditions for grouped results.
    3. If the GROUP BY clause is omitted, the HAVING clause behaves like the where clause. 

    - select state, count(**) from customers where state is not null group by state;
    The above query returns the states which are not null and it grouped based on states.
    So, why do we say that WHERE can not be used with grouped functions
    Note: We can not use where wil grouped results. or we can say that we can not add any type of filter conditions with our grouped results using WHERE clause. Here we have applied group by after applying the Where clause. 
    for Such situations we use HAVING clause

### Having:
    - select state, count(**) from customers where count(**) > 5 group by state;  ---> Error 
    - select state, count(**) from customers group by state having count(**) > 5;

    - select country, sum(creditlimit) from customers group by country;
    - select country, sum(creditlimit) from customers group by country having sum(creditlimit) > 50000;

### Order By:
    1. Used to sort the result-set in ascending or descending order.
    2. Sorts the records in ascending order by default.
    3. To sort the records in descending order, use DESC keyword.

### Ascending Order:
    - select country, sum(creditlimit) from customers group by country having sum(creditlimit) > 50000 order by sum(creditLimit);
### Descending Order:
    - select country, sum(creditlimit) from customers group by country having sum(creditlimit) > 50000 order by sum(creditLimit) desc;

# **IN:**
### Products Table:
    - select productName, productline, quantityinstock, buyprice, msrp from products limit 20;
### IN:
    1. The IN operator is shorthand for multiple OR conditions.
    2. The IN operator allows you to detemine if a specified value matches any value from a list or from a subquery.
    3. Syntax:
        - SELECT column1, column2, ... FROM table_name WHERE (expe|column1) IN ('value1', 'value2',... )
    4. The values in the list must be seperated by a comma.

    - select productName, productline, quantityinstock, buyprice, msrp from products where productline in ('Motorcycles', 'Classic Cars', 'Vintage Cars'); 
    - select productName, productline, quantityinstock, buyprice, msrp from products where productline in ('Motorcycles', 'Classic Cars', 'Vintage Cars') and quantityinstock > 8000;
    - select productName, productline, quantityinstock, buyprice, msrp from products where productline in ('Motorcycles', 'Classic Cars', 'Vintage Cars') and quantityinstock > 8000 order by quantityinstock;

### NOT IN:
    - select productName, productline, quantityinstock, buyprice, msrp from products where productline NOT IN ('Motorcycles', 'Classic Cars', 'Vintage Cars') and quantityinstock > 8000;

# **BETWEEN: (End value1 and value2 are inclusive)**
    1. We can use BETWEEN clause to replace a combination of "greater than equal and less than equal" conditions.
    2. Syntax: 
        - SELECT column_name(s) FROM table_name WHERE column_name BETWEEN value1 AND value2;
    3. It will return the records where expression is within the range of value1 and value2.
    4. Values can be numbers, text, or dates.

    - select productName, productline, quantityinstock, buyprice, msrp from products where quantityinstock > 4000 and quantityinstock < 5000;
    - select productName, productline, quantityinstock, buyprice, msrp from products where productline BETWEEN 4000 and 5000;
### IMPORTANT:
    - select productName, productline, quantityinstock, buyprice, msrp from products where productName BETWEEN "A" and "D";

### NOT BETWEEN:
    - select productName, productline, quantityinstock, buyprice, msrp from products where quantityinstock not  BETWEEN 4000 and 5000;

# **LIKE:**
    1. The LIKE operator is used in WHERE clause to search for a specified pattern in a column.
    2. There are two wildcards used in conjunction with the LIKE operator.
        - %: The percentage sign represents zero, one, or multiple characters.
        - _: The underscore represents a single character.
    3. Syntax:
        SELECT column1, column2, ... from table_name WHERE column LIKE pattern;
### List of customersName starting with letter 'C':
    - select customerNumber, customerName from customers where customerName LIKE "C%";
### List of CustomerName starting with letter 'C' and ending with 'co.' and % represents that there can be any number of letters in between:
    - select customerNumber, customerName from customers where customerName LIKE "C%co."; 

      Statements                      Description
    - LIKE 'S%'   :       It finds any value which starts with 'S'.
    - LIKE '%S%'  :       It finds any value which have 'S' in any position.
    - LIKE '_SS%' :       It finds any value which have 'SS' in the second and third positions.
    - LIKE 'S_%_%':       It finds any value which starts with 'S' and have at least three  characters in length.
    - LIKE '%S'   :       It finds any value which ends with 'S'.
    - LIKE '_S%P' :       It finds any value which have 'S' in the second position and ends with 'P'.
    - LIKE 'S___P':       It finds any value in a five digit numbers which start with 'S' and ends with 'P'.

### List of CustomerName starting with letter 'C' and ending with 'co.' and there is at least 1 'm' between 'C' and 'co.':
    - select customerNumber, customerName from customers where customerName LIKE "C%m%co.";

    - select customerNumber, customerName from customers where customerName LIKE "_a%";

### NOT LIKE:
    - select customerNumber, customerName from customers where customerName NOT LIKE "_a%";

### ESCAPE:
### Now, what if we have '%' itself in the middle of a name and we want to list those out? Eg: "AB%C", "A_BC":
    1.  Let's say you wanted to search for a '%' or a '_' character in the MySQL LIKE condition. You can do this using an Escape character.
        - SELECT * FROM table_name WHERE column_name LIKE 'G\%';
    2. We can override the default escape character in MySQL by providing the ESCAPE modifier as follows:
        - SELECT * FROM table_name WHERE column_name LIKE 'G!%' ESCAPE '!';
    
    - select customerNumber, customerName from customers where customerName LIKE "%\%%";

# **Join Introduction:**
    1. With join, we can query data from two(or multiple) tables based on a related column which is present in both the tables.
    2. While performing the join, we need to specify the shared column and the condition on which we want to join the tables.
    3. You can use JOINS in the SELECT, UPDATE, DELETE, statements to join multiple tables.
### Types of Joins: 
    1. Inner join or Simple join
    2. Left outer join or Left join
    3. Right outer join or Right join
    4. Full outer join or Full join

# **Inner join:** == Intersection of A and B 
    We can write INNER JOIN and JOIN interreplacibly
    1. This will only return rows where there is at least one row in both tables that matches the specified join condition.
    2. Syntax: 
        - SELECT table.col1, table.col2, ...
          FROM table_name1
          INNER JOIN table_name2
          ON
          table1.column_name = table2.column_name;
    
    t1:
        +------+------+
        | ID   | Name |
        +------+------+
        |    1 | A    |
        |    2 | B    |
        |    3 | C    |
        +------+------+
    t2:
        +------+------+
        | ID   | Name |
        +------+------+
        | A    | abc  |
        | D    | xyz  |
        | A    | def  |
        | C    | pqr  |
        +------+------+
    
    - select * from t1 inner join t2 on t1.name = t2.id;
        +------+------+------+------+
        | ID   | Name | ID   | Name |
        +------+------+------+------+
        |    1 | A    | A    | abc  |
        |    1 | A    | A    | def  |
        |    3 | C    | C    | pqr  |
        +------+------+------+------+
    
    - select * from t1 inner join t2 on t1.name = t2.id where t1.id >= 2;
### Printing specific columns from both the tables:
    - select class_ID, Name from classDetails inner join Teachers_Details on classteacher_ID = Teacher_ID; 
    - select classDetails.class_ID, Teachers_Details.Name from classDetails inner join Teachers_Details on classteacher_ID = Teacher_ID;

# **Inner join with 3 tables:**
    Syntax:
    - (SELECT table1.col1, table2.col2, ...
      FROM table1 
      INNER JOIN table2
      ON
      table1.column_name = table2.column_name)
      INNER JOIN table3
      ON table2.column_name = table3.column_name;
    
### We have 3 tables"
    1. ClassDetails:
        - Class_ID
        - ClassTeacher_ID
    2. TeachersDetails:
        - Teacher_ID
        - Name
        - Subject_ID
    3. SubjectDetails:
        - ID
        - Name 
        - Total Students
    
    - select Class_ID, TeacherDetails.Name, SubjectDetails.Name from ClassDetails INNER JOIN TeacherDetails on ClassTeacher_ID = Teacher_ID INNER JOIN SubjectDetails ON SubjectID = ID;

# **Left and Right Join:**
### Left Join:  A + (A Intersection B)
    1. It returns all the rows from the left table specified and only those rows from the other table where the join condition is matched.
    2. Syntax:
        - SELECT table1.col1, table2.col2, ...
          FROM table1
          LEFT JOIN table2
          ON table1.column_name = table2.column_name
    
    t1:
        +------+------+
        | ID   | Name |
        +------+------+
        |    1 | A    |
        |    2 | B    |
        |    3 | C    |
        +------+------+
    t2:
        +------+------+
        | ID   | Name |
        +------+------+
        | A    | abc  |
        | D    | xyz  |
        | A    | def  |
        | C    | pqr  |
        +------+------+
    - select * from t1 left join t2 on t1.name = t2.id;
        +------+------+------+------+
        | ID   | Name | ID   | Name |
        +------+------+------+------+
        |    1 | A    | A    | def  |
        |    1 | A    | A    | abc  |
        |    2 | B    | NULL | NULL |
        |    3 | C    | C    | pqr  |
        +------+------+------+------+

### Right Join: B + (A Intersection B)
    1. It returns all rows from the right table specified and only those rows from the left table where the join condition is satisfied.
    2. Syntax
        - SELECT table1.col1, table2.col2, ...
          FROM table1
          RIGHT JOIN table2
          ON 
          table1.column_name = table2.column_name;
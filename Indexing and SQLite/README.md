# Indexing and SQLite
## Indexing:
    1. Indexing is a way to optimise our search queries on large databases. With the help of indexing, we can avoid scanning the whole table to obtain the results we are looking for.
    2. In more formal terms, indexes in database is a kind of data structure that improves the speed of operations in a table.
## Default Indexing:
    1. There are two types of default indexing:
        - Clustered - When primary key is marked
        - Non-clustered - When Unique key is marked
    2. By Identifying which column we are going to use more often we can optimise the searching by sorting that column. This way, we can reduce the time from linear to Logarithmic.

    To look which columns are chosen by default for indexing, we run the following command:
        - select indexes from table_name;
### For Columns marked as primary key:
    1. In general, in MySQL, if any column is marked as Primary key, default indexing will be done based on that column. Column marked as PK will automatically get sorted.
    2. For a table which don't have any column marked as Primary key, there will be no indexing.
    3. Unique = Primary key + NULL values;
### For Columns marked as Unique:
    Instead of sorting the column marked as unique, a new table is generated for that column, where the references are stored, similar to hash table.

# Use Indexing:
### Three Types of Keys:
    - Primary Key  :    PRI Should be unique and cannot have null values 
    - Unique Key   :    UNI Should be unique and can have null values
    - Multiple Key :    MUL No constraint ( Used when we want to apply indexing to a column which can have duplicate and null values)

    - select * from customers where customerNumber = 480;
### Explain: 
    - explain select * from cutomers where customerNumber = 480;
    This will show the details of running of a particular query and the number of rows searched to find the desired value.
    If the column is indexed and we are searching for a value in that column, the number of rows traversed is 1. but for those which aren't indexed we need to traverse the whole table in order to find that value. 
### Creating our own index, when the table is already created:
    - create index index_name on table_name(column_name);
    - show index from customers;
### Creating our own index, while creating the table:
    - create table Test(id int primary key, name varchar(100), address varchar(100), index index_name(name));
    - desc Test;
    +---------+--------------+------+-----+---------+-------+
    | Field   | Type         | Null | Key | Default | Extra |
    +---------+--------------+------+-----+---------+-------+
    | id      | int          | NO   | PRI | NULL    |       |
    | name    | varchar(100) | YES  | MUL | NULL    |       |
    | address | varchar(100) | YES  |     | NULL    |       |
    +---------+--------------+------+-----+---------+-------+

### Removing the index from a column:
    - drop index index_name on table_name;

# indexing Good or Bad:
### Good:
    Indexing is Good when we need to apply search queries very often.

### Bad:
    It is bad when insertion and deletion of rows are very often, because in that case the table needs to get rearranged everytime a row is inserted or deleted.

### How is data stored internally in indexing:
    BinaryTree is used to store the indexes of the values. 
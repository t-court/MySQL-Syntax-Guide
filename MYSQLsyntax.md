# MySQL Cheat Sheet/Syntax Guide #

## 1. Logging into MySQL from the terminal ##
- SSH into your web server
- mysql -u root -p will log you into MySQL
- After entering your password you will be logged in

## 2. Users ##
### A semicolon ; is required at the end of every MySQL statement to signify to MySQL that it is the end ###
- To show all users run this command:
 `SELECT user FROM mysql.user;`
- To create a new user inside MySQL:
 `CREATE USER 'username' IDENTIFIED BY 'password';`
- To create a new user when connecting remotely:
 `CREATE USER 'username'@'ip_address' IDENTIFIED BY 'password';`
- To create a new user on the machine with MySQL:
 `CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';`
- Where username, ip_address and password are your entered values.
### The commands to grant user privileges are as follows: ###
- To grant all privileges -> `GRANT ALL PRIVILEGES ON database_name. TO 'username'@'localhost';`
- To grant limited permission -> `GRANT ALL PRIVILEGES ON 'database_name.table_name' TO 'username'@'localhost';`
- To show granted privileges -> `SHOW GRANTS FOR 'username'@'localhost';`
- To revoke user privileges -> `REVOKE privilege_type ON database.table FROM 'user_name'@'localhost';`

## 3. SHOW, DROP, & CREATE DATABASES ##
- To create a database:
`CREATE DATABASE 'database_name';`
- To see all databases:
`show databases;`
- To delete a database:
`DROP DATABASE 'database_name';`
- To Select a Database to work in:
 firstly `SHOW DATABASES; `
 secondly `USE 'DATABASENAME';`
- All data in MySQL is stored in tables, each MySQL database consists of tables, and each table consists of rows and columns. The columns are named and specify the type of data where as the rows are where the actual data itself is stored.
- To CREATE a TABLE with Columns and their proper data types:
`CREATE TABLE 'table name' (
    column_name1 data_type CONSTRAINT, 
    column_name2 data_type CONSTRAINT, 
    column_name3 data_type CONSTRAINT 
);`

## 4. Data Types ##
### String Data Types ###

| Data type         | Description   |
|-------------------|---------------|
| CHAR(size)	    | A FIXED length string (can contain letters, numbers, and special  characters). The size parameter specifies the column length in characters - can be from 0 to 255. Default is 1  |
| VARCHAR(size)	    | A VARIABLE length string (can contain letters, numbers, and special characters). The size parameter specifies the maximum column length in characters - can be from 0 to 65535    |
| BINARY(size)	    | Equal to CHAR(), but stores binary byte strings. The size parameter specifies the column length in bytes. Default is 1    |
| VARBINARY(size)	| Equal to VARCHAR(), but stores binary byte strings. The size parameter specifies the maximum column length in bytes.  |
| TINYTEXT	        | Holds a string with a maximum length of 255 characters    |
| TEXT(size)	    | Holds a string with a maximum length of 65,535 bytes  |
| * these are not all of them but they are the most common.   |

### Numeric Data Types ###

| Data type         | Description   |
|-------------------|---------------|
| BIT(size)         |  A bit-value type. The number of bits per value is specified in size. The size parameter can hold a value from 1 to 64. The default value for size is 1.  |
| TINYINT(size)	    | A very small integer. Signed range is from -128 to 127. Unsigned range is from 0 to 255. The size parameter specifies the maximum display width (which is 255)    |
| BOOL	            | Zero is considered as false, nonzero values are considered as true.   |
| BOOLEAN	        |    Equal to BOOL  |
| SMALLINT(size)	| A small integer. Signed range is from -32768 to 32767. Unsigned range is from 0 to 65535. The size parameter specifies the maximum display width (which is 255)   |
| MEDIUMINT(size)	| A medium integer. Signed range is from -8388608 to 8388607. Unsigned range is from 0 to 16777215. The size parameter specifies the maximum display width (which is 255)   |
| INT(size)	        | A medium integer. Signed range is from -2147483648 to 2147483647. Unsigned range is from 0 to 4294967295. The size parameter specifies the maximum display width (which is 255)   |
| INTEGER(size)	    | Equal to INT(size)    |
| BIGINT(size)	    | A large integer. Signed range is from -9223372036854775808 to 9223372036854775807. Unsigned range is from 0 to 18446744073709551615. The size parameter specifies the maximum display width (which is 255)    |
|FLOAT(size, d)	    | A floating point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter. This syntax is deprecated in MySQL 8.0.17, and it will be removed in future MySQL versions    |
| FLOAT(p)	        | A floating point number. MySQL uses the p value to determine whether to use FLOAT or DOUBLE for the resulting data type. If p is from 0 to 24, the data type becomes FLOAT(). If p is from 25 to 53, the data type becomes DOUBLE()   |
| DOUBLE(size, d)	| A normal-size floating point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter    |
| DECIMAL(size, d)	| An exact fixed-point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter. The maximum number for size is 65. The maximum number for d is 30. The default value for size is 10. The default value for d is 0.    |

### Date and Time Data Types ###
|  Data type  |  Description  |
|-------------|---------------|
| DATE	       |  A date. Format: YYYY-MM-DD. The supported range is from '1000-01-01' to '9999-12-31'  |
| DATETIME(fsp)	 |    A date and time combination. Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1000-01-01 00:00:00' to '9999-12-31 23:59:59'. Adding DEFAULT and ON UPDATE in the column definition to get automatic initialization and updating to the current date and time  |
| TIMESTAMP(fsp)    |   A timestamp. TIMESTAMP values are stored as the number of seconds since the Unix epoch ('1970-01-01 00:00:00' UTC). Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1970-01-01 00:00:01' UTC to '2038-01-09 03:14:07' UTC. Automatic initialization and updating to the current date and time can be specified using DEFAULT CURRENT_TIMESTAMP and ON UPDATE CURRENT_TIMESTAMP in the column definition  |
| TIME(fsp)	 |  A time. Format: hh:mm:ss. The supported range is from '-838:59:59' to '838:59:59'|
| YEAR	  |  A year in four-digit format. Values allowed in four-digit format: 1901 to 2155, and 0000.  |

## 5. Constraints ##
### There are two types of constraints in mysql: ###
    1. Column Level Constraints: Applied to individual columns, limits the data entered into the column.
    2. Table Level Constraints: Applied to the whole table, limits the data entered into the table.

### Common Constraints: ###

| Contraint     | Description |
|---------------|-------------|
| NOT NULL      |   Column cannot have a null value.  |
| AUTO_INCREMENT |  Automatically increments from 1 with every new table insert. |
| UNIQUE        |  Every value inserted into constrained column must be unique. |
| DEFAULT       | Sets the default value for a column when a value is not inserted into the new row.  |
| PRIMARY KEY   | Used to identify each record in a table, cannot be null or empty. There can only be one primary key per table. Often used with auto_increment. |
| FOREIGN KEY   | Aka the reference key, Foreign keys link tables together. The foreign key of table one matches the primary key of a different table two. Table one is referenceing table two. This allows for much more complex and intricate data storage. | 

# 6. SHOW, DROP, & SELECT Tables #
- To show tables:
`SHOW TABLES;`
- To delete a table:
`DROP TABLE 'table_name';`
- To Insert ROWS & RECORDS: 
`INSERT INTO table_name (column1,column2) Values (value1column1,value1column2), (value2column1,value2column2);`
`INSERT INTO table_name (column) VALUES (value);`

- The columns must be in the same order they are displayed in the table. The same goes for the values.

- To SELECT with the WHERE Clause:
`SELECT column_name FROM table_name WHERE column_name = 'value';`
- The WHERE clause compares the given value with the recorded value of the named column within the named table. If they are equal then it returns the value of the selected column from that same row.
`SELECT * FROM table_name WHERE coumn_name = 'value';`
- An asterisk is used to select and return all the columns of the named table where the named column value is equal to the given 'value'.
- To SELECT with the WHERE Clause using a range AND, IN and BETWEEN keywords can be use in conjunction with the WHERE keyword, for example:
`SELECT * FROM table_name WHERE column_name BETWEEN 10 AND 60;`
- That will return all the values in the table where the values of the named column are between 10 and 60.
- Using these keywords you can build conditions to search a range of strings:
`SELECT * FROM table_name WHERE column_name BETWEEN 'D' AND 'G';`
- That will return all the values in the table where the named column starts with a letter between d and g.

- To delete all rows from a table:
`DELETE FROM table_name;` 
- To DELETE an individual ROW:
`DELETE FROM table_name WHERE [Condition];`
The [condition] would specify the value in the row you are trying to delete.

- To UPDATE a ROW:
- The WHERE clause determines how many records will be updated.
UPDATE table_name SET column_name = 'Its new value' WHERE "column_name" = 'existing value';

- To add a new column:
ALTER TABLE 'table_name' ADD COLUMN column_name data_type constraint;
- To Order by and use Distinct Order By
- Returns data in either ascending or descending order. 
SELECT column_name FROM table_name ORDER BY column_name asc;
- Often tables and columns contain many duplicate values. 
- To select only distinct (different) values:
SELECT DISTINCT column_name FROM table_name;
- To Concatenate Columns use MySQL's Concat() function:
SELECT column_name CONCAT(column_name1, " ", column_name2, " ", column_name3) AS existing_column FROM table_name;
- To Select Distinct Rows:
SELECT DISTINCT (column_name) FROM table_name;
- Use LIKE operator in a WHERE clause to search for a specified pattern in a column. 

- Patterns:
* The percent sign (%) represents zero, one, or multiple characters.

* The underscore sign (_) represents one single character

* WHERE column_name LIKE 'x%' Finds any values that start with "x"

* WHERE column_name LIKE '%a' Finds any values that end with "a"

* WHERE column_name LIKE '%or%' Finds any values that have "or" in any position

* WHERE column_name LIKE '_e% Finds any values that have "e" in the second position

* WHERE column_name LIKE 'z_% Finds any values that start with "z" and are at least 2 characters in length

* WHERE column_name LIKE 'y__%' Finds any values that start with "y" and are at least 3 characters in length

* HERE ContactName LIKE 't%o' Finds any values that start with "t" and ends with "o"

- Using LIKE operator:
SELECT column_name, column_name FROM table_name WHERE column_name LIKE pattern:
- To select all cars brands that start with an f in a table called cars:
SELECT carBrand FROM cars WHERE carBrand LIKE "%f";

- To Create & Remove Index:
CREATE INDEX index_name ON table_name (column_name);
DROP INDEX index_name ON table_name;

- To use inner join;
SELECT column_name FROM table1 INNER JOIN table2 ON join_condition;
- INNER JOIN compares each row in table1 with every row in table2 based on the join condition. If rows from both tables cause the join condition to evaluate to TRUE, the INNER JOIN creates a new row whose columns contain all columns of rows from the tables and includes this new row in the result set. Otherwise, the INNER JOIN just ignores the rows.
- If the condition does not evaluates to TRUE, the INNER JOIN returns an empty result set. This can be applied to join more than 2 tables.

- To JOIN Multiple Tables:
SELECT table_one.column_one, table_three.column_one FROM table_one JOIN table_two ON table_one.primarykey = table_two.foreignkey JOIN table_three ON table_two.primarykey = table_three.foreignkey;

- Firstly we Join table 1 and table two which produces a temporary table with a combination of data from table 1 and table 2, which is then joined to table 3. This formula can be extended to more than 3 tables.
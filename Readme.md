# **Common Commands**

### Legend

1. <> : Necessary
1. [] : Optional

### Creating User
``` SQL
	CREATE USER 'username'@'host' IDENTIFIED BY 'password';
```
### Removing User
``` SQL
	DROP USER <user>;
```
### Granting Permission/Privileges
```
	GRANT <privileges> ON <database> TO <user>;
```
Grant Global Access
```
	GRANT ALL ON *.* TO 'robert'@'%' WITH GRANT OPTION;
```
Grant Read Write Access
```
	GRANT SELECT,INSERT,UPDATE,DELETE ON serv.* TO 'jeffrey'@'localhost';
```
Grant Read Access and power to give the same to other users
```
	GRANT SELECT ON edu.staff TO 'david'@'localhost' WITH GRANT OPTION;
```
Custom Grant
```
	GRANT ALL ON logan.* TO 'quentin'@'localhost' WITH MAX_QUERIES_PER_HOUR
	100;
```
	Grant can take in IDENTIFIED as an additional parameter. Needs to be appeneded at the end.
	To give additional privileges run Grant with updated paramters and the privileges will be added.

### Adding/removing privileges

##### Basic Syntax
```
	REVOKE <privileges> ON <database> FROM <user>;
```
##### Removing GRANT Option Priveleges
```    
    REVOKE DELETE,GRANT OPTION ON cust.* FROM 'todd'@'%';
```    
#####	 Removing all priveleges    
``` SQL
    REVOKE ALL,GRANT OPTION FROM 'neil'@'%.example.com';
```
### Creating Table
``` SQL
    CREATE TABLE table_name (<column_definitions>);
```
### Altering Table
``` SQL
    ALTER TABLE table_name <alter_definition>[, alter_definition] ...;
```

### Altering Column
```
    ADD <column_name> <column_definition> [FIRST | AFTER <column_name>];
```
You can only use either FIRST or AFTER and not both

### Modifying Column
```
    MODIFY <column_name> <column_definition>;
```
# **CRUD OPERATIONS**

### INSERTING

``` SQL
    INSERT [INTO] <table_name> [(<column_name>[, column_name,...])] 
    {VALUES | VALUE}
    ({expression|DEFAULT},...)[,(...),...];
    
    INSERT INTO employees (pref_name,givenname,surname,birthday)
    VALUES ("George","George Albert","Smith","1970-04-04");
```

### UPDATING

``` SQL
    UPDATE <table_name>
    SET column_name1={expression|DEFAULT}
    [, column_name2={expression|DEFAULT}] ...
    [WHERE <where_conditions>];
    
    UPDATE employees SET
    pref_name = "John", birthday = "1958-11-01"
    WHERE surname = "Taylor" AND givenname = "John";
```

### DELETING

``` SQL
    DELETE FROM <table_name> [WHERE <where_conditions>];
    DELETE FROM employees WHERE givenname="Spencer" AND surname="Kimball";
```

### READING
``` SQL
    SELECT <what> FROM <table_name>
    [WHERE <where-conditions>]
    [ORDER BY <column_name>];
```
# **BACKING UP DATABASE**

```
    mysqldump [-u username] [-p] database_name [table_name]
```

mysqldump outputs on standard output. Use pipiing to direct that output to another .sql file. 

```
    mysqldump -u root -p test > test.sql
```

### Restoring data
```
    mysql -u root -p test < test.sql
```

# **Tab Delimited Files**
We can use mysqldump to create tab delimited tab files. It willl create two files. One with the actual data and the other with the commands to create that data.

```
    mysqldump --tab /tmp/ -u root -p test employees
```

After generating the data in the employees.txt file mysqlimport can be used to import all our database directly into the tables.






    
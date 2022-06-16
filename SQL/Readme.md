# SQL

# Defination

> **Structure Query Language(SQL)** is a database query language **used for storing and managing data** in **Relational DBMS**. 

- SQL was the first commercial language introduced for E.F Codd's Relational model of database. 
- Today almost all RDBMS(MySql, Oracle, Infomix, Sybase, MS Access) use SQL as the standard database query language.
- SQL is used to perform all types of data operations in RDBMS.

## DDL: Data Definition Language

- This includes changes to the structure of the table like creation of table, altering table, deleting a table etc.
- All DDL commands are auto-committed. That means it saves all the changes permanently in the database.

![Screenshot Capture - 2022-06-16 - 09-17-58](https://user-images.githubusercontent.com/35686407/173987012-7a34ca37-e8f3-44fb-9742-28b78525df4d.png)

## DML: Data Manipulation Language
- DML commands are used for manipulating the data stored in the table and not the table itself.
- DML commands are not auto-committed. It means changes are not permanent to database, they can be rolled back.

![Screenshot Capture - 2022-06-16 - 09-19-10](https://user-images.githubusercontent.com/35686407/173987136-735d7933-77f1-4987-b01b-07372ef3e2c4.png)

## TCL: Transaction Control Language
- These commands are to keep a check on other commands and their affect on the database.
- These commands can annul changes made by other commands by rolling the data back to its original state.
- It can also make any temporary change permanent.

![Screenshot Capture - 2022-06-16 - 09-20-05](https://user-images.githubusercontent.com/35686407/173987289-2ac6475b-0edf-4d25-ad87-23aac3205157.png)

## DCL: Data Control Language
- Data control language are the commands to grant and take back authority from any database user.

![Screenshot Capture - 2022-06-16 - 09-20-50](https://user-images.githubusercontent.com/35686407/173987375-b562ef8e-b0ae-413e-a3a5-54d9a9060f6c.png)

## DQL: Data Query Language
- Data query language is used to fetch data from tables based on conditions that we can easily apply.

![Screenshot Capture - 2022-06-16 - 09-21-43](https://user-images.githubusercontent.com/35686407/173987438-0e589dac-d91e-4423-9693-c4906e06c31d.png)

# DataTypes

## String DataTypes

![Yahoo Baba - MySQL Create Table Tutorial in Hindi Urdu  tN3B0F24fJs - 885x498 - 6m30s](https://user-images.githubusercontent.com/35686407/173989143-fd04a110-cdbd-40f4-91e8-8282ea7cb732.png)

## Numeric DataTypes

![Yahoo Baba - MySQL Create Table Tutorial in Hindi Urdu  tN3B0F24fJs - 885x498 - 8m49s](https://user-images.githubusercontent.com/35686407/173989211-b8ef6f97-66ed-4102-9b00-d11541933a87.png)

## Date and Time

![Yahoo Baba - MySQL Create Table Tutorial in Hindi Urdu  tN3B0F24fJs - 853x480 - 10m15s](https://user-images.githubusercontent.com/35686407/173989268-de14afcd-ccb4-4d09-b825-715558c3c9a9.png)


# DATABASE COMMANDS

## 1. Create Database

```sql
CREATE DATABASE Database_Name;  
```

- SQL not allow  to create the database with the existing database name
- if you want to create another Student database in the same database system,  firstly you have to delete the existing database by using the Drop Statement
- You can also replace the existing database with the help of Replace keyword.

```sql
CREATE OR REPLACE DATABASE Student;  
```

## 2. Show Databases

```sql
SHOW DATABASE; 
```

## 3. Drop Database

1. Single

```sql
DROP DATABASE Student;  
```

2. Multiple

```sql
DROP DATABASE Database_Name1, [ Database_Name2, ......., Database_NameN ];
```

- IF EXISTS is optional

```oracle
DROP DATABASE [IF EXISTS] database_name;    
```


## 4. Rename Database

> In MySql

```sql
RENAME DATABASE old_database_name TO new_database_name;   
```

## 5. Select Database

```sql
USE database_name;
```



























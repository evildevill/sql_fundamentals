# SQL INJECTION FUNDAMENTALS 🖤✨

## Introduction

Most modern web applications utilize a database structure on the back-end. Such databases are used to store and retrieve data related to the web application, from actual web content to user information and content, and so on. To make the web applications dynamic, the web application has to interact with the database in real-time. As HTTP(S) requests arrive from the user, the web application's back-end will issue queries to the database to build the response. These queries can include information from the HTTP(S) request or other relevant information.

<img src="https://github.com/evildevill/sql_fundamentals/blob/main/img/db_request_3.png"/>

When user-supplied information is used to construct the query to the database, malicious users can trick the query into being used for something other than what the original programmer intended, providing the user access to query the database using an attack known as SQL injection (SQLi).

SQL injection refers to attacks against relational databases such as MySQL (whereas injections against non-relational databases, such as MongoDB, are NoSQL injection). This module will focus on MySQL to introduce SQL Injection concepts.

## SQL Injection (SQLi)

Many types of injection vulnerabilities are possible within web applications, such as HTTP injection, code injection, and command injection. The most common example, however, is SQL injection. A SQL injection occurs when a malicious user attempts to pass input that changes the final SQL query sent by the web application to the database, enabling the user to perform other unintended SQL queries directly against the database.

There are many ways to accomplish this. To get a SQL injection to work, the attacker must first inject SQL code and then subvert the web application logic by changing the original query or executing a completely new one. First, the attacker has to inject code outside the expected user input limits, so it does not get executed as simple user input. In the most basic case, this is done by injecting a single quote (') or a double quote (") to escape the limits of user input and inject data directly into the SQL query.

Once an attacker can inject, they have to look for a way to execute a different SQL query. This can be done using SQL code to make up a working query that executes both the intended and the new SQL queries. There are many ways to achieve this, like using stacked queries or using Union queries. Finally, to retrieve our new query's output, we have to interpret it or capture it on the web application's front end.

## Use Cases and Impact

A SQL injection can have a tremendous impact, especially if privileges on the back-end server and database are very lax.

First, we may retrieve secret/sensitive information that should not be visible to us, like user logins and passwords or credit card information, which can then be used for other malicious purposes. SQL injections cause many password and data breaches against websites, which are then re-used to steal user accounts, access other services, or perform other nefarious actions.

Another use case of SQL injection is to subvert the intended web application logic. The most common example of this is bypassing login without passing a valid pair of username and password credentials. Another example is accessing features that are locked to specific users, like admin panels. Attackers may also be able to read and write files directly on the back-end server, which may, in turn, lead to placing back doors on the back-end server, and gaining direct control over it, and eventually taking control over the entire website.

## Prevention

SQL injections are usually caused by poorly coded web applications or poorly secured back-end server and databases privileges. Later on, we will discuss ways to reduce the chances of being vulnerable to SQL injections through secure coding methods like user input sanitization and validation and proper back-end user privileges and control.

### Intro to Databases
Before we learn about SQL injections, we need to learn more about databases and Structured Query Language (SQL), which databases will perform the necessary queries. Web applications utilize back-end databases to store various content and information related to the web application. This can be core web application assets like images and files, content like posts and updates, or user data like usernames and passwords.

There are many different types of databases, each of which fits a particular type of use. Traditionally, an application used file-based databases, which was very slow with the increase in size. This led to the adoption of Database Management Systems (DBMS).

## Database Management Systems

A Database Management System (DBMS) helps create, define, host, and manage databases. Various kinds of DBMS were designed over time, such as file-based, Relational DBMS (RDBMS), NoSQL, Graph based, and Key/Value stores.

There are multiple ways to interact with a DBMS, such as command-line tools, graphical interfaces, or even APIs (Application Programming Interfaces). DBMS is used in various banking, finance, and education sectors to record large amounts of data. Some of the essential features of a DBMS include:

## Feature + Description

* `Concurrency`

```
A real-world application might have multiple users interacting with it simultaneously. 
A DBMS makes sure that these concurrent interactions succeed without corrupting or losing any data.
```
* `Consistency`	

```
With so many concurrent interactions, the DBMS needs to ensure that the data 
remains consistent and valid throughout the database.
```
* `Security`	

```
DBMS provides fine-grained security controls through user authentication and permissions. 
This will prevent unauthorized viewing or editing of sensitive data.
```
* `Reliability`

```
It is easy to backup databases and rolls them back to a 
previous state in case of data loss or a breach.
```
* `Structured Query Language`
	
```
SQL simplifies user interaction with the database with an 
intuitive syntax supporting various operations.
```

* ### Architecture
The diagram below details a two-tiered architecture.

<img src="https://github.com/evildevill/sql_fundamentals/blob/main/img/db_2.png"/>

Tier I usually consists of client-side applications such as websites or GUI programs. These applications consist of high-level interactions such as user login or commenting. The data from these interactions is passed to Tier II through API calls or other requests.

The second tier is the middleware, which interprets these events and puts them in a form required by the DBMS. Finally, the application layer uses specific libraries and drivers based on the type of DBMS to interact with them. The DBMS receives queries from the second tier and performs the requested operations. These operations could include insertion, retrieval, deletion, or updating of data. After processing, the DBMS returns any requested data or error codes in the event of invalid queries.

It is possible to host the application server as well as the DBMS on the same host. However, databases with large amounts of data supporting many users are typically hosted separately to improve performance and scalability.

# Types of Databases
Databases, in general, are categorized into ```Relational Databases``` and ```Non-Relational Databases.``` Only Relational Databases utilize SQL, while Non-Relational databases utilize a variety of methods for communications.

# Relational Databases
A relational database is the most common type of database. It uses a schema, a template, to dictate the data structure stored in the database. For example, we can imagine a company that sells products to its customers having some form of stored knowledge about where those products go, to whom, and in what quantity. However, this is often done in the back-end and without obvious informing in the front-end. Different types of relational databases can be used for each approach. For example, the first table can store and display basic customer information, the second the number of products sold and their cost, and the third table to enumerate who bought those products and with what payment data.

Tables in a relational database are associated with keys that provide a quick database summary or access to the specific row or column when specific data needs to be reviewed. These tables, also called entities, are all related to each other. For example, the customer information table can provide each customer with a specific ID that can indicate everything we need to know about that customer, such as an address, name, and contact information. Also, the product description table can assign a specific ID to each product. The table that stores all orders would only need to record these IDs and their quantity. Any change in these tables will affect all of them but predictably and systematically.

However, when processing an integrated database, a concept is required to link one table to another using its key, called a ```relational database management system``` (```RDBMS```). Many companies that initially use different concepts are switching to the RDBMS concept because this concept is easy to learn, use and understand. Initially, this concept was used only by large companies. However, many types of databases now implement the RDBMS concept, such as Microsoft Access, MySQL, SQL Server, Oracle, PostgreSQL, and many others.

For example, we can have a ```users``` table in a relational database containing columns like ```id```, ```username```, ```first_name```, ```last_name```, and others. The ```id``` can be used as the table key. Another table, ```posts```, may contain posts made by all users, with columns like ```id```, ```user_id```, ```date```, ```content```, and so on.
<p align="center">
<img src="https://github.com/evildevill/sql_fundamentals/blob/main/img/web_apps_relational_db.jpg"/>
</p>

We can link the ```id``` from the ```users``` table to the ```user_id``` in the ```posts``` table to retrieve the user details for each post without storing all user details with each post. A table can have more than one key, as another column can be used as a key to link with another table. So, for example, the ```id``` column can be used as a key to link the ```posts``` table to another table containing comments, each of which belongs to a particular post, and so on.

```The relationship between tables within a database is called a Schema.```

This way, by using relational databases, it becomes rapid and easy to retrieve all data about a particular element from all databases. So, for example, we can retrieve all details linked to a specific user from all tables with a single query. This makes relational databases very fast and reliable for big datasets with clear structure and design and efficient data management. The most common example of relational databases is ```MySQL```, which we will be covering in this module.

## Non-relational Databases

A non-relational database (also called a ```NoSQL``` database) does not use tables, rows, and columns or prime keys, relationships, or schemas. Instead, a NoSQL database stores data using various storage models, depending on the type of data stored. Due to the lack of a defined structure for the database, NoSQL databases are very scalable and flexible. Therefore, when dealing with datasets that are not very well defined and structured, a NoSQL database would be the best choice for storing such data. There are four common storage models for NoSQL databases:

* `Key-Value`
* `Document-Based`
* `Wide-Column`
* `Graph`
Each of the above models has a different way of storing data. For example, the ```Key-Value``` model usually stores data in JSON or XML, and have a key for each pair, and stores all of its data as its value:
<p align="center">
<img src="https://github.com/evildevill/sql_fundamentals/blob/main/img/web_apps_non-relational_db.jpg"/>
</p>

Code: ```json```
```
{
  "100001": {
    "date": "01-01-2021",
    "content": "Welcome to this web application."
  },
  "100002": {
    "date": "02-01-2021",
    "content": "This is the first post on this web app."
  },
  "100003": {
    "date": "02-01-2021",
    "content": "Reminder: Tomorrow is the ..."
  }
}
```

It looks similar to a dictionary item in languages like ```Python``` or ```PHP``` (i.e. ```{'key':'value'})```, where the ```key``` is usually a string, and the ```value``` can be a string, dictionary, or any class object.

The most common example of a NoSQL database is ```MongoDB```.
```
Non-relational Databases have a different method for injection, known as NoSQL injections.
SQL injections are completely different than NoSQL injections. NoSQL injections will be 
covered in a later module.
```

## Intro to MySQL

This module introduces SQL injection through ```MySQL```, and it is crucial to learn more about ```MySQL``` and SQL to understand how SQL injections work and utilize them properly. Therefore, this section will cover some of MySQL/SQL's basics and syntax and examples used within ```MySQL/MariaDB databases```.

## Structured Query Language (SQL)

SQL syntax can differ from one RDBMS to another. However, they are all required to follow the ISO standard for Structured Query Language. We will be following the MySQL/MariaDB syntax for the examples shown. SQL can be used to perform the following actions:

* `Retrieve data`
* `Update data`
* `Delete data`
* `Create new tables and databases`
* `Add / remove users`
* `Assign permissions to these users`

## Command Line

The ```mysql``` utility is used to authenticate to and interact with a MySQL/MariaDB database. The ```-u``` flag is used to supply the username and the ```-p``` flag for the password. The ```-p``` flag should be passed empty, so we are prompted to enter the password and do not pass it directly on the command line since it could be stored in cleartext in the ```bash_history``` file.

```
root@kali$ mysql -u root -p

Enter password: <password>
...SNIP...

mysql> 
```

Again, it is also possible the password directly into the command, though this should be avoided, as it could lead to the password being kept in logs and terminal history:

```
root@kali$ mysql -u root -p<password>

...SNIP...

mysql> 
```
```
Tip: There shouldn't be any spaces between '-p' and the password.
```

The examples above log us in as the superuser, i.e.,"```root```" with the password "```password,```" to have privileges to execute all commands. Other DBMS users would have certain privileges to which statements they can execute. We can view which privileges we have using the SHOW GRANTS command be discussed later.

When we do not specify a host, it will default to the ```localhost``` server. We can specify a remote host and port using the ```-h``` and ```-P``` flags.

```
root@kali$ mysql -u root -h docker.hackthebox.eu -P 3306 -p 

Enter password: 
...SNIP...

mysql> 
```

```
Note: The default MySQL/MariaDB port is (3306), but it can be configured to another port. It is specified using an 
uppercase `P`, unlike the lowercase `p` used for passwords.
```

```
Note: To follow along with the examples, try to use the 'mysql' tool on your PwnBox to log in to the DBMS found in the 
question at the end of the section, using its IP and port. Use 'root' for the username and 'password' for the password.
```

## Creating a database

Once we log in to the database using the ```mysql``` utility, we can start using SQL queries to interact with the DBMS. For example, a new database can be created within the MySQL DBMS using the CREATE ```DATABASE``` statement.

 ```
 mysql> CREATE DATABASE users;

Query OK, 1 row affected (0.02 sec)
 ```

MySQL expects command-line queries to be terminated with a semi-colon. The example above created a new database named `users`. We can view the list of databases with SHOW `DATABASES`, and we can switch to the `users` database with the `USE` statement:

```
mysql> SHOW DATABASES;

+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| users              |
+--------------------+

mysql> USE users;

Database changed
```

```
SQL statements aren't case sensitive, which means 'USE users;' and 'use users;' refer to the same command. However, the database name is case sensitive, so we cannot do 'USE USERS;' instead of 'USE users;'. So, it is a good practice to specify statements in uppercase to avoid confusion.
```

## Tables
DBMS stores data in the form of tables. A table is made up of horizontal rows and vertical columns. The intersection of a row and a column is called a cell. Every table is created with a fixed set of columns, where each column is of a particular data type.

A data type defines what kind of value is to be held by a column. Common examples are `numbers`, `strings`, `date`, `time`, and `binary data`. There could be data types specific to DBMS as well. A complete list of data types in MySQL can be found here. For example, let us create a table named `logins` to store user data, using the CREATE TABLE SQL query:

* Code: `sql`
```
CREATE TABLE logins (
    id INT,
    username VARCHAR(100),
    password VARCHAR(100),
    date_of_joining DATETIME
    );
```

As we can see, the `CREATE TABLE` query first specifies the table name, and then (within parentheses) we specify each column by its name and its data type, all being comma separated. After the name and type, we can specify specific properties, as will be discussed later.

```
mysql> CREATE TABLE logins (
    ->     id INT,
    ->     username VARCHAR(100),
    ->     password VARCHAR(100),
    ->     date_of_joining DATETIME
    ->     );
Query OK, 0 rows affected (0.03 sec)
```

The SQL queries above create a table named `logins` with four columns. The first column, `id` is an integer. The following two columns, `username` and `password` are set to strings of 100 characters each. Any input longer than this will result in an error. The `date_of_joining` column of type `DATETIME` stores the date when an entry was added.

```
mysql> SHOW TABLES;

+-----------------+
| Tables_in_users |
+-----------------+
| logins          |
+-----------------+
1 row in set (0.00 sec)
```

A list of tables in the current database can be obtained using the `SHOW TABLES` statement. In addition, the DESCRIBE keyword is used to list the table structure with its fields and data types.

```
mysql> DESCRIBE logins;

+-----------------+--------------+
| Field           | Type         |
+-----------------+--------------+
| id              | int          |
| username        | varchar(100) |
| password        | varchar(100) |
| date_of_joining | date         |
+-----------------+--------------+
4 rows in set (0.00 sec)
```

## Table Properties
Within the `CREATE TABLE` query, there are many properties that can be set for the table and each column. For example, we can set the `id` column to auto-increment using the `AUTO_INCREMENT` keyword, which automatically increments the id by one every time a new item is added to the table:

* Code: `sql`
```
    id INT NOT NULL AUTO_INCREMENT,
```

The `NOT NULL` constraint ensures that a particular column is never left empty 'i.e., required field.' We can also use the `UNIQUE` constraint to ensures that the inserted item are always unique. For example, if we use it with the `username` column, we can ensure that no two users will have the same username:

* Code: `sql`
```
    username VARCHAR(100) UNIQUE NOT NULL,
```
    
Another important keyword is the `DEFAULT` keyword, which is used to specify the default value. For example, within the `date_of_joining` column, we can set the default value to `Now()`, which in `MySQL` returns the current date and time:

* Code: `sql`
```
    PRIMARY KEY (id)
```

The final CREATE TABLE query will be as follows:

* Code: `sql`
```
CREATE TABLE logins (
    id INT NOT NULL AUTO_INCREMENT,
    username VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(100) NOT NULL,
    date_of_joining DATETIME DEFAULT NOW(),
    PRIMARY KEY (id)
    );
```

```
Note: Allow 10-15 seconds for the servers in the questions to start, to allow enough time for Apache/MySQL to initiate and run.
```

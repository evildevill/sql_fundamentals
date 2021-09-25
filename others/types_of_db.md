# Types of Databases
Databases, in general, are categorized into Relational Databases and Non-Relational Databases. Only Relational Databases utilize SQL, while Non-Relational databases utilize a variety of methods for communications.

# Relational Databases
A relational database is the most common type of database. It uses a schema, a template, to dictate the data structure stored in the database. For example, we can imagine a company that sells products to its customers having some form of stored knowledge about where those products go, to whom, and in what quantity. However, this is often done in the back-end and without obvious informing in the front-end. Different types of relational databases can be used for each approach. For example, the first table can store and display basic customer information, the second the number of products sold and their cost, and the third table to enumerate who bought those products and with what payment data.

Tables in a relational database are associated with keys that provide a quick database summary or access to the specific row or column when specific data needs to be reviewed. These tables, also called entities, are all related to each other. For example, the customer information table can provide each customer with a specific ID that can indicate everything we need to know about that customer, such as an address, name, and contact information. Also, the product description table can assign a specific ID to each product. The table that stores all orders would only need to record these IDs and their quantity. Any change in these tables will affect all of them but predictably and systematically.

However, when processing an integrated database, a concept is required to link one table to another using its key, called a relational database management system (RDBMS). Many companies that initially use different concepts are switching to the RDBMS concept because this concept is easy to learn, use and understand. Initially, this concept was used only by large companies. However, many types of databases now implement the RDBMS concept, such as Microsoft Access, MySQL, SQL Server, Oracle, PostgreSQL, and many others.

For example, we can have a users table in a relational database containing columns like id, username, first_name, last_name, and others. The id can be used as the table key. Another table, posts, may contain posts made by all users, with columns like id, user_id, date, content, and so on.

<img src="https://github.com/evildevill/sql_fundamentals/blob/main/img/web_apps_relational_db.jpg"/>

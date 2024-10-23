SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. <br>
A successful SQL injection attack can result in unauthorized access to sensitive data, such as: <br>
    Passwords. <br>
    Credit card details. <br>
    Personal user information <br>
Some common SQL injection examples include: <br>
    1.Retrieving hidden data, where you can modify a SQL query to return additional results. <br>
    2.Subverting application logic, where you can change a query to interfere with the application's logic. <br>
    3.UNION attacks, where you can retrieve data from different database tables. <br>
    4.Blind SQL injection, where the results of a query you control are not returned in the application's responses. <br>

```bash 
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
```
Note that ```--``` is a comment indicator in SQL. This means that the rest of the query is interpreted as a comment, effectively removing it. In this example, this means the query no longer includes ```AND released = 1.``` As a result, all products are displayed, including those that are not yet released.

Another attack:
```bash
https://insecure-website.com/products?category=Gifts'+OR+1=1--
```
This results in SQL query:
```bash
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```
The modified query returns all items where either the category is Gifts, or 1 is equal to 1. As 1=1 is always true, the query returns all items.

## Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
In this i was asked to perform a SQL injection attack that causes the application to display one or more unreleased products . In this link
```bash
https://0a2a0093037a7ee681e8a21e005c0065.web-security-academy.net/filter?category=Lifestyle
```
I added ```'+OR+1=1--``` to get the information and it worked.

## Lab: SQL injection vulnerability allowing login bypass:
This challenge asked to bypass a login page as administrator so in the username section i added ```administrator'--``` to login as now becuase of ```--``` it will not check the password. This is how i solved the lab.

# Retrieving data from other database tables:
For example, if an application executes the following query containing the user input Gifts:
```bash
SELECT name, description FROM products WHERE category = 'Gifts'
```
An attacker can submit:
```bash
' UNION SELECT username, password FROM users--
```
This causes the application to return all usernames and passwords along with the names and descriptions of products.

# Second-order SQL injection:
```First-order SQL injection``` occurs when the application processes user input from an HTTP request and incorporates the input into a SQL query in an unsafe way.
```Second-order SQL injection``` occurs when the application takes user input from an HTTP request and stores it for future use. This is usually done by placing the input into a database, but no vulnerability occurs at the point where the data is stored. Later, when handling a different HTTP request, the application retrieves the stored data and incorporates it into a SQL query in an unsafe way. For this reason, second-order SQL injection is also known as stored SQL injection.


# Examining the database
You can query the version details for the database. Different methods work for different database types. This means that if you find a particular method that works, you can infer the database type. For example, on Oracle you can execute:
```bash
SELECT * FROM v$version
```
You can also identify what database tables exist, and the columns they contain. For example, on most databases you can execute the following query to list the tables:
```bash
SELECT * FROM information_schema.tables
```

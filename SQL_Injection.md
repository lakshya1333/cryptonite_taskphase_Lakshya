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

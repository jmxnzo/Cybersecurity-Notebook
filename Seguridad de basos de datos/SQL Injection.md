SQL injections are a type of attack in which the attacker, by introducing an unexpected string into an input field, is capable of interfering with SQL statements executed in the database (BD is short for Base de Datos, which means database in Spanish).
• This type of vulnerability allows an attacker to execute commands in the database, extracting information, modifying data, or compromising the infrastructure.

Injection attacks are based on exploiting combinations of commands and data.
• Injection occurs when user input manages to escape the data context and enters the command context.

• Most vulnerabilities occur in the WHERE clause of SELECT statements. However, it is also possible for user input to end up in other parts, such as:
  - UPDATE statements, in the values to be updated or in the WHERE clause.
  - INSERT statements, in the values to be inserted.
  - SELECT statements, in the table name or column name.
  - SELECT statements, in the GROUP BY clause.


## Detect SQL Injection
1. Introduce the single quote (') and look for errors or anomalies.
2. Introduce SQL code that, when evaluated, is equivalent to an expected input and an unexpected input. Look for differences in the responses.
3. Introduce boolean conditions that evaluate as true and false ('OR 1=1', 'OR 1=2'), looking for differences in the application's responses.
4. Introduce inputs designed to provoke time delays, checking for differences in response time.



#### UNION Statement
The `UNION` statement in SQL is used to combine the results of two or more SELECT statements into a single result set. The key points to note about the `UNION` statement are:

1. The number of columns in the SELECT statements must be the same.
2. The data types of the corresponding columns in the SELECT statements must be compatible.


## Error-based SQL Injection
In some cases, the application's behavior does not change whether the result of the statement is true or false.
• However, if we can see error messages in the response when an exception occurs, it is possible to extract data even when responses are not returned.
• Error-based SQL injection refers to situations in which we can induce errors depending on a condition that we control.
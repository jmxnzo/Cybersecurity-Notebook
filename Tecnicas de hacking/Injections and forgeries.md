![[Pasted image 20231230181903.png]]

### Header types
![[Pasted image 20231230181935.png]]

### Response types
![[Pasted image 20231230182003.png]]

- Http is a stateless protocol, so the services or javascript need to implement the current state of communication
### OWASP Top 10
![[Pasted image 20231230182423.png]]

# XSS/HTML Injection
### Cross Site-Scripting
- if we can execute JavaScript code on a server, we have to deal with XSS(Cross Site Scripting)
### Prevention
Understanding how your framework protects you:
- Using specific libraries, such as DOMPurify.
- Employing secure methods (createTextNode, createElement, etc.).
- Strict data filtering.
- HTML entity encoding.
- Content Security Policy (CSP).


# Command injection
#### API examples of different languages
- PHP: exec, passthru, system, proc_open, …
- C/C++: system, execl, execvp, …
- Python: os.system, os.popen, subprocess.*, …
- Java: Runtime.exec(), ProcessBuilder, …
``` Bash
file; ls
file || ls
$(ls)
file && ls
`ls`
file | ls
```

### Out-of-band injections
![[Pasted image 20231230183103.png]]
#### Prevention
Use the API instead of commands: common operations are likely already implemented...

- Use appropriate language methods to process user input; for example, in PHP, use `escapeshellarg` and `escapeshellcmd`.
- Execute commands without shell: `popen(['cat', 'file'], ...)`.
- Implement a whitelist of permitted strings.
- Use whitelist validation with regular expressions (RegEx).

# SQL Injection
Ejemplo: operaciones comunes MySQL
• Detección n columnas: ORDER BY {1,2,3…n}
• Exfiltrar datos: UNION SELECT …
O concatenando strings: CONCAT(…, …, …)
• Nombres tablas: SELECT table_name FROM
information_schema.tables
• Nombres columnas: SELECT column_name FROM
information_schema.columns
• Recuerda, cada BBDD (Oracle, SQL Server,
MariaDB, etc) tiene su propio dialecto de SQL.
• Referencias útiles:
https://portswigger.net/web-security/sql-injection/cheat-sheet
https://book.hacktricks.xyz/pentesting-web/sql-injection
### NoSQL Injection
![[Pasted image 20231230184155.png]]
#### Prevention
https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html
- Prepared Statements / ORMs:
- Whitelist: Allowed strings.
- Whitelist: Validation with Regex.
- Escape special characters (Not recommended).
- Remember the principle of least privilege (If I only need to read from a table, why grant permissions throughout the entire database?).



# Cross Site Request Forgery
![[Pasted image 20231230201251.png]]
Requirements needed
(but not sufficient!)
1. There must be an action to perform (e.g., password change).
2. The page uses cookies to manage the user's session.
3. There are no unpredictable parameters.

#### Prevention
• Understand how your web development framework protects you if it has such functionality.
• Add an unpredictable token or parameter to each request that modifies the state.
• If it's an API, avoid using Cookies; use Authorization or equivalent.
• Specific protections: SameSite Cookies, CORS ...

# Server-side forgery
![[Pasted image 20231230201453.png]]
- for example file://localhost/etc/password


#### Prevention
• Depending on the client used to send requests, review the supported protocols and disable those that are unnecessary (file, gopher, etc.) if possible.
• Whitelist: Validate using a robust parser for domain, protocol, etc., and check if it follows the expected format.
• Disable unnecessary redirects.
• Use a firewall to block outgoing connections to certain services, or better yet, allow connections only to necessary services.
• Avoid manual checks like url.contains("127.0.0.1"); they are easy to bypass.
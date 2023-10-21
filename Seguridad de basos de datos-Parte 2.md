**1**. Crea un nuevo esquema llamado “casopractico1b”.
mysql> create database casepractice1b


**2**. Diseña el conjunto de roles y los permisos asociados a estos para cubrir las necesidades descritas por la empresa, suponiendo que los únicos permisos que se pueden dar son SELECT, INSERT, UPDATE y DELETE. Pega aquí el diagrama de la jerarquía de roles y adjunta en la entrega un Excel con una matriz de acceso en la que se especifiquen los permisos que tendrá cada rol sobre los objetos identificados.
![[casepractice1b.ods]]

**3**. Explica aquí las decisiones tomadas.

1. **Warehouse Manager and Warehouse Worker:** Warehouse Managers need full access to the 'Orders' table and additional access to the 'Stock' table. Warehouse Workers only need SELECT access to the 'Orders' table to prepare shipments.
    
2. **Sales Department:** Sales Department needs SELECT access to 'Catalog', 'Stock', and 'Orders' tables to manage products, check stock levels, and analyze demand.
    
3. **Route Organizer and Delivery Driver:** Route Organizers need SELECT access to 'Orders' to design routes. Delivery Drivers need INSERT access to the 'Deliveries' table to record deliveries.
    
4. **Accountant and Purchasing Manager:** Accountants and Purchasing Managers need full access to the 'Accounting' and 'Purchases' tables, respectively. They are mutually exclusive, so no need for extra roles.
    
5. **Security Analyst and System Administrator:** Security Analysts need SELECT and UPDATE access to the 'Users' table and SELECT access to the 'Event Log' for monitoring and restricting user access. System Administrators need additional INSERT and DELETE access on the 'Users' table for managing users.
    
6. **CAU Employee:** CAU Employees need SELECT, INSERT, and UPDATE access to the 'Incidents' table for technical support. They can INSERT into the 'Tickets' table.


**4**. Crea al menos un rol adicional que no haya sido especificado por la empresa para agrupar permisos y/o mejorar la gestión de permisos.

**5**. Explica qué otras mejoras se han introducido (si se ha hecho) y por qué has considerado que son mejoras.


![[Database.png]]
We introduced 2 new roles to the database and made changes to one of the existing roles. The new structure can be seen on top.
First we made the system administrator inherit from the security analyst, because they share all permissions. Thus each system administrator receives the roles of security analyst and the according system administrator privileges on top.

As well we made the possibility to create incident tickets a role, which owns every employee.
At last, we introduced the access to orders role to get a better overview on, who has the possibility to check orders. Since the route organizers only had the one permission, we indirectly just change the name of the role and group it together with the warehouse manager, who has read access to the orders as well.



**6**. Crea los roles en la BD mediante sentencias SQL. Pega aquí el código utilizado para ello. Nota: no utilices la tabla creada en la parte 1 del caso práctico. En su lugar, crea roles de verdad en MySQL ([https://dev.mysql.com/doc/refman/8.0/en/roles.html](https://dev.mysql.com/doc/refman/8.0/en/roles.html) ).

mysql> create role 'warehouse manager' ,'sales department', ' route organizers', 'delivery drivers', 'accountants', 'Purchasing managers',  'security analyst (d)',  'system administrator',  'CAU',  'create incident tickets',  'access to orders';
```
GRANT SELECT, INSERT, UPDATE, DELETE ON casepractice1b.stock TO 'warehouse manager';
GRANT SELECT, INSERT, UPDATE, DELETE ON casepractice1b.catalog TO 'sales department';
GRANT SELECT ON casepractice1b.stock TO 'sales department';
GRANT INSERT ON casepractice1b.deliveries TO 'delivery drivers';
GRANT SELECT, INSERT, UPDATE, DELETE ON casepractice1b.accounting TO 'accountants';
GRANT SELECT, INSERT, UPDATE, DELETE ON casepractice1b.purchases TO 'Purchasing managers';
GRANT SELECT, UPDATE ON casepractice1b.users TO 'security analyst';
GRANT SELECT ON casepractice1b.register TO 'security analyst';
GRANT INSERT, DELETE ON casepractice1b.users TO 'system administrator';
GRANT SELECT, UPDATE ON casepractice1b.incidents TO 'CAU';
GRANT INSERT ON casepractice1b.incidents TO 'create incident tickets';
GRANT SELECT ON casepractice1b.orders TO 'access to orders';


```

**7**. Comprueba que los accesos son concedidos o denegados correctamente en al menos tres situaciones diferentes. Para ello, crea usuarios ficticios a los que asignar roles para luego acceder con sus cuentas. También será necesario crear las tablas que figuran en el diagrama enviado por la empresa. Sin embargo, el contenido de las tablas carece de importancia, por lo que sus campos no tienen que reflejar la realidad (es decir, todas las tablas pueden tener únicamente un campo que sea “id”). Explica aquí qué tres situaciones has probado y cuál era el resultado esperado (acceso concedido o denegado). Pega un pantallazo del momento en el que se confirmó el acceso o la denegación de este por parte del SGBD.

The clause following the `DEFAULT ROLE` keywords permits these values:

- `NONE`: Set the default to `NONE` (no roles).
    
- `ALL`: Set the default to all roles granted to the account.

```
CREATE USER 'warehouse manager 1' IDENTIFIED BY 'Password123#@!';
CREATE USER 'delivery driver 1' IDENTIFIED BY 'Password123#@!';
CREATE USER 'system administrator 1' IDENTIFIED BY 'Password123#@!';
SET DEFAULT ROLE ALL TO 'warehouse manager 1', 'system administrator 1', 'delivery driver 1';
GRANT 'warehouse manager' TO 'warehouse manager 1';
GRANT 'delivery drivers' TO 'delivery driver 1';
GRANT 'system administrator' TO 'system administrator 1';
GRANT 'security analyst' TO 'system administrator 1';
GRANT 'access to orders' TO 'warehouse manager 1';
GRANT 'create incident tickets' TO 'warehouse manager 1';
GRANT 'create incident tickets' TO 'delivery driver 1';
GRANT 'create incident tickets' TO 'system administrator 1';
```


Testing warehouse manager:
- warehouse manager should have all access rights on the stock table, that's why all of the queries should work.
```
## check all access rights for stock
mysql> Select * from stock;
+------------+----------+
| product_id | quantity |
+------------+----------+
|          9 |       17 |
|        376 |       63 |
+------------+----------+
2 rows in set (0.00 sec)

mysql> INSERT INTO stock (product_id, quantity)
    -> VALUES (101, 50);
Query OK, 1 row affected (0.01 sec)

## checking if insert worked 
mysql> select * from stock;
+------------+----------+
| product_id | quantity |
+------------+----------+
|          9 |       17 |
|        101 |       50 |
|        376 |       63 |
+------------+----------+
3 rows in set (0.00 sec)

mysql> UPDATE stock SET quantity = 75 WHERE product_id = 9;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> DELETE FROM stock
    -> WHERE product_id = 101;
Query OK, 1 row affected (0.01 sec)

## checking that the stock was updated the right way
mysql> select * from stock;
+------------+----------+
| product_id | quantity |
+------------+----------+
|          9 |       75 |
|        376 |       63 |
+------------+----------+
2 rows in set (0.00 sec)

```


Testing delivery driver:
```
## Insert a new delivery record with specific values
mysql> INSERT INTO deliveries (delivery_id,order_id, delivery_date, delivery_sta
tus)
    -> VALUES (2002, 101, '2023-10-19', 'Delivered');
Query OK, 1 row affected (0.01 sec)

```

using root user to check the insert(delivery driver is only allowed to insert, but not select from the deliveries):
```
mysql> select * from deliveries;
+-------------+----------+---------------+-----------------+
| delivery_id | order_id | delivery_date | delivery_status |
+-------------+----------+---------------+-----------------+
|        2002 |      101 | 2023-10-19    | Delivered       |
+-------------+----------+---------------+-----------------+
1 row in set (0.00 sec)
```

Testing system administrator insert:
- system administrator should be able to insert new users to the system
```
mysql> INSERT INTO users (user_id, username, role, email)
    -> VALUES (101, 'newuser1', 'employee', 'newuser1@example.com');
Query OK, 1 row affected (0.01 sec)
mysql> SELECT * FROM users;
+---------+----------+----------+----------------------+
| user_id | username | role     | email                |
+---------+----------+----------+----------------------+
|     101 | newuser1 | employee | newuser1@example.com |
+---------+----------+----------+----------------------+
1 row in set (0.00 sec)


```

Testing incidents table(as warehouse manager):
```

## test insert to incidents
mysql> INSERT INTO incidents (incident_id, user_id, incident_date, description)
    -> VALUES
    ->     (1, 301, '2023-10-19', 'Network connectivity issue in office A'),
    ->     (2, 302, '2023-10-20', 'Server outage in data center'),
    ->     (3, 303, '2023-10-21', 'Security breach attempt detected'),
    ->     (4, 304, '2023-10-22', 'Employee reported suspicious email'),
    ->     (5, 305, '2023-10-23', 'Printer malfunction in department B');
Query OK, 5 rows affected (0.01 sec)
Records: 5  Duplicates: 0  Warnings: 0

## test select from incidents, which should fail
mysql> select * from incidents
    -> ;
ERROR 1142 (42000): SELECT command denied to user 'warehouse manager 1'@'localhost' for table 'incidents'

```

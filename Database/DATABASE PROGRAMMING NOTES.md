# DATABASE PROGRAMMING

## DATABASE

Database refers to organized files for storing and retrieving information.

## Veritabanı Yönetim Sistemi (Database Management System)

These are specialized software for database operations.

### FEATURES

- Aşağı seviyeli dosya formatlarıyla kullanıcının ilişkisin kesilmesi --> VTYS'lerde kullanıcıların, bilgilerin hangi dosyalarda ve nasıl organize edildiğini bilmeleri gerekmez / Black Box
- VTYS ler genel olarak yüksek seviyeleri deklaratif dillerle kullanıcı isteklerini yerine getirirler --> Structured Query Language (SQL)
- VTYS ler genel olarak client-server çalışma modeline sahiptir --> Birden fazla kullanıcı VTYS'ye istekte bulunabilir. VTYS bu istekleri karşılar
- VTYS lerin çoğu yardımcı bir takım araçlar da içerirler --> backup-restore programları, yönetici programlar vb.
- VTYS lerde belli düzeylerde güvenlik ve güvenilirlik (security and safety/reliability) mekanizması oluşturulmuştur --> SQL Injection Attack - ATOM

## SQL Kategorileri

SQL için iki temel kategori vardır: DDL (Data Definition Language), DML (Data Manipulation Language)

### DDL (Data Definition Language)

Komutlar veritabanının yapısını ve özelliklerini tanımlar. Bu komutlar, veritabanındaki tablo ve görünümlerin oluşturulması, silinmesi ve değiştirilmesi gibi işlemleri gerçekleştirir.

### DML (Data Manipulation Language)

Komutlar veritabanındaki verilere erişim ve veriler üzerinde değişiklikler yapmayı sağlar. Bu komutlar, verilerin eklenmesi, güncellenmesi ve silinmesi gibi işlemleri gerçekleştirir. "CRUD" işlemleri.

## Veritabanı Tablo İlişkileri

- One-to-one relationship: One record of the first table is linked to zero or one record of another table. It is used to create a relationship between two tables in which a single row of the first table can only be related to one and only one record of a second table.
- One-to-many relationship: This relationship indicates that one item can be related to one or more other items. It is used to create a relationship between two tables. Any single rows of the first table can be related to one or more rows of the second tables, but the rows of second tables can only relate to the only row in the first table.
- Many-to-many relationship: This relationship indicates that one item can be related to one or more other items, and at the same time, other items can also be related to one or more items. Many-to-Many relationship lets you relate each row in one table to many rows in another table and vice versa.

To create table relationships, the "FOREIGN KEY" command is used in the SQL language used in database management systems. This command indicates that one table is related to another table and defines the relationship. "foreign key verirken primary key ile aynı verilmesi önerilir"

## CASCADE

Is used to simultaneously delete or update an entry from both the child and parent table. The keyword CASCADE is used as a conjunction while writing the query of ON DELETE or ON UPDATE.

Inner join - self join diff: Teoride aynı ama self join de aynı ilişkiyi mantıksal vermiş oluyoruz. Self join - inner join'e göre daha yavaş.

In SQL, there are three set operators that can be used to combine the results of two or more SELECT statements: "UNION, INTERSECT, EXCEPT".

### UNION / UNION ALL

Is used to combine the results of two or more SELECT statements into a single result set.

```sql
SELECT column1, column2, ...
FROM table1
UNION -- removing any duplicate rows.
SELECT column1, column2, ...
FROM table2;
```

### INTERSECT

Is used to return only the rows that are present in both result sets.

```sql
SELECT column1, column2, ...
FROM table1
INTERSECT
SELECT column1, column2, ...
FROM table2;
```

### EXCEPT

Is used to return only the rows that are present in the first result set but not in the second result set.

```sql
SELECT column1, column2, ...
FROM table1
EXCEPT
SELECT column1, column2, ...
FROM table2;
```

## Normalizasyon (Normalization)

Used to eliminate redundant data and improve performance, data integrity, and organization. Normalization generally aims to:

- Performansı artırmak
- Veri bütünlüğünü sağlamak
- Veriler daha iyi organize edilir
- Gereksiz tekrarlar olmadığından verinin kapladığı alan da azalmış olur
- Veriler daha anlaşılır olur
- Normalizasyon ile "primary key-foreign key" ilişkileri de belirlendiğinden VTYS sorguları daha hızlı çalıştırma imkanı bulabilir.

```sql
Customer ID | Customer Name | Phone Numbers
--------------------------------------------
101        | John Smith    | 555-1234, 555-5678
102        | Jane Doe      | 555-4321, 555-8765

```

#### Birinci Normal Form (1NF)

Tablo içerisinde tekrarlayan alanlar bulunmaz, Her alanda yalnızca bir değer bulunur. First Normal Form requires that each column in a table contains atomic (indivisible) values, and each row must be unique.

```sql
Customer ID | Customer Name
---------------------------
101        | John Smith
102        | Jane Doe
```

```sql
Customer ID | Phone Number
--------------------------
101        | 555-1234
101        | 555-5678
102        | 555-4321
102        | 555-8765
```

#### İkinci Normal Form (2NF)

Bunun için önce 1NF olmalıdır. Her kayıt için primary key olmaldıır. Anahtar değerler ile varsa kompozit anahtarlar arasında parçalı bir bağımlılık bulunmamalıdır. Ana tablo ile diğer tablolar arasında foreign key ilişkisi kurulmalıdır. Second Normal Form requires that each non-key column in a table is fully dependent on the entire primary key.

```sql
Store ID | Product ID | Product Name | Store Name | Sales Date  | Sales Amount
-------------------------------------------------------------------------------
1       | 101        | Apple        | Store A    | 2021-01-01 | 1000
1       | 102        | Banana       | Store A    | 2021-01-01 | 2000
2       | 101        | Apple        | Store B    | 2021-01-01 | 1500
2       | 102        | Banana       | Store B    | 2021-01-01 | 2500
```

```sql
Store ID | Store Name
---------------------
1       | Store A
2       | Store B

Product ID | Product Name
-------------------------
101       | Apple
102       | Banana

Sales ID | Store ID | Product ID | Sales Date  | Sales Amount
------------------------------------------------------------
1       | 1        | 101        | 2021-01-01 | 1000
2       | 1        | 102        | 2021-01-01 | 2000
3       | 2        | 101        | 2021-01-01 | 1500
4       | 2        | 102        | 2021-01-01 | 2500
```

#### Üçüncü Normal Form (3NF)

Bunun için önce 2NF olmalıdır. Her alan primary key alanına tam bağımlı olmalıdır. A table should not contain transitive dependencies where some columns depend on other non-key columns.

```sql
Order ID | Customer ID | Customer Name | Product ID | Product Name | Product Category | Product Price
---------------------------------------------------------------------------------------------------
1        | 101         | John Smith     | 001        | iPhone        | Electronics      | 1000
2        | 102         | Jane Doe       | 002        | MacBook Pro   | Electronics      | 2000
3        | 101         | John Smith     | 003        | T-shirt       | Clothing         | 20
4        | 103         | Bob Johnson    | 002        | MacBook Pro   | Electronics      | 2000
```

```sql
Table 1: Customers
-------------------
Customer ID | Customer Name
--------------------------
101        | John Smith
102        | Jane Doe
103        | Bob Johnson

Table 2: Products
------------------
Product ID | Product Name    | Product Category | Product Price
------------------------------------------------------------
001        | iPhone           | Electronics      | 1000
002        | MacBook Pro      | Electronics      | 2000
003        | T-shirt          | Clothing         | 20

Table 3: Orders
----------------
Order ID | Customer ID | Product ID
-----------------------------------
1        | 101         | 001
2        | 102         | 002
3        | 101         | 003
4        | 103         | 002
```

---

# POSTGRESQL

## Select

```sql
select * from games;
```

## Insert

```sql
insert into games (name, publisher, release_date, is_available) values ('Fifa 2022', 'Electronic Arts', '2022-03-23', true);
```

### Many Insert

```sql
INSERT INTO employees (name, age, salary)
VALUES
('John', 35, 4500),
('Jane', 28, 3500),
('Mike', 40, 5000);

insert into card_types (description) values ('Visa'), ('Master'), ('Amex');
```

## Update

```sql
update games set is_available = not is_available where publisher='Yabox';
```

## Delete

```sql
delete from games where is_available = false and publisher = 'Yabox';
```

## Inner Join

```sql
select g.name, g.release_date
from players_to_games ptg inner join games g on ptg.game_id = g.game_id 
where start_date = '2022-11-19' and g.is_available = true;
```

Standard SQL, or in other words, CRUD operations in SQL are not considered programming languages. However, SQL and all language features, including the "plpgsql" language used in PostgreSQL, are considered programming languages.

Anonymous Block ("do block"): PL/pgSQL is a block-structured language. In PostgreSQL, a block of code can be marked as anonymous by being enclosed in the DO keyword. This is known as a "DO block". It allows the execution of multiple SQL statements as a single transaction.

```sql
do $$
declare
    a int;
    b integer = 10;
    c varchar(10);
begin
    a = 20;
    b := b + 3;
    c = 'csd';
    
    raise notice 'a = %, b = %, c = %', a, b, c;
end
$$;
```

After creating a function, it needs to be called to execute its code. The language used in a function must be specified when creating it.

```sql
create or replace function add_two_ints(a int, b int)
returns int as $$
declare
    result int = a + b;
begin
    return result;
end
$$ language plpgsql;
```

Function Overloading is supported in PostgreSQL, allowing multiple functions with the same name but different parameters.

```sql
create or replace function add_two_ints(int, int)
returns int as $$
begin
    return $1 + $2;
end
$$ language plpgsql;
```

## String Functions:

- ASCII: Return the ASCII code value of a character or Unicode. (e.g., `ASCII('A')` returns 65)
- CHR: Convert an ASCII code to a character or a Unicode code. (e.g., `CHR(65)` returns 'A')
- CONCAT: Concatenate two or more strings into one. (e.g., `CONCAT('A','B','C')` returns 'ABC')
- CONCAT_WS: Concatenate strings with a separator. (e.g., 'A,B,C')
- REPEAT: Repeat a string the specified number of times. (e.g., `REPEAT('*', 5)` returns '*****')
- INITCAP: Convert words in a string to title case. (e.g., `INITCAP('hI tHERE')` returns 'Hi There')
- LOWER: Convert a string to lowercase. (e.g., `LOWER('hI tHERE')` returns 'hi there')
- UPPER: Convert a string to uppercase. (e.g., `UPPER('hI tHERE')` returns 'HI THERE')
- LEFT: Return the first n characters in a string. (e.g., `LEFT('ABC', 1)` returns 'A')
- RIGHT: Return the last n characters in the string. (e.g., `RIGHT('ABC', 2)` returns 'BC')
- REPLACE: Replace all occurrences in a string of a substring from with substring to. (e.g., `REPLACE('ABC','B','A')` returns 'AAC')

### SELECT INTO

```sql
SELECT column1, column2, ... INTO variable_name
FROM table_name
WHERE ...;
```

```sql
CREATE OR REPLACE FUNCTION get_phone_code_by_city_name(city_name varchar)
returns varchar as
$$
DECLARE
    phone_code varchar;
BEGIN
    SELECT phone_code FROM cities c WHERE c.city_name = $1 INTO phone_code;
    RETURN phone_code;
END
$$ language plpgsql;
```

```sql
-- The following is equivalent to SELECT * INTO new_table FROM old_table WHERE condition;
-- It creates a new table named "new_table" and inserts into it the data returned by the query of "old_table" where the condition is met.
CREATE TABLE new_table AS
SELECT *
FROM old_table
WHERE condition;
```

## COALESCE

`COALESCE` is used to return the first non-null value in a list of expressions. The function evaluates arguments from left to right until it finds the first non-null argument. It provides the same functionality as NVL or IFNULL function provided by SQL-standard, allowing you to handle null values by returning a specified value.

Example:

```sql
DECLARE 
    my_variable1 INTEGER;
    my_variable2 INTEGER;
    my_variable3 INTEGER;
BEGIN
    my_variable1 := NULL;
    my_variable2 := 2;
    my_variable3 := 3;
    RAISE NOTICE 'First non-null value: %', COALESCE(my_variable1, my_variable2, my_variable3);
END;
```

## OUT FUNCTIONS

OUT functions are used to pass a value out of a function and back to the calling application or script. An OUT parameter is similar to a regular function parameter, but its value is modified by the function and then returned to the caller when the function completes.

Example:

```sql
CREATE OR REPLACE FUNCTION get_add_subtract_multiply(a int, b int, OUT sum int, OUT sub int, OUT mul int)
AS
$$
BEGIN
    sum = a + b;
    sub = a - b;
    mul = a * b;
END
$$ language plpgsql;
```

## VOID FUNCTIONS

A VOID function is a function that does not return any value. The `RETURNS VOID` keyword is used in the function definition.

Example:

```sql
CREATE OR REPLACE FUNCTION function_name(parameter_list)
RETURNS VOID
AS $$
BEGIN
   -- Function body goes here
END $$
LANGUAGE language_name;
```

## TABLE-VALUED FUNCTION (TVF)

A table-valued function is a function that returns a table as its result.

Example:

```sql
CREATE FUNCTION function_name (parameter1 datatype, parameter2 datatype)
RETURNS TABLE (column1 datatype, column2 datatype) 
AS $$
    SELECT ...
$$ LANGUAGE SQL;
```

## IF - ELSE - ELSE IF - STATEMENT

The `IF...ELSE` statement in PostgreSQL is used to perform conditional logic in a query. It can be used in different variations, including the use of `ELSE IF` for multiple conditions.

```sql
DO $$ 
DECLARE
    min INT = -10;
    bound INT = 10;
    val INT = ROUND(RANDOM() * (bound - min) + min);
BEGIN
    IF val > 0 THEN
        RAISE NOTICE '% is positive', val;
    ELSIF val = 0 THEN
        RAISE NOTICE 'zero';
    ELSE
        RAISE NOTICE '% is negative', val;
    END IF;
END $$;
```

## CASE END CASE STATEMENT

The `CASE...END` statement in PostgreSQL is another way to perform conditional logic in a query, similar to the `IF...ELSE` statement.

```sql
SELECT 
    product_name, 
    price, 
    CASE
        WHEN price < 50 THEN 'Discounted' 
        WHEN price >= 50 AND price < 100 THEN 'Regular'
        ELSE 'Expensive'
    END AS price_category
FROM products;
```

## DATE FUNCTIONS

### EXTRACT

`EXTRACT` is used to extract a specific field from a date or timestamp value.

```sql
SELECT EXTRACT(MONTH FROM '2022-12-25'::DATE);
```

### NOW()

`NOW()` is used to get the current timestamp.

### AGE()

`AGE()` is used to calculate the difference between two dates.

```sql
SELECT AGE(birthdate, CURRENT_DATE) FROM people;
```

### CURRENT_DATE, CURRENT_TIME, CURRENT_TIMESTAMP

These functions return the current date, time, and timestamp, respectively.

```sql
RAISE NOTICE '%', CURRENT_DATE;
RAISE NOTICE '%', CURRENT_TIME;
RAISE NOTICE '%', CURRENT_TIMESTAMP;
```

### DATE_PART

`DATE_PART` returns a specific part of a date/time value.

```sql
SELECT DATE_PART('year', timestamp '2023-01-01');
```

### TO_DATE

`TO_DATE` is used to convert a string representation of a date into a date value.

```sql
SELECT TO_DATE('2022-01-01', 'YYYY-MM-DD');
```

### DATE_TRUNC

`DATE_TRUNC` is used to truncate a timestamp to a specific precision.

```sql
DATE_TRUNC('field', timestamp)
```

Where `'field'` is the precision to which the timestamp should be truncated, and `timestamp` is the input timestamp. The precision can take various values, and each value represents a different time unit. Here are the possible values for the `field` parameter:

- 'millennium'
- 'century'
- 'decade'
- 'year'
- 'quarter'
- 'month'
- 'week'
- 'day'
- 'hour'
- 'minute'
- 'second'
- 'milliseconds'
- 'microseconds'

```sql
SELECT DATE_TRUNC('month', TIMESTAMP '2022-12-25');
```


### Stored Procedure

A stored procedure in PostgreSQL is a precompiled block of code that is stored in the database and can be executed on demand. Unlike functions, stored procedures in PostgreSQL do not have a return value concept, and they are called using the `CALL` statement.

```sql
CREATE OR REPLACE PROCEDURE procedure_name ([parameter_list])
LANGUAGE [language_name]
AS $$
DECLARE
   -- local variables go here
BEGIN
   -- code goes here
END;
$$;
```

```sql
CREATE OR REPLACE PROCEDURE sp_insert_animal(int, varchar(100), date, varchar(100))
LANGUAGE plpgsql
AS $$
BEGIN
   INSERT INTO animals (owner_id, name, birth_date, type) VALUES ($1, $2, $3, $4);
END
$$;
```

Stored procedures are called using the `CALL` statement:

```sql
CALL sp_insert_animal(1, 'Foo', '2015-09-20', 'Street cat');
```

### LOOP

#### Infinite LOOP

```sql
DO $$
DECLARE
   i INT = 1;
   n INT = 10;
BEGIN
   LOOP
      RAISE NOTICE 'i = %', i;
      EXIT WHEN i = n;
      i = i + 1;
   END LOOP;
END;
$$;
```

#### WHILE LOOP

```sql
DO $$
DECLARE
   i INT = 1;
   count INT = 10;
BEGIN
   WHILE i <= count LOOP
      RAISE NOTICE 'i = %', i;
      i = i + 1;
   END LOOP;
END;
$$;
```

#### FOR LOOP

```sql
DO $$
DECLARE
   count INT = 10;
BEGIN
   FOR i IN 1..count BY 2 LOOP
      RAISE NOTICE 'i = %', i;
   END LOOP;
END;
$$;
```

### ARRAY

PostgreSQL arrays contain a collection of elements of the same data type, indexed starting from 1. Arrays can be created using the array type or the ARRAY syntax.

```sql
-- Using array type
CREATE TABLE mytable (
   myarray INTEGER[]
);

-- Using ARRAY syntax with default values
CREATE TABLE mytable (
   myarray INTEGER[] DEFAULT '{1,2,3}'
);

-- Querying with ANY
SELECT * FROM mytable WHERE 5 = ANY(myarray);
```

### TRIGGER

Before creating a trigger in PostgreSQL, a trigger function must be written. The trigger function should return either `NEW` or `OLD` values, representing the new and old data. Here are examples of `BEFORE` and `AFTER` triggers:

#### BEFORE Trigger

```sql
CREATE OR REPLACE FUNCTION port_insert_before_trigger()
RETURNS TRIGGER
AS $$
BEGIN
   IF 1024 <= NEW.num AND NEW.num <= 65535 THEN
      RETURN NEW;
   END IF;

   RETURN OLD;
END;
$$ LANGUAGE plpgsql;
```

#### AFTER Trigger

```sql
CREATE OR REPLACE FUNCTION port_insert_after_trigger()
RETURNS TRIGGER
AS $$
BEGIN
   IF 1024 <= NEW.num AND NEW.num <= 65535 THEN
      RETURN NEW;
   END IF;

   RETURN OLD;
END;
$$ LANGUAGE plpgsql;
```

Creating triggers:

```sql
CREATE TRIGGER t_port_insert_before
BEFORE INSERT ON ports
FOR EACH ROW EXECUTE FUNCTION port_insert_before_trigger();

CREATE TRIGGER t_port_insert_after
AFTER INSERT ON ports
FOR EACH ROW EXECUTE FUNCTION port_insert_after_trigger();
```

The `FOR EACH ROW EXECUTE FUNCTION` expression specifies that the trigger will be executed for each row.

### VIEW

In PostgreSQL, a view can be created using the `CREATE VIEW` or `CREATE OR REPLACE VIEW` statements. The `WITH CHECK OPTION` option can be used for updatable views, ensuring that insert, update, and delete operations adhere to a specified condition.

```sql
CREATE OR REPLACE VIEW v_devices_ports_count
AS
SELECT d.device_id, COUNT(*) AS port_count
FROM devices d
INNER JOIN ports p ON d.device_id = p.device_id
GROUP BY d.device_id
ORDER BY d.device_id;
```

```sql
CREATE OR REPLACE VIEW v_devices_use_well_known_ports
AS
SELECT * FROM ports
WHERE num < 1024
WITH CHECK OPTION;
```
### MATERIALIZED VIEW

Materialized views in PostgreSQL store results as a cached table, providing faster access. Unlike regular views, changes in the underlying tables are not automatically reflected. The `REFRESH MATERIALIZED VIEW` statement is used to update the materialized view.

```sql
CREATE MATERIALIZED VIEW employee_department_info AS
SELECT e.employee_id, e.first_name, e.last_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
```

### TRUNCATE

The `TRUNCATE` statement in PostgreSQL quickly removes all records from a table. Unlike `DELETE`, it does not delete rows one by one, making it faster. It also restarts identity columns by default.

```sql
-- Truncate all records from the 'ports' table
TRUNCATE ports;

-- Truncate all records from the 'devices' table and cascading to related tables
TRUNCATE devices CASCADE;

-- Truncate all records from the 'devices' table and restart identity columns
TRUNCATE devices RESTART IDENTITY CASCADE;
```

### OFFSET, FETCH

- `OFFSET`: Specifies the starting point for the result set in a query.
- `FETCH`: Used to retrieve a specific number of rows in a query result.

#### Example: Using OFFSET and FETCH

```sql
-- Skip the first 5 rows and fetch the next 10 rows
SELECT * FROM mytable OFFSET 5 FETCH NEXT 10 ROWS ONLY;
```

### CURSOR

A cursor in PostgreSQL is a mechanism for traversing the result set of a query. Cursors are often used inside functions.

#### Example: Using a Cursor
```sql
CREATE OR REPLACE FUNCTION get_ports_by_device_id(id INT, delimiter TEXT)
RETURNS TEXT
AS $$
DECLARE
   ports_str TEXT DEFAULT '';
   port_info RECORD;
   crs_ports CURSOR (id INT) FOR SELECT p.port_id AS pid, p.num AS number
                                   FROM ports p INNER JOIN devices d ON d.device_id = p.device_id
                                   WHERE d.device_id = id;
BEGIN
   OPEN crs_ports(id);

   LOOP
      FETCH crs_ports INTO port_info;
      EXIT WHEN NOT FOUND;

      IF ports_str <> '' THEN
         ports_str = ports_str || delimiter;
      END IF;

      ports_str = ports_str || port_info.number || ':' || port_info.pid;
   END LOOP;

   CLOSE crs_ports;
   RETURN ports_str;
END;
$$ LANGUAGE plpgsql;
```

Usage:
```sql
SELECT * FROM get_ports_by_device_id(1, ', ');
```

**Note**: There's no need to use `DEALLOCATE` for cursors in PostgreSQL. Cursors are automatically closed when the function or transaction ends.

### TRANSACTION

In PostgreSQL, a transaction is initiated with `BEGIN` and continues until either `COMMIT` or `ROLLBACK` commands are executed. The `SAVEPOINT` command allows partial rollbacks, acting as a checkpoint within a transaction.

#### Example: Using Transactions with Savepoints

```sql
BEGIN;
CREATE TABLE sensors (
    sensor_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    host VARCHAR(100) NOT NULL,
    port INT CHECK (port > 1023) NOT NULL,
    register_datetime TIMESTAMP DEFAULT(current_timestamp) NOT NULL
);

CREATE TABLE sensor_data (
    port_id BIGSERIAL PRIMARY KEY,
    sensor_id INT REFERENCES sensors(sensor_id) NOT NULL,
    value DOUBLE PRECISION,
    measure_datetime TIMESTAMP
);

SAVEPOINT tables_created_point;

INSERT INTO sensors (name, host, port)
VALUES
('test', '192.168.1.123', 33000),
('weather', '192.168.1.122', 33001);

SELECT * FROM sensors;

ROLLBACK TO tables_created_point;
COMMIT;
```

### XML OPERATIONS

#### `xmlcomment` Function

```sql
DO $$
DECLARE
   data XML;
BEGIN
   data = xmlcomment('This is comment');
   RAISE NOTICE '%', data;
END
$$;
```

#### `xmlconcat` Function
```sql
CREATE OR REPLACE FUNCTION create_xml_with_comment(data XML, comment VARCHAR(50))
RETURNS XML
AS $$
BEGIN
   RETURN xmlconcat(xmlcomment(comment), data);
END;
$$ LANGUAGE plpgsql;

DO $$
DECLARE
   data XML;
BEGIN
   data = create_xml_with_comment('
   <book id="1" name="Cin Ali Lunaparkta">
      <chapters>
         <chapter id="1" name="Hazırlanma"/>
         <chapter id="2" name="Evden çıkış"/>
         <chapter id="3" name="Lunaparka varış"/>
      </chapters>
   </book>', 'this is a text');

   INSERT INTO books (name, ISBN, chapter_summary) VALUES ('Cin Ali Lunaparkta', '1234567', data);
   RAISE NOTICE '%', data;
END
$$;

#### `xmlforest` Function

```plpgsql
CREATE OR REPLACE FUNCTION get_book_as_xml(name VARCHAR, isbn VARCHAR)
RETURNS XML
AS $$
BEGIN
   RETURN xmlelement(name book, xmlforest(name AS name, isbn AS isbn));
END;
$$ LANGUAGE plpgsql;

SELECT get_book_as_xml(name, isbn) FROM books;
```

#### `xmlelement` and `xmlattribute` Functions

```sql
DO $$
DECLARE
   data XML;
BEGIN
   data = xmlelement(name sensors, xmlattributes('1' AS id, 'weather' AS name));
   RAISE NOTICE '%', data;
END;
$$;
```

### JSON OPERATIONS

#### JSON Functions

```sql
CREATE TABLE books (
    book_id SERIAL PRIMARY KEY,
    name VARCHAR(250) NOT NULL,
    ISBN VARCHAR(30),
    chapter_summary JSON NOT NULL
);

CREATE OR REPLACE PROCEDURE sp_insert_book(VARCHAR, VARCHAR, JSON)
LANGUAGE plpgsql
AS $$
BEGIN
    INSERT INTO books (name, ISBN, chapter_summary) VALUES ($1, $2, $3);
END;
$$;

CALL sp_insert_book('Cin Ali Lunaparkta', '12345', '{
  "book": {
    "id": "1",
    "name": "Cin Ali Lunaparkta",
    "chapters": [
      {"id": 1, "name": "Hazırlanma"},
      {"id": 2, "name": "Evden çıkış"},
      {"id": 3, "name": "Lunaparka varış"}
    ]
  }
}');
```
#### Accessing JSON Data
```sql
SELECT chapter_summary FROM books;

SELECT chapter_summary -> 'book' FROM books;
SELECT chapter_summary ->> 'book' FROM books;

SELECT chapter_summary -> 'book', chapter_summary ->> 'book' FROM books;
SELECT chapter_summary -> 'book' ->> 'name' FROM books;
SELECT CAST(chapter_summary -> 'book' ->> 'id' AS INT) * 2 FROM books;

SELECT SUM(CAST(chapter_summary -> 'book' ->> 'totalPage' AS INT)) FROM books;
SELECT json_array_element(chapter_summary -> 'book' -> 'chapters', 0) -> 'name' FROM books;
SELECT json_array_element_text(chapter_summary -> 'book' -> 'chapters', 0) FROM books;
```

### USER TRANSACTION 

#### Creating Roles in PostgreSQL

```sql 
-- Creating roles with different attributes
CREATE ROLE abbas LOGIN PASSWORD '123456';
CREATE ROLE deniz SUPERUSER LOGIN PASSWORD '1234';
CREATE ROLE erol CREATEDB LOGIN PASSWORD '12345';
CREATE ROLE erdem WITH LOGIN PASSWORD '2345' VALID UNTIL '2023-05-27 22:10';
CREATE ROLE huseyin WITH LOGIN PASSWORD '2345' VALID UNTIL '2023-05-27';
CREATE ROLE weather_info_api LOGIN PASSWORD 'csd1993' CONNECTION LIMIT 1000;

-- Querying roles
SELECT rolname FROM pg_roles WHERE rolname = 'weather_info_api';
SELECT * FROM pg_roles WHERE rolname = 'weather_info_api';
SELECT * FROM pg_roles WHERE rolname = 'abbas';

-- Updating role attributes
UPDATE pg_roles SET rolcreaterole = TRUE WHERE rolname = 'abbas';
```

#### Granting and Revoking Privileges

```sql
-- Granting select, insert, delete privileges on the 'books' table to the 'erdem' role
GRANT SELECT, INSERT, DELETE ON books TO erdem;

-- Revoking select, insert, delete privileges on the 'games' table from the 'erdem' role
REVOKE SELECT, INSERT, DELETE ON games FROM erdem;
```

# MSSQL (Microsoft SQL Server)

#### Variable Declaration and Assignment

```sql
-- DECLARE is used to create variables
DECLARE @variable_name data_type [ = value];

-- SET is used to assign a value to a variable
SET @variable_name = value;

-- Example
DECLARE @count INT = 10;
SET @count = @count + 5;
```

In T-SQL, variable names start with '@' during declaration and access.

#### Table-Valued Function (TVF)

```sql
-- TVF that returns a table
CREATE FUNCTION function_name (
    @parameter1 datatype,
    @parameter2 datatype
)
RETURNS TABLE
AS
RETURN (
    -- Query to define the returned table
    SELECT ...
);
```

#### Scalar Function
```sql
-- Scalar function that returns a single value
CREATE FUNCTION function_name (@parameter1 data_type, @parameter2 data_type)
RETURNS return_data_type
AS
BEGIN
   -- Function logic
   RETURN value;
END;
```

#### Side Effect and Functions

In T-SQL, functions, including scalar functions and table-valued functions, are not allowed to have side effects. They cannot change the state of the database or modify data.

#### String Concatenation

In T-SQL, the '+' operator is used for string concatenation.

```sql
DECLARE @result VARCHAR(100);
SET @result = 'Hello' + ' ' + 'World';
```

#### Substring Function

```sql
-- SUBSTRING function
SUBSTRING(string_expression, start, length)
```

#### IF Statement

```sql
-- IF statement for conditional execution
IF Boolean_expression
BEGIN
   -- SQL statements
END
ELSE
BEGIN
   -- SQL statements
END
```

#### NULL Value Checking

For NULL value checking, IS or IS NOT operators can be used.

#### CASE Statement

```sql
-- CASE statement for conditional logic
CASE
    WHEN Boolean_expression THEN result_expression
    [WHEN Boolean_expression THEN result_expression]
    ...
    [ELSE result_expression]
END
```

#### Date and Time Types

- `date`: Stores only the date.
- `time`: Stores only the time.
- `datetime`: Stores both the date and time.
- `datetime2`: Similar to `datetime` with a larger range and more precise fractional seconds.
- `smalldatetime`: Stores both the date and time with a smaller range and less precision.
- `datetimeoffset`: Stores both the date and time, along with the time zone offset.

#### Date and Time Functions

- `GETDATE()`, `SYSDATETIME()`, `GETUTCDATE()`, `SYSUTCDATETIME()`: Obtain current date and time.
- `DATEPART()`: Extract parts of a date or datetime.
- `DATEDIFF()`: Calculate the difference between two dates or datetimes.
- `DATEFROMPARTS()`: Create a date from individual parts.
- `DATETIMEFROMPARTS()`: Create a datetime from individual parts.
- `EOMONTH()`: Return the last day of the month.

#### Identity Value and @@IDENTITY

`@@IDENTITY` is used to obtain the last identity value generated for any table in the current session.

### Stored Procedures (SP)

Stored procedures are pre-compiled collections of SQL statements. They are created using the `CREATE PROCEDURE` statement and executed using `EXEC` or `EXECUTE`.

Example:

```sql
-- Creating a stored procedure
CREATE PROCEDURE sp_insert_reservation(
    @description NVARCHAR(MAX),
    @reservation_date DATE,
    @start_date DATE,
    @end_date DATE
)
AS
BEGIN
    INSERT INTO reservations (description, reservation_date, start_date, end_date)
    VALUES (@description, @reservation_date, @start_date, @end_date);
END;

-- Executing the stored procedure
EXEC sp_insert_reservation 'Hotel reservation', '2023-02-05', '2023-06-26', '2023-07-01';
```

Stored procedures are advantageous for reusability, improved performance, better security, and abstraction.

### Miscellaneous

- `@@IDENTITY`: System function to get the last identity value generated for any table in the current session. Useful after an `INSERT` operation.

### Triggers in SQL Server

**Trigger Overview:** A trigger is a special type of stored procedure that automatically executes in response to certain events or actions occurring on a table. Triggers are attached to a specific table and defined to execute either before or after an event occurs.

**Types of Triggers:**

- **INSTEAD OF Trigger:**
    
    - Fires instead of the operation it is defined for (insert, delete, or update).
    - Executes before the operation is reflected in the table.

```sql
CREATE OR REPLACE TRIGGER example_trigger
INSTEAD OF INSERT OR UPDATE OR DELETE
ON example_table
FOR EACH ROW
BEGIN
  -- instead of trigger code or statement(s) here
END;
```

**AFTER Trigger:**

- Fires after the operation it is defined for has already been executed.
- Allows performing additional actions after the original action completes.

```sql
CREATE OR REPLACE TRIGGER example_trigger
AFTER INSERT OR UPDATE OR DELETE
ON example_table
FOR EACH ROW
BEGIN
  -- after trigger code or statement(s) here
END;
```

**Tips and Tricks for Triggers:**

- Keep triggers simple for quick and efficient execution.
- Use triggers for data validation to enforce data integrity rules.
- Be mindful of trigger firing order, especially when multiple triggers are defined for the same event and table.
- Consider performance implications, especially for triggers executed for every row affected by a triggering event.
- Test thoroughly before implementing triggers in a production environment.
- Document triggers, including their purpose, behavior, and interactions with other database objects.
- Use "INSTEAD OF" triggers with caution due to their power and potential complexity.

### Transactions in SQL Server

**Transaction Overview:** In SQL Server, a transaction is a sequence of one or more database operations treated as a single logical unit of work. Transactions ensure reliable and consistent changes to the database.

**ACID Properties:**

- **Atomicity:** Ensures that transactions are completed without interruption.
- **Consistency:** Guarantees the validity of data changes during a transaction.
- **Isolation:** Transactions are isolated from each other, preventing interference.
- **Durability:** Once committed, changes made by a transaction are permanent, even in case of system failure.

**Implicit Transactions:**

- Automatically started and committed by the database engine without explicit `BEGIN TRANSACTION` and `COMMIT TRANSACTION` statements.
- Each T-SQL statement is automatically wrapped in an implicit transaction.

**Explicit Transactions:**

- Explicitly started and committed or rolled back by the developer using `BEGIN TRANSACTION`, `COMMIT TRANSACTION`, and `ROLLBACK TRANSACTION` statements.
- Provides more control over the transaction, especially for complex operations.

**Example of Explicit Transaction:**

```sql
BEGIN TRAN
DECLARE @status INT = 0

DELETE FROM sensors WHERE sensor_id = 5
SET @status = @@ERROR

IF @status <> 0
    GOTO END_TRANSACTION

INSERT INTO sensors (name, host, port) VALUES ('Humidity', '192.168.1.12', 5000)
SET @status = @@ERROR

IF @status <> 0
    GOTO END_TRANSACTION

SELECT @@IDENTITY

COMMIT TRAN

END_TRANSACTION:
IF @status <> 0
    ROLLBACK TRAN
```

**View in SQL Server**

**View Overview:** A view in SQL Server is a virtual table based on an SQL query referring to other tables in the database. It does not store rows and columns on disk like a concrete table but contains the SQL query.

**Creating a View:**

```sql
-- Creating a view without parameters
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Modifying a View:**

```sql
-- Modifying a view
CREATE OR REPLACE VIEW view_name AS
SELECT modified_columns
FROM modified_table
WHERE modified_condition;
```

**Check Option in Views:**

```sql
-- Creating a view with check option
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition
WITH CHECK OPTION;
```

**Pros of Views:**

- Simplification of complex queries.
- Enhanced security by allowing access only through predefined views.
- Customization of data presentation for specific users or applications.
- Potential performance improvements.

**Cons of Views:**

- Maintenance difficulty with frequent changes to underlying tables.
- Additional overhead in terms of processing.
- Limitations on the types of operations and complexity of queries.
- Potential impact on performance if poorly designed or used inappropriately.

### Looping in T-SQL

#### WHILE Loop:

The `WHILE` loop in T-SQL is used to repeatedly execute a block of code as long as a specified condition is true.

**Syntax:**

```sql
WHILE condition
BEGIN
    -- T-SQL statements to be executed
END
```

**Example:**

```sql
DECLARE @counter INT
SET @counter = 1

WHILE @counter <= 10
BEGIN
    -- T-SQL statements to be executed
    SET @counter = @counter + 1
END
```
```sql
DECLARE @count INT;
SET @count = 1;

WHILE @count <= 10
BEGIN
   INSERT INTO Cars VALUES('Car-'+CAST(@count as varchar), @count*100)
   SET @count = @count + 1;
END;
```

### Exception Handling in T-SQL

Exception handling in T-SQL is implemented using the `TRY...CATCH` statement. The `TRY` block contains code that may cause an error, and the `CATCH` block contains code to handle errors gracefully.

**Syntax:**

```sql
BEGIN TRY  
    -- Statements that may cause an error  
END TRY  
BEGIN CATCH  
    -- Error handling statements  
END CATCH;
```
**Example:**

```sql
CREATE PROCEDURE spInsertCustomer  
(  
    @CustomerID int,  
    @CustomerName varchar(50),  
    @City varchar(50)  
)  
AS  
BEGIN  
    BEGIN TRY  
        -- Insert statement that may cause an error  
        INSERT INTO Customers (CustomerID, CustomerName, City)  
        VALUES (@CustomerID, @CustomerName, @City);  
    END TRY  
    BEGIN CATCH  
        -- Error handling statements  
        PRINT 'Error occurred: ' + ERROR_MESSAGE();  
    END CATCH;  
END;
```

#### sys.messages Table:

The `sys.messages` table is a system table in Microsoft SQL Server that stores information about system messages and error messages. It contains messages for different languages.

#### Error Handling Functions:

Several functions provide information about errors for use in error handling:

- `ERROR_PROCEDURE`: Returns the name of the stored procedure or trigger where the error occurred.
- `ERROR_NUMBER`: Returns the error number that was raised when the error occurred.
- `ERROR_MESSAGE`: Returns the error message text that describes the error.
- `ERROR_SEVERITY`: Returns the severity level of the error.
- `ERROR_LINE`: Returns the line number in the T-SQL code where the error occurred.

### Cursors in T-SQL

A cursor is used to iterate through a set of rows returned by a `SELECT` statement or perform operations on individual rows of data.

**Cursor Syntax:**
```sql
DECLARE cursor_name CURSOR FOR
SELECT column1, column2, ... FROM table_name WHERE condition;

OPEN cursor_name;

FETCH NEXT FROM cursor_name INTO variable1, variable2, ...;

WHILE @@FETCH_STATUS = 0
BEGIN
    -- Code to process the row data
    ...

    FETCH NEXT FROM cursor_name INTO variable1, variable2, ...;
END

CLOSE cursor_name;
DEALLOCATE cursor_name;
```
**Example:**
```sql
DECLARE crs_people CURSOR FOR SELECT citizen_id FROM people
OPEN crs_people

DECLARE @citizen_id CHAR(36)

FETCH NEXT FROM crs_people INTO @citizen_id

WHILE @@FETCH_STATUS = 0
BEGIN
    UPDATE people SET last_name = UPPER(last_name), address = UPPER(address) WHERE citizen_id = @citizen_id
    -- ...
    FETCH NEXT FROM crs_people INTO @citizen_id
END

CLOSE crs_people
DEALLOCATE crs_people
```

#### ABSOLUTE FETCH:

`ABSOLUTE FETCH` allows fetching a specific row from the result set based on its position.

**Example:**

```sql
DECLARE @bound INT = (SELECT COUNT(*) FROM people) + 1
DECLARE @min INT = 1
DECLARE @index INT = FLOOR(RAND() * (@bound - @min) + @min)

DECLARE crs_people CURSOR SCROLL FOR SELECT citizen_id FROM people
OPEN crs_people

DECLARE @citizen_id CHAR(36)

FETCH ABSOLUTE @index FROM crs_people INTO @citizen_id

IF @@FETCH_STATUS = 0
    SELECT * FROM people WHERE citizen_id = @citizen_id

CLOSE crs_people
DEALLOCATE crs_people
```

### Pros and Cons of Cursors

**Pros:**

1. **Flexibility:** Cursors provide flexibility in processing data, allowing custom row-by-row iteration.
2. **Control:** Cursors offer explicit control over row-by-row processing, beneficial for complex business logic.
3. **Persistence:** Cursors remain open until explicitly closed, suitable for long-running processes.

**Cons:**

1. **Performance:** Cursors can be slow and resource-intensive, especially with large result sets.
2. **Complexity:** Cursors are complex to implement and maintain, especially for inexperienced developers.
3. **Locking:** Cursors can cause locking and blocking issues if not used properly.

**When to Use Cursors:**

1. Data validation and cleansing.
2. Complex business logic.
3. Long-running processes.

### SQLCMD (SQL Command Line)

#### General Overview:

SQLCMD is a command-line utility that comes with Microsoft SQL Server, allowing you to interact with the SQL Server instance directly from the command prompt. It provides a way to execute T-SQL commands and scripts without the need for a visual editor or an integrated development environment (IDE).

- When executed, SQLCMD defaults to Windows Authentication for the connection.
- T-SQL commands entered directly into the command prompt are stored in memory until the `GO` command is used to execute them.
- The `GO` command is used to execute the last T-SQL statement entered. If the statement is incorrect, an appropriate error message is displayed.

#### Basic Usage:

- To run a T-SQL query directly from the command line:
```sql
sqlcmd -q "SELECT * FROM my_table"
```

* To get help in SQLCMD:
```sql
sqlcmd -?
```

* To run a script file:
```sql
sqlcmd -S <server_name> -i "script.sql"
```

* To specify a different output file:
```sql
sqlcmd -S <server_name> -i "script.sql" -o "result.txt"
```

- To run a stored procedure:
```sql
sqlcmd -S <server_name> -q "EXEC sp_databases"
```

* To connect using a specific login and password:
```sql
sqlcmd -S <server_name> -U <username> -P <password>
```

* To read and execute commands from a file during the SQLCMD session:
```sql
:r "script.sql"
```

#### Login Operation:

In MSSQL Server, logins are created to manage authorization. Each login does not have the authority to create another login. To create a login, the `CREATE LOGIN` statement is used:

```sql
CREATE LOGIN baris WITH PASSWORD='123456'
CREATE LOGIN cankut WITH PASSWORD='12345', DEFAULT_DATABASE=tennisclubappdb
```

To change the password of a login:

```sql
ALTER LOGIN cankut WITH PASSWORD='123'
```

#### Server Roles:

In MSSQL Server, various server roles define different sets of permissions. Some common server roles include:

- `bulkadmin`: Permission to run the BULK INSERT statement.
- `dbcreator`: Permission to create, alter, drop, and restore databases.
- `diskadmin`: Permission to manage SQL Server files on disk.
- `processadmin`: Permission to end processes running inside the SQL Server instance.
- `public`: Default role for all logins.
- `securityadmin`: Permission to manage logins and their properties.
- `serveradmin`: Permission to configure server-wide settings and shut down the server.
- `setupadmin`: Permission to add or remove linked servers.
- `sysadmin`: Permission to perform all administrative tasks on the server.

Use the `sp_helpsrvrolemember` stored procedure to view members of a server role:

```sql
EXEC sp_helpsrvrolemember 'setupadmin'
```

To assign a login to a server role, use the `ALTER SERVER ROLE` statement:

```sql
ALTER SERVER ROLE securityadmin ADD MEMBER cankut
ALTER SERVER ROLE dbcreator ADD MEMBER baris
```

#### Permissions on Tables:

- Granting and revoking permissions on tables is done using the `GRANT` and `REVOKE` statements.
    
- Granting select permission on the `courts` table to the `cankut` user:

```sql
GRANT SELECT ON courts TO cankut
```

Granting insert and delete permissions on the `courts` table to the `cankut` user:

```sql
GRANT DELETE, INSERT ON courts TO cankut
```

Revoking delete permission on the `courts` table from the `cankut` user:

```sql
REVOKE DELETE ON courts FROM cankut
```

Revoking select permission on the `courts` table from the `public` role:
```sql
REVOKE SELECT ON courts FROM public
```

### SQL Index

An index is a database feature that is generally defined on tables, allowing for faster access to relevant data by reducing the number of operations needed. The primary purpose of an index is to provide fast data retrieval. Primary key and foreign key columns are indexed by default.

#### Index Details:

- When a new database is created, associated files are created, and SQL Server divides these files into logical 8KB pages. Each page is assigned an index number starting from zero, and these pages consist of rows.
    
- Rows' lengths and counts within pages can vary based on data size. Rows are accessed at the page level, and for tables with indexes, the data is organized as a tree data structure.
    

#### Types of Indexes:

In SQL Server, indexes are primarily categorized into two groups: clustered and non-clustered indexes.

##### Clustered Index:

- Organizes data physically.
- Columns used for a clustered index should be the most frequently used in queries to benefit from fast access.
- It is recommended that indexed columns are ones that change as little as possible, as modifying an indexed column will require reordering the entire index.

```sql
CREATE CLUSTERED INDEX idx_sensor_host_port ON sensors(host, port)
```

##### Non-clustered Index:

- Organizes data logically.
- Logical ordering is done with addresses (1 table -> max 999 entries).
- Non-clustered indexes do not directly provide access to data; instead, they are accessed via a heap or a clustered index at a lower level.
- It is recommended to index fields that are frequently used in the `WHERE` clause.

```sql
CREATE NONCLUSTERED INDEX idx_sensor_host_port ON sensors(host, port)
```

##### Unique Index:

- Prevents duplicate values and speeds up data access.
- A unique index is automatically created for the primary key in a table.
- If indexed columns are nullable, only one null value is allowed.

```sql
CREATE UNIQUE INDEX idx_enrolls_student_id_lecture_id ON enrolls(student_id, lecture_id)
```

##### Filtered Index:

- Defined for data that meets a specific condition, improving performance and making index maintenance faster for a specific group of data.

```sql
CREATE NONCLUSTERED INDEX idx_sensor_host_port ON sensors(host, port) WHERE port > 1024
```

##### Composite Index:

- Defined for multiple columns in a table. The order of columns is crucial, with diverse columns placed first.

```sql
CREATE NONCLUSTERED INDEX idx_sensor_host_port ON sensors(host, port)
```

##### Covered Index:

- Used when all the columns needed for a query are in the index itself, reducing the need for additional key lookup operations.

```sql
CREATE NONCLUSTERED INDEX idx_sensor_host_port ON sensors(host, port) INCLUDE(name, latitude, longitude)
```

##### Full-text Index:

- Used for text-based searches, improving performance compared to `LIKE` operations on large text fields.

##### Column Store Index:

- Organized column-wise rather than row-wise, making it suitable for scenarios with infrequent insert, delete, and update operations but heavy read, filter, and group operations.

```sql
CREATE COLUMNSTORE INDEX idx_sensor_host_port ON sensors(host, port)
```

#### Possible Disadvantages of Indexing:

- Each index consumes additional space in the database, potentially leading to insufficient disk space.
- Creating or rebuilding an index locks the respective table, preventing other operations.
- Index maintenance for insert, delete, and update operations can negatively impact performance.
- The time required for creating or rebuilding an index depends on the data size and count.

#### Considerations for Indexing:

- Tables with frequent insert, delete, and update operations benefit from fewer indexes.
- The performance of an index is negatively affected by the number of repeated values in the indexed column.
- Clustered indexes should be used for as few columns as possible, ideally unique and non-nullable fields.
- Pay attention to the order of columns in composite indexes.
- Calculated fields can be indexed if necessary.
- Carefully select indexed fields.
- The number of fields in indexing directly affects the performance of insert, delete, and update operations.

### WINDOW FUNCTION:

Window functions in SQL are used to perform calculations across a specified range of rows related to the current row within a result set. Here are the key concepts associated with window functions:

- **Partition By:**
    
    - Partitions the result set into smaller sets or partitions based on the values in one or more columns.
    - The window function is applied independently within each partition.
    - Syntax: `OVER (PARTITION BY column1, column2, ...)`
- **Order By:**
    
    - Defines the order of rows within each partition.
    - It is used to determine the sequence in which the window function processes the rows.
    - Syntax: `OVER (ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...)`
- **Row or Range:**
    
    - Specifies the range of rows used by the window function.
    - `ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING` can be an example, specifying a range of the current row and its adjacent rows.

### Example - Database Creation and Queries:

```sql
-- Database creation
CREATE DATABASE shoppingdb;
USE shoppingdb;

-- Customers table creation
CREATE TABLE customers (
    customer_id bigint PRIMARY KEY IDENTITY(1, 1),
    name nvarchar(256) NOT NULL,
    address nvarchar(MAX) NOT NULL
);

-- Orders table creation
CREATE TABLE orders (
    order_id int PRIMARY KEY IDENTITY(1, 1),
    customer_id bigint FOREIGN KEY REFERENCES customers(customer_id) NOT NULL,
    date DATE,
    quantity INT,
    unit_price MONEY
);

-- Window function queries
-- #1
SELECT
    c.name,
    c.address,
    SUM(o.quantity * o.unit_price) OVER (PARTITION BY c.address) AS total,
    MAX(o.quantity * o.unit_price) OVER (PARTITION BY c.address) AS max
FROM customers c
INNER JOIN orders o ON c.customer_id = o.customer_id;

-- #2
SELECT
    c.name,
    SUM(o.quantity * o.unit_price) AS total,
    MAX(o.quantity * o.unit_price) AS max
FROM customers c
INNER JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.name;

-- #3
SELECT
    c.name,
    c.address,
    o.quantity * o.unit_price AS total,
    ROW_NUMBER() OVER (PARTITION BY c.address ORDER BY o.quantity * o.unit_price DESC) AS row_num
FROM customers c
INNER JOIN orders o ON c.customer_id = o.customer_id;
```

### BACKUP:

SQL Server provides various backup methods. Some common types include:

- **Full Backup:**
```sql
BACKUP DATABASE dbprogs21_schooldb TO DISK='C:\db\dbprogs21_schooldb.bak' WITH FORMAT;
```

**Differential Backup:**
```sql
BACKUP DATABASE dbprogs21_schooldb TO DISK='C:\db\dbprogs21_schooldb.bak' WITH DIFFERENTIAL;
```

**Transaction Log Backup:**
```sql
BACKUP LOG dbprogs21_schooldb TO DISK='C:\db\dbprogs21_schooldb.bak' WITH FORMAT;
```

**Tail Log Backup:**
```sql
BACKUP LOG dbprogs21_schooldb TO DISK='C:\db\dbprogs21_schooldb.bak' WITH CONTINUE_AFTER_ERROR;
```

Other types include Copy-only, File, and Partial backups.

### SQL SERVER JOB:

SQL Server jobs are tools provided by the SQL Server Agent service to perform various tasks at scheduled intervals. To create a job:

1. Open SQL Server Management Studio and navigate to SQL Server Agent.
2. Right-click on Jobs and select "New Job."
3. Define the job details, steps, and schedule.

Example Steps:

- Define a step to execute a SQL script or command.
- Set the action to be taken on success or failure.
- Configure advanced settings like retry attempts and logging.

Schedules determine when jobs run, and you can create recurring or one-time schedules.

### LINKED SERVER:

Linked Servers (LS) are used to establish connections between SQL Server instances or different database systems. Key steps:

1. In SQL Server Management Studio, navigate to "Server Objects" > "Linked Servers."
2. Define the linked server, specifying the server type and connection details.
3. Use the linked server in queries, e.g.:
```sql
SELECT * FROM [LinkedServerName].DatabaseName.SchemaName.TableName;
```
4. Ensure proper user permissions on the linked server.



# ORACLE

#### 1. Hello World Program:

```sql
DECLARE
BEGIN
    DBMS_OUTPUT.PUT_LINE('Merhaba Dünya');
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;
```

#### 2. Anonymous Block Example:

```sql
DECLARE
    n_val NUMBER;
    s_msg VARCHAR(100);
BEGIN
    n_val := 10;
    s_msg := 'n_val = ' || n_val;
    DBMS_OUTPUT.PUT_LINE(s_msg);
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;
```

#### 3. Usage of Data Types:

```sql
DECLARE
    n_val NUMBER;
    c_citizenId CHAR(11);
    c_name NVARCHAR2(50);
    c_familyName NVARCHAR2(50);
    c_fullName NVARCHAR2(100);
BEGIN
    n_val := 10;
    DBMS_OUTPUT.PUT_LINE('n_val = ' || n_val);
    c_citizenId := '12345678911';
    DBMS_OUTPUT.PUT_LINE('c_citizenId = ' || c_citizenId);
    c_name := 'Oğuz';
    c_familyName := 'Karan';
    c_fullName := c_name || ' ' || c_familyName;
    DBMS_OUTPUT.PUT_LINE('Name = ' || c_fullName);
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;
```

#### 4. Creating a Simple schooldb Database and Queries:

```sql
CREATE DATABASE schoolappdb;

CREATE TABLE students (
    student_id NUMBER(10) GENERATED AS IDENTITY PRIMARY KEY,
    citizen_number CHAR(11) UNIQUE NOT NULL,
    first_name NVARCHAR2(100) NOT NULL,
    middle_name NVARCHAR2(100),
    last_name NVARCHAR2(100) NOT NULL,
    address LONG NOT NULL
);

CREATE TABLE lectures (
    lecture_code CHAR(7) PRIMARY KEY,
    name NVARCHAR2(50) NOT NULL,
    credits NUMBER(10) NOT NULL,
    ects_credits NUMBER(10)
);

CREATE TABLE enrolls (
    enroll_id NUMBER(10) GENERATED AS IDENTITY PRIMARY KEY,
    student_id NUMBER(10) REFERENCES students(student_id) NOT NULL,
    lecture_code CHAR(7) REFERENCES lectures(lecture_code) NOT NULL,
    grade NUMBER(10)
);

-- Inserts and Selects are provided in the original code

-- Aggregate Functions:
SELECT COUNT(*) FROM students;
SELECT COUNT(*), first_name FROM students GROUP BY first_name;
SELECT COUNT(*), first_name FROM students WHERE student_id > 8 GROUP BY first_name HAVING COUNT(*) > 1;

-- Sum and Avg Functions:
SELECT AVG(grade) FROM enrolls WHERE lecture_code = 'BIM 101';
SELECT AVG(grade) FROM enrolls WHERE student_id = 7;
SELECT AVG(lec.credits * e.grade) AS average, AVG(lec.ects_credits * e.grade) AS ects_average
FROM enrolls e INNER JOIN lectures lec ON lec.lecture_code = e.lecture_code
WHERE e.student_id = 7;

-- Select-In Usage:
SELECT * FROM students WHERE first_name IN ('Ali', 'Oğuz');
SELECT * FROM students s WHERE s.student_id IN (SELECT e.student_id FROM enrolls e WHERE e.grade > 70);

-- Union, Intersect, and Minus Operations:
SELECT first_name FROM students
UNION
SELECT name FROM lectures;

SELECT first_name AS nam FROM students
INTERSECT
SELECT name FROM lectures;

SELECT first_name AS nam FROM students
MINUS
SELECT name FROM lectures;
```

### String Functions, Operators, and Conditional Statements:

#### 1. Important Operators:

```sql
=               -- Equality comparison
<>              -- Inequality comparison
!=              -- Inequality comparison
>, <, >=, <=    -- Greater than, less than, greater than or equal, less than or equal
IN()            -- In comparison
NOT             -- Not comparison
BETWEEN         -- Between comparison
IS NULL         -- Null comparison
IS NOT NULL     -- Not null comparison
LIKE            -- Pattern matching
EXISTS          -- Existence comparison
```

#### 2. BETWEEN Operator:
```sql
SELECT s.first_name FROM 
enrolls e INNER JOIN students s ON s.student_id = e.student_id
WHERE e.grade BETWEEN 50 AND 70;

```

#### 3. String Functions and Operators:

```sql
DECLARE
    n_val NUMBER;
BEGIN
    n_val := 10;
    DBMS_OUTPUT.PUT_LINE(CHR(65 + 32));
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
BEGIN    
    DBMS_OUTPUT.PUT_LINE(ASCII('ğ'));
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
BEGIN    
    DBMS_OUTPUT.PUT_LINE('Length = ' || LENGTH('ankara'));
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

-- Update statement using string functions:
UPDATE students SET first_name = UPPER(first_name) WHERE student_id > 1;

-- CONCAT function and || operator:
SELECT CONCAT(CONCAT(first_name, ' '), surname) AS "Full name" FROM students; 

DECLARE
BEGIN        
    DBMS_OUTPUT.PUT_LINE(CONCAT(CONCAT('Oğuz', ' '), 'Karan')); 
    DBMS_OUTPUT.PUT_LINE('Oğuz' || ' ' || 'Karan');  
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
BEGIN        
    DBMS_OUTPUT.PUT_LINE(LPAD('A', 4, 'x'));
    DBMS_OUTPUT.PUT_LINE(RPAD('A', 4, 'x'));  
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
    v_name VARCHAR2(50) := 'Yiğithan';
    v_surname VARCHAR2(50) := 'Uluğ';
BEGIN        
    DBMS_OUTPUT.PUT_LINE(RPAD(SUBSTR(v_name, 1, 1), LENGTH(v_name), 'X') || ' ' || RPAD(SUBSTR(v_surname, 1, 1), LENGTH(v_surname), 'X'));     
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
    v_name VARCHAR2(50) := '                  Yiğithan          ';
    v_surname VARCHAR2(50) := '                Uluğ             ';
BEGIN        
    v_name := TRIM(v_name);
    v_surname := TRIM(v_surname);
    DBMS_OUTPUT.PUT_LINE(RPAD(SUBSTR(v_name, 1, 1), LENGTH(v_name), 'X') || ' ' || RPAD(SUBSTR(v_surname, 1, 1), LENGTH(v_surname), 'X'));     
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
    v_text VARCHAR2(150) := 'Bugün hava çok güzel. Bu çok güzel havada ders mi yapılır';    
BEGIN
    DBMS_OUTPUT.PUT_LINE(REPLACE(v_text, 'güzel', 'kötü'));     
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
    v_text VARCHAR2(150) := 'Bugün hava çok güzel. Bu çok güzel havada ders mi yapılır';    
BEGIN    
    DBMS_OUTPUT.PUT_LINE(INSTR(v_text, 'çok'));
    DBMS_OUTPUT.PUT_LINE(INSTR(v_text, 'çok', 13));  
    DBMS_OUTPUT.PUT_LINE(INSTR(v_text, 'çok', 13, 5));  
EXCEPTION
    WHEN OTHERS THEN 
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;
```

#### 4. IF Statements:

```sql
DECLARE
    n_val NUMBER := 20;
BEGIN
    IF n_val > 0 THEN
        DBMS_OUTPUT.PUT_LINE('Positive');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Not Positive');
    END IF;
EXCEPTION
    WHEN OTHERS THEN
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
    n_val NUMBER := 0;
BEGIN
    IF n_val > 0 THEN
        DBMS_OUTPUT.PUT_LINE('Positive');
    ELSIF n_val = 0 THEN
        DBMS_OUTPUT.PUT_LINE('Zero');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Negative');
    END IF;
EXCEPTION
    WHEN OTHERS THEN
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
    v_grade VARCHAR2(1) := 'F';
BEGIN
    IF v_grade = 'A' THEN
        DBMS_OUTPUT.PUT_LINE('Excellent');
    ELSIF v_grade = 'B' THEN
        DBMS_OUTPUT.PUT_LINE('Good');
    ELSIF v_grade = 'C' THEN
        DBMS_OUTPUT.PUT_LINE('Average');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Poor');
    END IF;
EXCEPTION
    WHEN OTHERS THEN
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
    c_grade CHAR(1) := 'A';
BEGIN
    CASE c_grade
        WHEN 'A' THEN
            DBMS_OUTPUT.PUT_LINE('Excellent');
        WHEN 'B' THEN
            DBMS_OUTPUT.PUT_LINE('Good');
        WHEN 'C' THEN
            DBMS_OUTPUT.PUT_LINE('Average');
        ELSE
            DBMS_OUTPUT.PUT_LINE('Poor');
    END CASE;
EXCEPTION
    WHEN OTHERS THEN
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
    c_grade CHAR(1) := 'A';
BEGIN
    CASE
        WHEN c_grade = 'A' THEN
            DBMS_OUTPUT.PUT_LINE('Excellent');
        WHEN c_grade = 'B' THEN
            DBMS_OUTPUT.PUT_LINE('Good');
        WHEN c_grade = 'C' THEN
            DBMS_OUTPUT.PUT_LINE('Average');
        ELSE
            DBMS_OUTPUT.PUT_LINE('Poor');
    END CASE;
EXCEPTION
    WHEN OTHERS THEN
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;

DECLARE
    n_val NUMBER := 0;
BEGIN
    CASE
        WHEN n_val > 0 THEN
            DBMS_OUTPUT.PUT_LINE('Positive');
        WHEN n_val = 0 THEN
            DBMS_OUTPUT.PUT_LINE('Zero');
        ELSE
            DBMS_OUTPUT.PUT_LINE('Negative');
    END CASE;
EXCEPTION
    WHEN OTHERS THEN
        RAISE_APPLICATION_ERROR(-20000, 'Exception occurred');
END;
```

# XML

```sql
-- Create database and table
```sql
CREATE DATABASE librarydb;

USE librarydb;

CREATE TABLE books (
    book_id INT PRIMARY KEY IDENTITY(1, 1),
    name NVARCHAR(250) NOT NULL,
    ISBN NVARCHAR(30),
    chapter_summary XML NOT NULL
);
```

```sql
-- Insert data into the books table
```sql
DECLARE @chapter_summary XML;

SET @chapter_summary = '
    <book id="1" name="Cin Ali Lunaparkta">
        <chapters>
            <chapter id="1" name="Hazırlanma"/>
            <chapter id="2" name="Evden çıkış"/>
            <chapter id="3" name="Lunaparka varış"/>
        </chapters>
    </book>';

INSERT INTO books (name, ISBN, chapter_summary)
VALUES ('Cin Ali Lunaparkta', '1234', @chapter_summary);
```

```sql
-- Select data from the books table
SELECT chapter_summary FROM books;
```

```sql
-- Use XML exist function to query hierarchical information
```sql
SELECT name
FROM books
WHERE chapter_summary.exist('/book/chapters/chapter[@id=1]') = 1 AND book_id = 1;

SELECT name
FROM books
WHERE chapter_summary.exist('/book/chapters/chapter[@name="Hazırlanma"]') = 1;
```

```sql
-- Create a stored procedure to get chapter summary info by book id
```sql
CREATE PROCEDURE sp_get_chapter_summary_info_by_book_id(@book_id INTEGER)
AS
BEGIN
    DECLARE @chapter_summary XML;

    SELECT @chapter_summary = chapter_summary
    FROM books
    WHERE book_id = 1;

    -- Retrieve id and name of chapters from the XML data of a book
    SELECT
        BookID.value('@id', 'INTEGER'),
        BookID.value('@name', 'NVARCHAR(100)')
    FROM @chapter_summary.nodes('/book/chapters/chapter') AS BookTable(BookID);
END;

EXEC sp_get_chapter_summary_info_by_book_id 1;
```


```sql
-- Use XQuery query function to query XML data
```sql
DECLARE @chapter_summary XML;

SELECT @chapter_summary = chapter_summary
FROM books
WHERE book_id = 1;

-- Retrieve chapters and book information
SELECT @chapter_summary.query('/book/chapters/chapter');
SELECT @chapter_summary.query('/book');
SELECT @chapter_summary.query('/book/chapters');
```

```sql
-- Use XQuery modify function to update XML data

UPDATE books
SET chapter_summary.modify('insert <chapter id="4" name="Eve dönüş"/> into (/book/chapters)[1]')
WHERE book_id = 1;

SELECT chapter_summary
FROM books
WHERE book_id = 1;
```

```sql
-- Query data from a table and convert it to XML format
DECLARE @students XML;

SET @students = (SELECT * FROM students FOR XML AUTO);

SELECT  @students;
```

The XML data from the `students` table is transformed into the following XML format:

```sql
<students>
    <student student_id="1" name="Oguz" address="Göktürk" />
    <student student_id="2" name="Kaan" address="Atasehir" />
    <student student_id="3" name="Ali" address="Basaksehir" />
</students>
```


# JSON

```sql
-- Check if a text is in JSON format using the isjson function
```sql
DECLARE @data NVARCHAR(MAX);

SET @data = '
    {
        "book": {
            "id": 1,
            "name": "Cin Ali Lunaparkta",
            "totalPage": 100,
            "chapters": [
                {"id": 1, "name": "Hazırlanma"},
                {"id": 2, "name": "Evden çıkış"},
                {"id": 3, "name": "Lunaparka varış"}
            ]
        }
    }';

SELECT ISJSON(@data);
```

```sql
-- Create a table and a procedure for inserting JSON data
CREATE TABLE books (
    book_id INT PRIMARY KEY IDENTITY(1, 1),
    name NVARCHAR(250) NOT NULL,
    ISBN NVARCHAR(30),
    chapter_summary NVARCHAR(MAX) NOT NULL
);

CREATE PROCEDURE sp_insert_book(@name NVARCHAR(250), @isbn NVARCHAR(30), @chapter_summary NVARCHAR(MAX))
AS
BEGIN
    IF ISJSON(@chapter_summary) = 0
        THROW 60000, 'Not a json format', 1;

    INSERT INTO books (name, isbn, chapter_summary) VALUES (@name, @isbn, @chapter_summary);
END;

EXEC sp_insert_book 'Cin Ali Lunaparkta', '12345', '{
    "book": {
        "id": 1,
        "name": "Cin Ali Lunaparkta",
        "totalPage": 100,
        "chapters": [
            {"id": 1, "name": "Hazırlanma"},
            {"id": 2, "name": "Evden çıkış"},
            {"id": 3, "name": "Lunaparka varış"}
        ]
    }
}';
```

```sql
-- Retrieve values from JSON data using json_value
```sql
SELECT JSON_VALUE(chapter_summary, '$.book.totalPage') FROM books;

SELECT JSON_VALUE(chapter_summary, '$.book.chapters[0].name') FROM books;

SELECT JSON_VALUE(chapter_summary, '$.book.chapters[1].name') FROM books;
```

```sql
-- Modify JSON data using json_modify function
```sql
SELECT chapter_summary FROM books;

UPDATE books
SET chapter_summary = JSON_MODIFY(chapter_summary, '$.book.chapters[2].name', 'Varış')
WHERE book_id = 1;

UPDATE books
SET chapter_summary = JSON_MODIFY(chapter_summary, '$.book.chapters[0].sectionCount', 2)
WHERE book_id = 1;

UPDATE books
SET chapter_summary = JSON_MODIFY(chapter_summary, 'append $.book.chapters', JSON_QUERY('{"id": 3, "name": "Eve dönüş"}', '$'))
WHERE book_id = 1;

UPDATE books
SET chapter_summary = JSON_MODIFY(chapter_summary, '$.book.chapters[4].id', 4)
WHERE book_id = 1;

UPDATE books
SET chapter_summary = JSON_MODIFY(chapter_summary, '$.book.chapters[4]', NULL)
WHERE book_id = 1;

UPDATE books
SET chapter_summary = JSON_MODIFY(chapter_summary, '$.book.chapters[3]', JSON_QUERY('{"id": 4, "name": "Eve dönüş"}', '$'))
WHERE book_id = 1;

UPDATE books
SET chapter_summary = JSON_MODIFY(chapter_summary, '$.book.chapters[0].sectionCount', NULL)
WHERE book_id = 1;

UPDATE books
SET chapter_summary = JSON_MODIFY(
    JSON_MODIFY(chapter_summary, '$.book.chapters[3].title_name', JSON_VALUE(chapter_summary, '$.book.chapters[3].name')),
    '$.book.chapters[3].name', NULL
);
```

```sql
-- Get JSON format from a query result using "for json auto"
```sql
SELECT
    id,
    name,
    host,
    port,
    register_datetime,
    (
        SELECT
            port_id,
            sensor_id,
            value,
            measure_datetime
        FROM sensor_data
        WHERE s.id = sensor_data.sensor_id
        FOR JSON AUTO
    ) AS sensor_data
FROM sensors s
WHERE id = 236
FOR JSON AUTO;
```

```sql
-- Extract tabular data from JSON using openjson function
```sql
SELECT *
FROM OPENJSON('[
    {
        "id": 236,
        "name": "Ramphastos tucanus",
        "host": "209.254.156.157",
        "port": 47243,
        "register_datetime": "2023-05-07T23:04:57.203",
        "port_id": 1,
        "sensor_id": 236,
        "value": -8.8639999e+001,
        "measure_datetime": "2022-09-01T00:00:00"
    },
    {
        "id": 236,
        "name": "Ramphastos tucanus",
        "host": "209.254.156.157",
        "port": 47243,
        "register_datetime": "2023-05-07T23:04:57.203",
        "port_id": 259,
        "sensor_id": 236,
        "value": 7.4899998e+000,
        "measure_datetime": "2023-02-18T00:00:00"
    }
]') WITH (
    id INT,
    name NVARCHAR(100),
    host NVARCHAR(100),
    port INT,
    register_datetime DATETIME,
    port_id INT,
    sensor_id INT,
    value REAL,
    measure_datetime DATETIME
);
```




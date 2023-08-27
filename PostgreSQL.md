> # DATABASE

# To see the list of database:

```
\l
```

# To create a database:

```
CREATE DATABASE database_name;
```

# To see the list of table names:

```
\d or \dt
```

# To create a Table:

```
CREATE TABLE cars (
brand VARCHAR(255),
model VARCHAR(255),
year INT
);
```

# To Display the complete table:

```
SELECT \* FROM cars;
```

# To Insert values into the table:

```
INSERT INTO cars (brand, model, year)
VALUES
     ('Volvo', 'p1800', 1968),
     ('BMW', 'M1', 1978),
     ('Toyota', 'Celica', 1975);
```

# To show the particular columns of a table:

```
SELECT brand, year FROM cars;
```

_Note:_ ALTER TABLE is used to add, delete, or modify columns in an existing table & also used to add and drop various constraints on an existing table.

# To add new column to the table:

```
ALTER TABLE cars
ADD color VARCHAR(255);

```

# To update or modify a column value in the table:

```
UPDATE cars
SET color = 'red'
WHERE brand = 'Volvo';
```

_Note:_ Without WHERE clause, all records will be updated.

# To update multiple columns:

```
UPDATE cars
SET color = 'white', year = 1970
WHERE brand = 'Toyota';
```

# To change the datatype of a column:

```
ALTER TABLE cars
ALTER COLUMN year TYPE VARCHAR(4);
```

# To DROP a column:

```
ALTER TABLE cars
DROP COLUMN color;
```

# To DELETE a row:

```
DELETE FROM cars
WHERE brand = 'Volvo';
```

# To DELETE complete TABLE data:

```
DELETE FROM cars;
```

OR

```
TRUNCATE TABLE cars;
```

# To DROP a table:

```
DROP TABLE cars;
```

> # SYNTAX

## SELECT DISTINCT

```
SELECT DISTINCT country FROM customers;
```

## SELECT COUNT(DISTINCT)

```
SELECT COUNT(DISTINCT country) FROM customers;
```

## Sort Data

- In Ascending Order:

```
SELECT * FROM products
ORDER BY price;
```

- In Descending Order:

```
SELECT * FROM products
ORDER BY price DESC;
```

## The LIMIT clause:

It is used to limit the maximum number of records to return.

```
SELECT * FROM customers
LIMIT 20;
```

## THe OFFSET clause:

It is used to specify where to start selecting the records to return.

```
SELECT * FROM customers
LIMIT 20 OFFSET 40;
```

It will show maximum of 20 records starting from 41th record.

## MIN

```
SELECT MIN(price)
FROM products;
```

## MAX

```
SELECT MAX(price)
FROM products;
```

In MAX and MIN, the column name will be shown as min or max respectively.

## Set Column Name

```
SELECT MIN(price) AS lowest_price
FROM products;
```

Here, the column name will be shown as lowest_price in place of min.

## COUNT

```
SELECT COUNT(customer_id)
FROM customers;
```

It will return the total number of customer*id present in the table.\
Note:* NULL values are not counted.

## SUM

```
SELECT SUM(quantity)
FROM order_details;
```

## AVG

```
SELECT AVG(price)
FROM products;
```

_Note:_ NULL values are ignored and the decimal places will be large.

- With 2 Decimals

```
SELECT AVG(price)::NUMERIC(10,2)
FROM products;
```

It will return the average with 2 decimal place.

## LIKE

It is used used with WHERE clause to search for specific pattern in a column.

- % -> It represents zero, one or multiple characters.
- \ -> It represents one single chaaracter.

* ### Starts with

```
SELECT * FROM customers
WHERE customer_name LIKE 'A%';
```

It will show all the customer name starts with A.

- ### Contains

```
SELECT * FROM customers
WHERE customer_name LIKE '%A%';
```

It will show all the customer name which contains A.

- ### ILIKE
  ILIKE is case insensitive.

```
SELECT * FROM customers
WHERE customer_name ILIKE '%A%';
```

It will show all the customer name which contains A or a.

- ### Ends with

```
SELECT * FROM customers
WHERE customer_name LIKE '%en';
```

It will show all the names ends with en.

- ### \_ wildcard
  It can be any character or number, but each \_ represents one and only one character.

```
SELECT * FROM customers
WHERE city LIKE 'L_nd__';
```

Here the length of all the shown city will be same and in place of \_ there will be any character or numnber.

## IN

It is a shorthand for multiple OR condition and is used with WHERE clause.

```
SELECT * FROM customers
WHERE country IN ('Germany', 'France', 'UK');
```

It will show all the customers whose country is in given range.

## NOT IN(SELECT)

```
SELECT * FROM customers
WHERE customer_id NOT IN (SELECT customer_id FROM orders);
```

It will display all the customers whose id is not present in Orders table.

## BETWEEN

```
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 15;
```

```
SELECT * FROM Products
WHERE product_name BETWEEN 'Pavlova' AND 'Tofu';
```

It will display all the name between them alphabetically.

## Aliases

It's used to give a table or a column in a table, a temporary name.

```
SELECT customer_id AS id
FROM customers;
```

We can also skip AS.

```
SELECT customer_id id
FROM customers;
```

### Concatenate Columns

The AS keyword is often used when two or more fields are concatenated into one.

```
SELECT product_name || unit AS product
FROM products;
```

To give space between Product Name and Unit,

```
SELECT product_name || ' ' || unit AS product
FROM products;
```

## Using Aliases With a Space Character

```
SELECT product_name AS "My Great Products"
FROM products;
```

## JOIN

A JOIN clause is used to combine rows from two or more tables, based on a related column between them.

```
SELECT product_id, product_name, category_name
FROM products
INNER JOIN categories ON products.category_id = categories.category_id;
```

Suppose there are two tables, products and categories. Now the above command will command will combine the above two tables into one with respect to their related elements.

- INNER JOIN: Returns records that have matching values in both tables
- LEFT JOIN: Returns all records from the left table, and the matched records from the right table
- RIGHT JOIN: Returns all records from the right table, and the matched records from the left table
- FULL JOIN: Returns all records when there is a match in either left or right table

## CROSS JOIN

The CROSS JOIN keyword matches ALL records from the "left" table with each record from the right table.

```
SELECT testproduct_id, product_name, category_name
FROM testproducts
CROSS JOIN categories;
```

Its like taking the cross product of both the table.

## UNION

```
SELECT product_id, product_name
FROM products
UNION
SELECT testproducts_id, product_name
FROM testproducts
ORDER BY product_id;
```

It will take the union of both and display by sorting them.
Duplicates are taken once only.

## UNION ALL

It will return the duplicates also.

## GROUP BY

The GROUP BY clause groups rows that have the same values into summary rows, like "find the number of customers in each country".

```
SELECT COUNT(customer_id), country
FROM customers
GROUP BY country;
```

It will group all the same country into one and also return the count of customers in particular grouped country.

## HAVING

The HAVING clause was added to SQL because the WHERE clause cannot be used with aggregate functions.

```
SELECT COUNT(customer_id), country
FROM customers
GROUP BY country
HAVING COUNT(customer_id) > 5;
```

## EXISTS

The EXISTS operator is used to test for the existence of any record in a sub query.
The EXISTS operator returns TRUE if the sub query returns one or more records.

```
SELECT customers.customer_name
FROM customers
WHERE EXISTS (
  SELECT order_id
  FROM orders
  WHERE customer_id = customers.customer_id
);
```

## NOT EXISTS

```
SELECT customers.customer_name
FROM customers
WHERE NOT EXISTS (
  SELECT order_id
  FROM orders
  WHERE customer_id = customers.customer_id
);
```

## ANY

ANY means that the condition will be true if the operation is true for any of the values in the range.

```
SELECT product_name
FROM products
WHERE product_id = ANY (
  SELECT product_id
  FROM order_details
  WHERE quantity > 120
);
```

## ALL

ALL means that the condition will be true only if the operation is true for all values in the range.

```
SELECT product_name
FROM products
WHERE product_id = ALL (
  SELECT product_id
  FROM order_details
  WHERE quantity > 10
);
```

## CASE

The CASE expression goes through conditions and returns a value when the first condition is met (like an if-then-else statement).

Once a condition is true, it will stop reading and return the result. If no conditions are true, it returns the value in the ELSE clause.

If there is no ELSE part and no conditions are true, it returns NULL.

```
SELECT product_name,
CASE
  WHEN price < 10 THEN 'Low price product'
  WHEN price > 50 THEN 'High price product'
ELSE
  'Normal product'
END
FROM products;
```

## CASE with an Alias

When a column name is not specified for the "case" field, the parser uses case as the column name.

To specify a column name, add an alias after the END keyword.

```
SELECT product_name,
CASE
  WHEN price < 10 THEN 'Low price product'
  WHEN price > 50 THEN 'High price product'
ELSE
  'Normal product'
END AS "price category"
FROM products;
```

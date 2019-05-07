# java-sql

A student that completes this project shows that they can:

- Query data from a single table
- Query data from multiple tables
- Create a new datadaase using PostgreSQL

# Introduction

Working with SQL

# Instructions

Surf to [SQL Try Editor at W3Schools.com](https://www.w3schools.com/Sql/tryit.asp?filename=trysql_select_top)  
Answer the following data queries. Keep track of the SQL you write by pasting it into this document under its appropriate header below. You will be submitting that through the regular fork, change, pull process.

### **Clicking the `Restore Database` button in the page will repopulate the database with the original data and discard all changes you have made**.

### find all customers that live in London. Returns 6 records.

> This can be done with SELECT and WHERE clauses
> SELECT \*
> FROM Customers
> WHERE city = 'London'
> ORDER BY city

### find all customers with postal code 1010. Returns 3 customers.

> This can be done with SELECT and WHERE clauses
> SELECT \*
> FROM Customers
> WHERE PostalCode = '1010'
> ORDER BY ContactName

### find the phone number for the supplier with the id 11. Should be (010) 9984510.

> This can be done with SELECT and WHERE clauses
> SELECT phone
> FROM Suppliers
> WHERE SupplierId = '11'

### list orders descending by the order date. The order with date 1997-02-12 should be at the top.

> This can be done with SELECT, WHERE, and ORDER BY clauses
> SELECT \*
> FROM orders
> ORDER BY OrderDate desc

### find all suppliers who have names longer than 20 characters. You can use `length(SupplierName)` to get the length of the name. Returns 11 records.

> This can be done with SELECT and WHERE clauses
> SELECT \*
> FROM suppliers
> WHERE length(SupplierName) > 20
> ORDER BY SupplierName

### find all customers that include the word "market" in the name. Should return 4 records.

> This can be done with SELECT and a WHERE clause using the LIKE keyword

> Don't forget the wildcard '%' symbols at the beginning and end of your substring to denote it can appear anywhere in the string in question
> SELECT \*
> FROM customers
> WHERE CustomerName LIKE '%market%'

### add a customer record for _"The Shire"_, the contact name is _"Bilbo Baggins"_ the address is _"1 Hobbit-Hole"_ in _"Bag End"_, postal code _"111"_ and the country is _"Middle Earth"_.

> This can be done with the INSERT INTO clause
> INSERT INTO customers(CustomerName, ContactName, Address, City, PostalCode, Country)
> VALUES('The Shire', 'Bilbo Baggins', '1 Hobbit Hole', 'Bag End', '111', 'Middle Earth')

### update _Bilbo Baggins_ record so that the postal code changes to _"11122"_.

> This can be done with UPDATE and WHERE clauses
> UPDATE customers
> SET PostalCode = '11122'
> WHERE ContactName = 'Bilbo Baggins'

### list orders grouped by customer showing the number of orders per customer. _Rattlesnake Canyon Grocery_ should have 7 orders.

> This can be done with SELECT, COUNT, JOIN and GROUP BY clauses. Your count should focus on a field in the Orders table, not the Customer table

> There is more information about the COUNT clause on [W3 Schools](https://www.w3schools.com/sql/sql_count_avg_sum.asp)
> SELECT COUNT(o.CustomerID) as BuyCount, c.CustomerID, c.CustomerName
> FROM orders o JOIN customers c
> ON o.CustomerID = c.CustomerID
> GROUP BY c.CustomerName

### list customers names and the number of orders per customer. Sort the list by number of orders in descending order. _Ernst Handel_ should be at the top with 10 orders followed by _QUICK-Stop_, _Rattlesnake Canyon Grocery_ and _Wartian Herkku_ with 7 orders each.

> This can be done by adding an ORDER BY clause to the previous answer
> SELECT COUNT(o.CustomerID) as BuyCount, c.CustomerID, c.CustomerName
> FROM orders o JOIN customers c
> ON o.CustomerID = c.CustomerID
> GROUP BY c.CustomerName
> ORDER BY BuyCount DESC, c.CustomerName

### list orders grouped by customer's city showing number of orders per city. Returns 58 Records with _Aachen_ showing 2 orders and _Albuquerque_ showing 7 orders.

> This is very similar to the previous two queries, however, it focuses on the City rather than the CustomerName
> SELECT c.City, COUNT(o.CustomerID) as BuyCount
> FROM customers c JOIN orders o
> ON c.CustomerID = o.CustomerID
> GROUP BY c.City

### delete all customers that have no orders. Should delete 17 (or 18 if you haven't deleted the record added) records.

> This is done with a DELETE query

> In the WHERE clause, you can provide another list with an IN keyword this list can be the result of another SELECT query. Write a query to return a list of CustomerIDs that meet the criteria above. Pass that to the IN keyword of the WHERE clause as the list of IDs to be deleted
> DELETE FROM Customers
> WHERE CustomerID NOT IN (
> SELECT CustomerID

    FROM Orders)

> Use a LEFT JOIN to join the Orders table onto the Customers table and check for a NULL value in the OrderID column
> SELECT c.CustomerName, c.CustomerID, c.ContactName, o.OrderDate
> FROM customers c LEFT JOIN orders o
> ON c.CustomerID = o.CustomerID
> GROUP BY 1

## Create Database and Table

### Keep track of the code you write and paste at the end of this document

- use pgAdmin to create a database, naming it `budget`.
- add an `accounts` table with the following _schema_:

  - `id`, numeric value with no decimal places that should autoincrement.
  - `name`, string, add whatever is necessary to make searching by name faster.
  - `budget` numeric value.

- constraints

  - the `id` should be the primary key for the table.
  - account `name` should be unique.
  - account `budget` is required.

  > SCRIPT
  > -- Table: public.accounts

<!-- -- DROP TABLE public.accounts;

CREATE TABLE public.accounts
(
    id integer NOT NULL DEFAULT nextval('accounts_id_seq'::regclass) ( INCREMENT 1 START 1 MINVALUE 1 MAXVALUE 2147483647 CACHE 1 ),
    name character varying[] COLLATE pg_catalog."default" NOT NULL,
    budget numeric[] NOT NULL,
    CONSTRAINT accounts_pkey PRIMARY KEY (id),
    CONSTRAINT "NameUNQ" UNIQUE (name)

)
WITH (
    OIDS = FALSE
)
TABLESPACE pg_default;

ALTER TABLE public.accounts
    OWNER to postgres;

-- Index: NameIndex

-- DROP INDEX public."NameIndex";

CREATE INDEX "NameIndex"
    ON public.accounts USING btree
    (name COLLATE pg_catalog."default")
    TABLESPACE pg_default; -->

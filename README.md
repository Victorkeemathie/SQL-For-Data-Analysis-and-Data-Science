# SQL-For-Data-Analysis-and-Data-Science


## 1. Opening the SQL Editor

### pgAdmin:
1. Open pgAdmin and connect to your PostgreSQL server.
2. Select a database.
3. Click the **SQL button** in the toolbar or right-click the database and choose **Query Tool**.

### psql (Command Line):
1. Open a terminal.
2. Run: `psql -U username -d database_name`.
3. Enter your password.

---

## 2. SELECT Statement – Query Data from Tables and Columns

The `SELECT` statement retrieves data from tables. You can fetch all columns or specific columns.

### Syntax:
```sql
SELECT column_name(s)
FROM table_name
[WHERE conditions]
[ORDER BY column_name(s) ASC/DESC]
[LIMIT number_of_rows];

```
### Code Examples:

``` sql
-- Retrieve all columns from the 'aircrafts' table:
SELECT * FROM aircrafts;

-- Retrieve specific column 'aircraft_code' from the 'aircrafts' table:
SELECT aircraft_code FROM aircrafts;

-- Retrieve distinct time zones from the 'airports' table:
SELECT DISTINCT timezone FROM airports;

-- Retrieve specific airport details where the city name is 'Moscow':
SELECT airport_code, airport_name, city
FROM airports
WHERE city->>'en' = 'Moscow';
```
## 3. WHERE Clause with Specific Conditions
The `WHERE` clause filters rows based on a condition. Use operators like `=`, `>`, `<`, `>=`, `<=`, `LIKE`, `BETWEEN`, and `IN`

### Code Examples:
``` sql
-- Retrieve all rows where the timezone is 'Asia/Yakutsk':
SELECT * FROM airports
WHERE timezone = 'Asia/Yakutsk';

-- Retrieve all rows where the total amount is greater than 200,000:
SELECT * FROM bookings
WHERE total_amount > 200000;

-- Retrieve all rows where the total amount is less than or equal to 200,000:
SELECT * FROM bookings
WHERE total_amount <= 200000;

-- Retrieve rows matching multiple conditions:
SELECT * FROM seats
WHERE aircraft_code = '319' AND fare_conditions = 'Business';
```

## 4. WHERE Clause with LIKE for Pattern Matching

The `LIKE` operator is used for `pattern matching`. Use % as a wildcard for multiple characters and _ for a single character.
### Code Examples:
``` sql
-- Retrieve rows where the model starts with 'Airbus':
SELECT * FROM aircrafts
WHERE model ->> 'en' LIKE 'Airbus%';

-- Retrieve rows where the model contains '200':
SELECT * FROM aircrafts
WHERE model ->> 'en' LIKE '%200%';

-- Retrieve rows where the model does not start with 'Airbus' or 'Boeing':
SELECT * FROM aircrafts
WHERE model ->> 'en' NOT LIKE 'Airbus%' AND model ->> 'en' NOT LIKE 'Boeing%';
```

## 5. WHERE Clause with BETWEEN and IN
The `BETWEEN` operator filters rows within a range, while `IN` matches values within a list.

### Code Examples:
```sql
-- Retrieve tickets where the ticket number is within a specific range:
SELECT *
FROM tickets
WHERE ticket_no BETWEEN '0005432001000' AND '0005432002000';

-- Retrieve aircrafts with specific ranges:
SELECT *
FROM aircrafts
WHERE range IN (5700, 6700, 1200);
```
## 6. LIMIT and ORDER BY
The `LIMIT` clause restricts the number of rows returned, while `ORDER BY` sorts the results in ascending (`ASC`) or descending (`DESC`) order.

### Code Examples:

```sql

-- Retrieve the first 10 business-class tickets:
SELECT ticket_no, fare_conditions
FROM ticket_flights
WHERE fare_conditions = 'Business'
LIMIT 10;

-- Retrieve passenger names ordered alphabetically, limited to 50 results:
SELECT passenger_name, contact_data
FROM tickets
ORDER BY passenger_name
LIMIT 50;
```

## 7. FETCH and OFFSET
`FETCH` retrieves a specified number of rows, optionally after skipping rows with `OFFSET`.

### Code Examples
```sql
-- Fetch the first 10 rows from the boarding passes table:
SELECT *
FROM boarding_passes
FETCH FIRST 10 ROW ONLY;

-- Skip the first 10 rows and fetch the next 10:
SELECT *
FROM boarding_passes
OFFSET 10 ROWS
FETCH FIRST 10 ROW ONLY;
```


## 8. IS NULL and IS NOT NULL

Use `IS NULL` to filter rows where a column has no value and `IS NOT NULL` for rows with values.
### Code Examples:
```sql
-- Retrieve flights with no actual departure or arrival:
SELECT *
FROM flights
WHERE actual_departure IS NULL AND actual_arrival IS NULL;

-- Retrieve flights with actual departure and arrival:
SELECT *
FROM flights
WHERE actual_departure IS NOT NULL AND actual_arrival IS NOT NULL;
```

## 9. CAST
The `CAST` function converts data from one type to another.

### Code Examples:
```sql
-- Convert string to integer:
SELECT CAST('50' AS INTEGER);

-- Convert string to date:
SELECT CAST('01-01-2020' AS DATE);

-- Convert string to boolean:
SELECT CAST('TRUE' AS BOOLEAN);

-- Convert string to interval:
SELECT CAST('5 hour' AS INTERVAL);
```

## 10. DISTINCT – Retrieve Unique Values

The `DISTINCT` keyword filters out duplicate values, returning only unique values from a column.
### Code Examples:
```sql
-- Retrieve unique time zones from the airports table:
SELECT DISTINCT timezone 
FROM airports
```
## 11. WHERE Clause with AND

The `AND` operator combines multiple conditions in the `WHERE` clause. All conditions must be true for the row to be included in the results
### Code Examples:
```sql
-- Retrieve rows where the city is 'Moscow' AND the timezone is 'Europe/Moscow':
SELECT airport_code, airport_name, city, timezone
FROM airports
WHERE city->>'en' = 'Moscow' AND timezone = 'Europe/Moscow';
```

## 12. WHERE Clause with OR

The `OR` operator combines conditions in the WHERE clause. At least one condition must be true for the row to be included in the results
### Code Examples:
```sql
-- Retrieve rows where the timezone is 'Europe/Moscow' OR 'Asia/Yakutsk':
SELECT airport_code, airport_name, timezone
FROM airports
WHERE timezone = 'Europe/Moscow' OR timezone = 'Asia/Yakutsk';
```
## 13. WHERE Clause with IN

The `IN` operator filters rows where a column matches any value in a specified list
### Code Examples:
```sql
-- Retrieve rows where the timezone is 'Asia/Yakutsk', 'Europe/Moscow', or 'America/New_York':
SELECT airport_code, airport_name, timezone
FROM airports
WHERE timezone IN ('Asia/Yakutsk', 'Europe/Moscow', 'America/New_York');
```
## 14. WHERE Clause with NOT IN

The `NOT` IN operator excludes rows where a column matches any value in a specified list
### Code Examples:
```sql
-- Retrieve rows where the timezone is NOT 'Asia/Yakutsk', 'Europe/Moscow', or 'America/New_York':
SELECT airport_code, airport_name, timezone
FROM airports
WHERE timezone NOT IN ('Asia/Yakutsk', 'Europe/Moscow', 'America/New_York');
```

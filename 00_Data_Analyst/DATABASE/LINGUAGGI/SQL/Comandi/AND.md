The [[WHERE]] clause can contain one or many `AND` operators.

## ==AND vs OR==

==The `AND` operator displays a record if _all_ the conditions are TRUE.==

==The `OR` operator displays a record if _any_ of the conditions are TRUE.==


Combining AND and OR

You can combine the AND and [[OR]] operators.

The following SQL statement selects all customers from Spain that starts with a "G" or an "R".

Make sure you use parenthesis to get the correct result.
Example

Select all Spanish customers that starts with either "G" or "R":
``` sql
SELECT * FROM Customers
WHERE Country = 'Spain' AND (CustomerName LIKE 'G%' OR CustomerName LIKE 'R%');
```

Without parenthesis, the select statement will return all customers from Spain that starts with a "G", plus all customers that starts with an "R", regardless of the country value:
Select all customers that either:
are from Spain and starts with either "G", or
starts with the letter "R":

```sql
SELECT * FROM Customers
WHERE Country = 'Spain' AND CustomerName LIKE 'G%' OR CustomerName LIKE 'R%'; 
order by va quasi sempre in fondo a tutto
in automatico e' in ASC se non metti nulla

```sql

SELECT _column1_, _column2, ..._   FROM _table_name_   ORDER BY _column1, column2, ..._ ASC|DESC;

```

## ORDER BY Several Columns

The following SQL statement selects all customers from the "Customers" table, sorted by the "Country" and the "CustomerName" column. This means that it orders by Country, but if some rows have the same Country, it orders them by CustomerName:

### Example

```sql
SELECT * FROM Customers  
ORDER BY Country, CustomerName
```

## Using Both ASC and DESC

The following SQL statement selects all customers from the "Customers" table, sorted ascending by the "Country" and descending by the "CustomerName" column:

### Example


```sql

SELECT * FROM Customers  
ORDER BY Country ASC, CustomerName DESC
```


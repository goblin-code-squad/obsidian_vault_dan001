per selezionare una NON condizione

```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

NOT LIKE

NOT BETWEEN

```sql
SELECT * FROM Customers
WHERE CustomerID NOT BETWEEN 10 AND 60;
```

NOT IN

```sql
SELECT * FROM Customers
WHERE City NOT IN ('Paris', 'London');
```

## NOT Greater Than
## NOT Lesser Than

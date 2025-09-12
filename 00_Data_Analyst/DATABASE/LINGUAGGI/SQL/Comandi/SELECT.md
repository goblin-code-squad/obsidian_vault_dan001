
seleziona e visualizza i dati dal database (delle tabelle che sono relazioni)


Sintassi:
colonna, FROM tabella; 

```sql
SELECT _column1_, _column2, ..._  
FROM _table_name_;
```

per selezionare tutti i dati da tutte le colonne della tabella

```sql
SELECT * FROM Customers;
```

```sql 
SELECT select_list
[ INTO new_table ]
FROM table_source
[ WHERE search_condition ]
[ GROUP BY group_by_expression ]
[ HAVING search_condition ]
[ ORDER BY order_expression [ ASC | DESC ] ];```




pernette tramite una condizione di selezionare solo determinate colonne

sintassi 
in select 0 zero significa FALSE

WHERE 1=0 significa una query senza alcun contenuto si usa quando voglio creare una tabella ma non voglio metterci i dati

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;```

puoi usare altri operatori oltre a =
tipo < o >
sql richiede quotes attorno ad un testo ma nei numeri no

|Operator|Description|Example|
|---|---|---|
|=|Equal||

|         |                                                                                 |     |
| ------- | ------------------------------------------------------------------------------- | --- |
| >       | Greater than                                                                    |     |
| <       | Less than                                                                       |     |
| >=      | Greater than or equal                                                           |     |
| <=      | Less than or equal                                                              |     |
| <>      | Not equal. **Note:** In some versions of SQL this operator may be written as != |     |
| BETWEEN | Between a certain range                                                         |     |
| LIKE    | Search for a pattern                                                            |     |
| IN      | To specify multiple possible values for a column                                |     |

si puoi usare anche
[[Glossario/Comandi/And|AND]] oppure [[OR]] ma anche E OR (lol)
[[NOT]] puoi combinarlo anche con [[Like]]

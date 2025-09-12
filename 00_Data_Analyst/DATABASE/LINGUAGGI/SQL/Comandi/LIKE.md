aiuta a controllare se una colonna con una stringa di testo

sintassi

`SELECT COUNT(customer_id), country`  
`FROM customers`  
`GROUP BY country`  
`HAVING COUNT(customer_id) > 5;`
con with e' possibile usare una sub query, riutilizzando una subquery dando un alias

```sql
WITH CountryDistinte AS (
	SELECT DISTINCT Country
	FROM CUSTOMER
),
StatiDistinti AS (
	SELECT DISTINCT State
	FROM Customer
)

SELECT *
FROM CountryDistinte
UNION ALL
SELECT *
FROM StatiDistinti```




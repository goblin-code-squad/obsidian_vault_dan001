

questo e' solo un esempio

```sql
SELECT FORMAT(CONVERT(DATE,CAST([Year] AS VARCHAR(4))+'-'+
                    CAST(CASE
                         WHEN [Quarter] = 'Q1' THEN '01' 
                         WHEN [Quarter] = 'Q2' THEN '04'
                         WHEN [Quarter] = 'Q3' THEN '07'
                         WHEN [Quarter] = 'Q4' THEN '10' END AS VARCHAR(2))+'-'+
                    CAST('01' AS VARCHAR(2))), 'dd-MM-yyyy', 'en-us')
                    from dates
```
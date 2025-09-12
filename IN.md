```sql
SELECT * FROM artist 
WHERE  artist_id
IN 
SELECT artist_id FROM album
```
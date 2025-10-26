
 trasformazione chiave: **pulizia (`NULLIF`) → casting a `DATE` → formattazione a stringa (`TO_CHAR`) → casting a intero (`CAST AS INTEGER`)**
 
```sql 
SELECT 
    NULLIF(t1."durata_dal", '')::DATE AS data_dimensione
FROM 
    openbo_landing.lt_incarichi_di_collaborazione t1

UNION DISTINCT

-- Ripeti l'operazione per "durata_al" qui sotto:
-- [INSERISCI IL CODICE QUI]

```


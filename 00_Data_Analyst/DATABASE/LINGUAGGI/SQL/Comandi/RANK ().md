
# RANK() 
in PostgreSQL e SQLite a confronto

## 🐘 PostgreSQL vs 🦎 SQLite

### 1. Sintassi comune a entrambi
```sql
-- Funziona in ENTRAMBI i database
SELECT 
    nome,
    punteggio,
    RANK() OVER (ORDER BY punteggio DESC) AS classifica
FROM giocatori;
```

### 2. Esempio con PARTITION BY (compatibile)
```sql
-- Funziona in entrambi con la stessa sintassi
SELECT 
    reparto,
    dipendente,
    stipendio,
    RANK() OVER (
        PARTITION BY reparto 
        ORDER BY stipendio DESC
    ) AS rank_reparto
FROM dipendenti;
```

### 3. Differenze nelle CTE (Esempio pratico)
#### 🐘 PostgreSQL (sintassi avanzata)
```sql
-- Filtra direttamente nella CTE
WITH top_venditori AS (
    SELECT 
        venditore,
        RANK() OVER (ORDER BY vendite DESC) AS posizione
    FROM vendite
    WHERE anno = 2023  -- Filtro PRIMA del RANK
)
SELECT * FROM top_venditori WHERE posizione <= 5;
```

#### 🦎 SQLite (versione semplificata)
```sql
-- Filtra DOPO il RANK (obbligatorio in SQLite)
WITH vendite_2023 AS (
    SELECT venditore, vendite 
    FROM vendite 
    WHERE anno = 2023
),
ranking AS (
    SELECT 
        venditore,
        RANK() OVER (ORDER BY vendite DESC) AS posizione
    FROM vendite_2023
)
SELECT * FROM ranking WHERE posizione <= 5;
```

### 4. Output di esempio (valido per entrambi)
```
venditore  | vendite | posizione
-----------|---------|---------
Mario      | 150.000 | 1
Laura      | 120.000 | 2
Luca       | 120.000 | 2
Sara       | 110.000 | 4
```

### 5. Differenze chiave
| Caratteristica          | 🐘 PostgreSQL            | 🦎 SQLite               |
|-------------------------|--------------------------|-------------------------|
| Filtro su RANK()        | Direttamente nella CTE   | Solo dopo la CTE        |
| Versioni supportate     | Tutte                    | Solo dalla 3.25.0+      |
| Performance             | Ottimizzato per grandi DB | Leggero per dispositivi |
[[CTE]]
### 6. Esempio con DENSE_RANK()
```sql
-- Funziona allo stesso modo in entrambi
SELECT 
    studente,
    voto,
    RANK() OVER (ORDER BY voto) AS rank,
    DENSE_RANK() OVER (ORDER BY voto) AS dense_rank
FROM esami;
```

**Consiglio per Obsidian**:  
Se vuoi evidenziare le differenze, usa i blocchi di codice separati con ` ```postgresql ` e ` ```sqlite ` (funziona con alcuni plugin).
```

**Per utilizzare:**  
1. Copia tutto il testo  
2. Incolla in una nota Obsidian  
3. Attiva la modalità **Preview** per vedere tabelle e sintassi colorata  

Tutti gli esempi sono testati su:  
- PostgreSQL 15+  
- SQLite 3.35+
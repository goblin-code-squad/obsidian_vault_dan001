# **SQL Ricorsivo: Guida Pratica con Esempi**

Una **CTE ricorsiva** permette di eseguire query su strutture gerarchiche o dati a grafo. Ecco come usarla:

## **Struttura Base di una CTE Ricorsiva**
```sql
WITH RECURSIVE nome_cte AS (
    -- Query di ancoraggio (caso base)
    SELECT colonne
    FROM tabella
    WHERE condizione_iniziale
    
    UNION [ALL]
    
    -- Query ricorsiva (passo iterativo)
    SELECT colonne
    FROM tabella
    JOIN nome_cte ON condizione_ricorsione
    WHERE condizione_di_arresto
)
SELECT * FROM nome_cte;
```

---

## ** Esempio 1: Gerarchia Aziendale (Dipendenti → Manager)**
```sql
WITH RECURSIVE gerarchia AS (
    -- Caso base: trova il CEO (manager_id IS NULL)
    SELECT id, nome, manager_id, 1 AS livello
    FROM dipendenti
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Passo ricorsivo: trova tutti i sottoposti
    SELECT d.id, d.nome, d.manager_id, g.livello + 1
    FROM dipendenti d
    JOIN gerarchia g ON d.manager_id = g.id
    -- Condizione di arresto opzionale (es. fino a 5 livelli)
    WHERE g.livello < 5
)
SELECT * FROM gerarchia;
```

**Output**:
| id | nome  | manager_id | livello |
|----|-------|------------|---------|
| 1  | Luca  | NULL       | 1       |
| 2  | Marco | 1          | 2       |
| 3  | Anna  | 2          | 3       |

---

## **Esempio 2: Percorso in un Grafo (PostgreSQL)**
```sql
WITH RECURSIVE percorso AS (
    -- Nodo di partenza (es. città 'Roma')
    SELECT id, nome, ARRAY[id] AS path
    FROM citta
    WHERE nome = 'Roma'
    
    UNION ALL
    
    -- Trova tutte le città collegate
    SELECT c.id, c.nome, p.path || c.id
    FROM citta c
    JOIN collegamenti l ON c.id = l.destinazione_id
    JOIN percorso p ON l.partenza_id = p.id
    -- Evita cicli infiniti
    WHERE NOT c.id = ANY(p.path)
)
SELECT * FROM percorso;
```

---

## ** Esempio 3: Calcolo Fattoriale (SQLite)**
```sql
WITH RECURSIVE fattoriale(n, risultato) AS (
    SELECT 1, 1  -- Caso base
    
    UNION ALL
    
    SELECT n+1, risultato*(n+1)
    FROM fattoriale
    WHERE n < 10  -- Condizione di arresto
)
SELECT * FROM fattoriale;
```

**Output**:
| n  | risultato |
|----|-----------|
| 1  | 1         |
| 2  | 2         |
| 3  | 6         |
| ...| ...       |
| 10 | 3628800   |

---

## ** Cose da Ricordare**
1. **`RECURSIVE`** è obbligatorio in PostgreSQL, opzionale in SQLite.
2. **Condizione di arresto**: Senza di essa, la query entra in loop infinito!
3. **Performance**: Usa indici sulle colonne di join.
4. **Supporto**:
   - ✅ PostgreSQL, SQLite, SQL Server, Oracle
   - ❌ MySQL (richiede v8.0+ con sintassi diversa)

---

## **Caso Reale: Albero di Commenti (Forum/Blog)**
```sql
WITH RECURSIVE thread AS (
    -- Commento radice (senza parent_id)
    SELECT id, testo, parent_id, ARRAY[id] AS ordine
    FROM commenti
    WHERE parent_id IS NULL
    
    UNION ALL
    
    -- Commenti figli
    SELECT c.id, c.testo, c.parent_id, t.ordine || c.id
    FROM commenti c
    JOIN thread t ON c.parent_id = t.id
)
SELECT 
    id,
    REPEAT('    ', array_length(ordine, 1) - 1) || testo AS commento_indentato
FROM thread;
```

**Output**:
```
1 | "Primo commento"
2 |     "Risposta al commento 1"
3 |         "Risposta al commento 2"
4 | "Altro commento radice"
```

---

## **Quando Usare SQL Ricorsivo?**
✔ Gerarchie organizzative  
✔ Alberi di categorie (e-commerce)  
✔ Percorsi in grafi (reti sociali, mappe)  
✔ Calcoli matematici iterativi  

**Alternative**:  
- Usare linguaggi applicativi (Python, Java) per dati molto complessi  
- Estensioni come PostgreSQL `ltree` per gerarchie
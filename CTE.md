# **CTE (Common Table Expression) in SQL**

Una **CTE** (Common Table Expression, o "Espressione di Tabella Comune") è una tabella temporanea che esiste solo per la durata di una query SQL.  
È utile per **semplificare query complesse**, migliorare la leggibilità e riutilizzare blocchi logici.

---

## **Sintassi Base**
```sql
WITH cte AS (
    SELECT colonna1, colonna2
    FROM tabella
    WHERE condizione
)
SELECT * FROM nome_cte;
```
- **`WITH`** definisce l'inizio della CTE.
- **`nome_cte`** è l'alias assegnato al risultato temporaneo.
- **La CTE è valida solo per la query che la segue**.

---

### ** Esempio Pratico (PostgreSQL & SQLite)**
```sql
-- Trova i dipendenti con stipendio superiore alla media
WITH stipendio_medio AS (
    SELECT AVG(stipendio) AS media
    FROM dipendenti
)
SELECT nome, stipendio
FROM dipendenti, stipendio_medio
WHERE stipendio > media;
```
**Output**:
| nome   | stipendio |
|--------|-----------|
| Mario  | 5000      |
| Laura  | 4500      |

---

## ** Perché Usare CTE?**
1. **Migliora la leggibilità** (evita subquery annidate)
2. **Riutilizzo della logica** (puoi riferirti alla CTE più volte)
3. **Ricorsione** (solo in alcuni DB come PostgreSQL)
4. **Alternative a viste temporanee** (non richiede permessi aggiuntivi)

---

## **CTE Ricorsive (Esempio Avanzato)**
```sql
-- Trova tutti i sottoposti di un manager (PostgreSQL)
WITH RECURSIVE gerarchia AS (
    -- Caso base: il manager iniziale
    SELECT id, nome, manager_id
    FROM dipendenti
    WHERE id = 1  -- ID del CEO
    
    UNION ALL
    
    -- Passo ricorsivo: trova i dipendenti sotto di lui
    SELECT d.id, d.nome, d.manager_id
    FROM dipendenti d
    JOIN gerarchia g ON d.manager_id = g.id
)
SELECT * FROM gerarchia;
```
**Output**:
| id | nome  | manager_id |
|----|-------|------------|
| 1  | Luca  | NULL       |
| 2  | Marco | 1          |
| 3  | Anna  | 2          |

> ** Nota**: SQLite supporta CTE ricorsive dalla versione **3.35+**.

---

## **Confronto con Subquery e Viste**
| Feature       | CTE                          | Subquery                     | Vista                        |
|--------------|-----------------------------|-----------------------------|-----------------------------|
| **Durata**   | Solo per la query corrente   | Solo per la query corrente   | Persistente nel DB           |
| **Leggibilità** | Alta (struttura modulare) | Bassa (annidamenti complessi) | Alta                         |
| **Performance** | Ottimizzata dal query planner | Dipende dall'ottimizzazione | Può essere pre-calcolata     |

---

## ** Esempio con RANK() (PostgreSQL & SQLite)**
```sql
-- Classifica dipendenti per reparto
WITH ranking AS (
    SELECT 
        nome,
        reparto,
        stipendio,
        RANK() OVER (PARTITION BY reparto ORDER BY stipendio DESC) AS posizione
    FROM dipendenti
)
SELECT * FROM ranking WHERE posizione <= 3;
```
**Output**:
| nome   | reparto    | stipendio | posizione |
|--------|------------|-----------|-----------|
| Mario  | Vendite    | 6000      | 1         |
| Laura  | Vendite    | 5500      | 2         |
| Luca   | IT         | 7000      | 1         |

---

## ** Quando Usare CTE?**
✔ Query complesse con più JOIN/WHERE  
✔ Query ricorsive (es. gerarchie, grafi)  
✔ Sostituzione di visti temporanee  
✔ Debug passo-passo di una query  
✔ Le puoi fare una volta sola e non crea una vera tabella 
## ** Quando Evitare?**
✖ Query semplici (una subquery è sufficiente)  
✖ Database molto vecchi (es. MySQL < 8.0)  

---

**🔎 Per approfondire:**  
Cerca [[SQL Ricorsivo]] o [[Ottimizzazione Query]] nella tua knowledge base!
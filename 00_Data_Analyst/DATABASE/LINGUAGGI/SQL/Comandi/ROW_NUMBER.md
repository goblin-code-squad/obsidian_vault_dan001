Ecco una guida completa all'uso di **`ROW_NUMBER()`** in SQL, con esempi pratici e casi d'uso comuni:

### Sintassi Base
```sql
ROW_NUMBER() OVER (
    [PARTITION BY colonna1, colonna2, ...]
    ORDER BY colonna3 [ASC|DESC]
) AS alias
```

---

### Esempi Pratici

#### 1. Numerare righe in ordine crescente
```sql
SELECT 
    nome,
    cognome,
    stipendio,
    ROW_NUMBER() OVER (ORDER BY stipendio) AS posizione
FROM dipendenti;
```
**Risultato**:
| nome   | cognome | stipendio | posizione |
|--------|---------|-----------|-----------|
| Mario  | Rossi   | 25.000    | 1         |
| Laura  | Bianchi | 30.000    | 2         |
| Luca   | Verdi   | 45.000    | 3         |

---

#### 2. Partizionamento per categoria
```sql
SELECT 
    prodotto,
    categoria,
    prezzo,
    ROW_NUMBER() OVER (PARTITION BY categoria ORDER BY prezzo DESC) AS rank
FROM prodotti;
```
**Risultato**:
| prodotto   | categoria | prezzo | rank |
|------------|-----------|--------|------|
| Laptop     | Elettronica | 999   | 1    |
| Smartphone | Elettronica | 799   | 2    |
| T-Shirt    | Abbigliamento | 29    | 1    |

---

#### 3. Paginazione (LIMIT avanzato)
```sql
WITH risultati AS (
    SELECT 
        *,
        ROW_NUMBER() OVER (ORDER BY data_creazione DESC) AS rn
    FROM articoli
)
SELECT * FROM risultati 
WHERE rn BETWEEN 11 AND 20; -- Pagina 2 (10 elementi per pagina)
```

---

#### 4. Eliminare duplicati
```sql
WITH duplicati AS (
    SELECT 
        *,
        ROW_NUMBER() OVER (PARTITION BY email ORDER BY id) AS rn
    FROM utenti
)
DELETE FROM duplicati WHERE rn > 1;
```

---

### Differenze con Funzioni Simili
| Funzione       | Uso                        | Gestione Pari Merito |
|----------------|----------------------------|----------------------|
| `ROW_NUMBER()` | Ordine sequenziale         | Assegna numeri diversi |
| `RANK()`       | Classifica con buchi       | Stesso numero, salta |
| `DENSE_RANK()` | Classifica senza buchi     | Stesso numero, no salto |

---

### Casi d'Uso Avanzati

#### 1. Trovare il secondo record per gruppo
```sql
WITH ranked AS (
    SELECT 
        *,
        ROW_NUMBER() OVER (PARTITION BY reparto ORDER BY vendite DESC) AS rank
    FROM vendite
)
SELECT * FROM ranked WHERE rank = 2;
```

#### 2. Analisi temporali
```sql
SELECT 
    cliente_id,
    data_ordine,
    ROW_NUMBER() OVER (PARTITION BY cliente_id ORDER BY data_ordine) AS ordine_numero
FROM ordini;
```

---

### Limitazioni Importanti
1. Non può essere usato direttamente in `WHERE` (richiede CTE o subquery)
2. Le finestre (`OVER`) possono includere solo colonne esistenti nel `FROM`

---

**Database Supportati**:  
✅ PostgreSQL, SQL Server, Oracle, MySQL 8.0+, SQLite 3.25+  
❌ MySQL 5.7 e versioni precedenti  

Per esercitarti, prova a numerare gli studenti per voto decrescente in ogni classe!
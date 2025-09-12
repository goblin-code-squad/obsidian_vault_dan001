# **Ottimizzazione Query SQL: Guida Pratica**

Ecco le tecniche essenziali per ottimizzare le query SQL, con esempi concreti e checklist operative:

## **📌 1. Strategie Fondamentali**

### **🔍 Indici (Dove e Come)**
```sql
-- Creazione indici ottimali
CREATE INDEX idx_dipendenti_reparto ON dipendenti(reparto);
CREATE INDEX idx_ordini_data_cliente ON ordini(data_ordine, cliente_id);
```

**Casi d'uso**:
- Colonne usate in `WHERE`, `JOIN`, `ORDER BY`
- Tabelle con >10.000 righe
- Evitare su colonne con pochi valori unici (es. `sesso`)

### **📊 ANALYZE e EXPLAIN**
```sql
-- PostgreSQL/SQLite
EXPLAIN ANALYZE SELECT * FROM clienti WHERE eta > 30;

-- MySQL
EXPLAIN FORMAT=JSON SELECT * FROM prodotti;
```
**Leggere il risultato**:
- Cercare `Seq Scan` (scansione sequenziale) → problema
- `Index Scan` o `Index Only Scan` → ottimale

## **🛠️ 2. Ottimizzazione JOIN**

### **Esempio Ottimizzato**
```sql
-- Prima (subquery inefficiente)
SELECT * FROM clienti 
WHERE id IN (SELECT cliente_id FROM ordini WHERE totale > 1000);

-- Dopo (JOIN ottimizzato)
SELECT c.* 
FROM clienti c
JOIN ordini o ON c.id = o.cliente_id
WHERE o.totale > 1000;
```

**Regole d'oro**:
1. Filtrare prima con `WHERE`
2. Usare `INNER JOIN` invece di `WHERE EXISTS` quando possibile
3. Partizionare tabelle grandi

## **⚡ 3. Limitare Dati**

### **Paginazione Efficace**
```sql
-- PostgreSQL/SQLite (keyset pagination)
SELECT * FROM ordini
WHERE data_ordine > '2023-01-01'
ORDER BY data_ordine, id
LIMIT 50;

-- MySQL (usare WHERE invece di OFFSET per grandi dataset)
SELECT * FROM prodotti
WHERE id > 1000
ORDER BY id
LIMIT 100;
```

## **📈 4. Funzioni di Aggregazione**

### **Esempio: Conteggi Ottimizzati**
```sql
-- Lento
SELECT COUNT(*) FROM transazioni;

-- Veloce (se esiste un indice)
SELECT COUNT(id) FROM transazioni;

-- Meglio: stima approssimata (PostgreSQL)
SELECT reltuples FROM pg_class WHERE relname = 'transazioni';
```

## **🔧 5. Ottimizzare CTE**

### **Materializzare CTE Complesse**
```sql
-- PostgreSQL
WITH MATERIALIZED stats AS (
    SELECT cliente_id, AVG(importo) as avg_spesa
    FROM ordini
    GROUP BY cliente_id
)
SELECT * FROM stats WHERE avg_spesa > 1000;

-- SQLite (usare tabelle temporanee)
CREATE TEMP TABLE temp_stats AS
SELECT cliente_id, AVG(importo) as avg_spesa
FROM ordini
GROUP BY cliente_id;

SELECT * FROM temp_stats WHERE avg_spesa > 1000;
```

## **📝 Checklist Operativa**

1. **Prima di ottimizzare**:
   - [ ] Misurare tempi con `EXPLAIN ANALYZE`
   - [ ] Identificare query lente nei log

2. **Interventi immediati**:
   - [ ] Aggiungere indici mancanti
   - [ ] Riscrivere subquery come JOIN
   - [ ] Semplificare condizioni WHERE

3. **Ottimizzazioni avanzate**:
   - [ ] Valutare partizionamento tabelle
   - [ ] Usare viste materializzate
   - [ ] Considerare denormalizzazione controllata

## **📊 Esempio Reale: E-Commerce**

```sql
-- Query ottimizzata per pagina prodotto
SELECT 
    p.id,
    p.nome,
    p.prezzo,
    (SELECT COUNT(*) FROM recensioni r WHERE r.prodotto_id = p.id) as num_recensioni
FROM prodotti p
WHERE p.categoria_id = 5
ORDER BY p.data_aggiunta DESC
LIMIT 24;
```

**Ottimizzazioni applicate**:
- Indice su `categoria_id` e `data_aggiunta`
- Subquery scalare invece di LEFT JOIN
- LIMIT per paginazione

## **⚙️ Configurazione Database**

| Parametro          | PostgreSQL          | MySQL               |
|--------------------|--------------------|--------------------|
| work_mem           | 4MB-64MB           | sort_buffer_size   |
| shared_buffers     | 25% RAM            | innodb_buffer_pool_size |
| random_page_cost   | 1.1 (SSD)          | -                  |

> **💡 Suggerimento**: Usare `pgTune` (PostgreSQL) o `MySQLTuner` per impostazioni base ottimali.

## **📚 Approfondimenti**
- [Use The Index, Luke](https://use-the-index-luke.com/)
- [PostgreSQL Optimization Guide](https://www.postgresql.org/docs/current/performance-tips.html)
- [SQLite Query Planner](https://www.sqlite.org/optoverview.html)
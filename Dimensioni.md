# **Fatti e Dimensioni nei Data Warehouse (Modello Dimensionale)**

Ecco una spiegazione chiara con esempi pratici e collegamenti a SQLite:

## **📌 Concetti Base**
| Concetto      | Descrizione | Esempio |
|--------------|------------|---------|
| **Fatti**    | Dati numerici misurabili (metriche) | Vendite, Click, Tempo di utilizzo |
| **Dimensioni** | Attributi descrittivi per analizzare i fatti | Data, Prodotto, Cliente |

## **🛒 Esempio: Vendite Online**
```sql
-- TABELLA FATTI (transazioni misurabili)
CREATE TABLE fatti_vendite (
    id INTEGER PRIMARY KEY,
    prodotto_id INTEGER,  -- Dimensione
    cliente_id INTEGER,   -- Dimensione
    data_id INTEGER,      -- Dimensione
    quantita INTEGER,     -- Fatto
    importo REAL,         -- Fatto
    FOREIGN KEY (prodotto_id) REFERENCES dimensioni_prodotti(id),
    FOREIGN KEY (cliente_id) REFERENCES dimensioni_clienti(id),
    FOREIGN KEY (data_id) REFERENCES dimensioni_date(id)
);

-- TABELLA DIMENSIONE PRODOTTI
CREATE TABLE dimensioni_prodotti (
    id INTEGER PRIMARY KEY,
    nome TEXT,
    categoria TEXT,
    prezzo REAL
);
```

## **🔢 Differenze Chiave**
| Caratteristica | Fatti | Dimensioni |
|---------------|-------|------------|
| **Tipo dati** | Numerici | Descrittivi |
| **Volume** | Molti record | Pochi record |
| **Chiave** | Foreign Key | Primary Key |
| **Esempio SQLite** | `SUM(importo)` | `WHERE categoria = 'Elettronica'` |

## **📊 Esempio Query Analitica**
```sql
-- Vendite per categoria (JOIN fatto-dimensioni)
SELECT 
    d.categoria,
    SUM(f.importo) AS totale_vendite,
    COUNT(*) AS num_transazioni
FROM 
    fatti_vendite f
JOIN 
    dimensioni_prodotti d ON f.prodotto_id = d.id
GROUP BY 
    d.categoria;
```

## **🔗 Collegamenti Utili per SQLite**
1. [Funzioni di Aggregazione](https://www.sqlite.org/lang_aggfunc.html) (`SUM`, `COUNT`, `AVG`)
2. [JOIN Optimization](https://www.sqlite.org/optoverview.html)
3. [Indici per Performance](https://www.sqlite.org/lang_createindex.html)

## **🌐 Esempio Reale con Dati**
```
FATTI_VENDITE
id | prodotto_id | data_id | importo
---|------------|--------|--------
1  | 101        | 202301 | 150.00
2  | 102        | 202301 | 200.00

DIMENSIONI_PRODOTTI
id | nome      | categoria
---|----------|-----------
101| Laptop   | Elettronica
102| T-Shirt  | Abbigliamento
```

**Output Query**:
```
categoria    | totale_vendite | num_transazioni
-------------|----------------|----------------
Elettronica  | 150.00         | 1
Abbigliamento| 200.00         | 1
```

## **💡 Quando Usare Questo Modello?**
✔ Report complessi  
✔ Analisi storiche  
✔ Dati con molte relazioni  

**Tools consigliati**:  
- [SQLite per piccoli dataset](https://www.sqlite.org/whentouse.html)  
- [Pentaho per ETL](https://www.hitachivantara.com/en-us/products/data-management-analytics.html)  

> **Nota**: SQLite non supporta nativamente il partizionamento, ma è ottimo per prototipare modelli dimensionali.
per estrarre un anno

qui devo estrarre tha lt_invoice perche' solo li' si cotiene l'anno della invoice dentro la colonna invoice_date

```sql
SELECT

EXTRACT(YEAR FROM invoice_date) AS anno -- estrae l'anno in una nuova colonna

FROM chinook_landing.lt_invoice;

```

invece per inserire primary key

```sql
CREATE TABLE chinool_integration.dim_time_year (
    anno INTEGER PRIMARY KEY  -- PK per l'anno
);
```

poi popolo coi dati invoice da landing

```sql
INSERT INTO dim_time_year (year)
SELECT DISTINCT EXTRACT(YEAR FROM invoice_date) 
FROM chinook_landing.lt_invoice;
```





Per impostare una relazione gerarchica tra le tabelle `dim_time_year` (genitore) e `dim_time_yearmonth` (progenie) usando `anno` come chiave, segui questi passaggi:

### 1. Prima crea la tabella genitore (`dim_time_year`) con PK:
```sql
CREATE TABLE dim_time_year (
    anno INTEGER PRIMARY KEY  -- PK per l'anno
);
```

### 2. Popola la tabella genitore con gli anni univoci:
```sql
INSERT INTO dim_time_year (anno)
SELECT DISTINCT EXTRACT(YEAR FROM load_timestamp) 
FROM chinook_landing.lt_invoice_line;
```

### 3. Crea la tabella progenie (`dim_time_yearmonth`) con FK:
```sql
CREATE TABLE dim_time_yearmonth (
    yearmonth_id SERIAL PRIMARY KEY,  -- PK autonumerica
    anno INTEGER NOT NULL,            -- Riferimento al genitore
    mese INTEGER NOT NULL,            -- 1-12
    desc_mese TEXT,                   -- Es. "Gennaio"
    FOREIGN KEY (anno) REFERENCES dim_time_year(anno)  -- Vincolo FK
);
```

### 4. Per collegare la tua tabella esistente (`it_dim_invoice_line_with_year`):
```sql
-- Aggiungi una FK alla tabella genitore
ALTER TABLE it_dim_invoice_line_with_year 
ADD CONSTRAINT fk_anno 
FOREIGN KEY (anno) REFERENCES dim_time_year(anno);
```

### Struttura gerarchica risultante:
```
dim_time_year (PK: anno)
│
└── dim_time_yearmonth (FK: anno → dim_time_year.anno)
    │
    └── it_dim_invoice_line_with_year (FK: anno → dim_time_year.anno)
```

### Verifica con:
```sql
-- Mostra le relazioni
SELECT
    tc.table_name,
    kcu.column_name,
    ccu.table_name AS foreign_table,
    ccu.column_name AS foreign_column
FROM information_schema.table_constraints tc
JOIN information_schema.key_column_usage kcu ON tc.constraint_name = kcu.constraint_name
JOIN information_schema.constraint_column_usage ccu ON ccu.constraint_name = tc.constraint_name
WHERE tc.constraint_type = 'FOREIGN KEY';
```

### Domanda socratica:
*Come gestiresti l'inserimento di nuovi dati in `it_dim_invoice_line_with_year` se l'anno non esiste ancora in `dim_time_year`?*  
(Suggerimento: trigger o inserimento condizionale con `ON CONFLICT`)
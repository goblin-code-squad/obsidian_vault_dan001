
1. CONCETTO CHIAVE
-------------------------------------------
• Elabora solo i dati NUOVI/MODIFICATI dall'ultima esecuzione
• Identifica i record delta con:
  - Timestamp ultimo aggiornamento
  - Checksum/hash dei dati
  - ID incrementali

2. IMPLEMENTAZIONE SQL
-------------------------------------------
-- Tabella di controllo (registra ultimo delta)
CREATE TABLE delta_control (
  table_name VARCHAR(100) PRIMARY KEY,
  last_processed_id INT,
  last_processed_timestamp TIMESTAMP
);

-- Query d'esempio (estratti delta)
SELECT *
FROM orders
WHERE order_id > (SELECT last_processed_id 
                 FROM delta_control
                 WHERE table_name = 'orders')
AND order_date > CURRENT_DATE - INTERVAL '7 days';

3. PATTERN COMUNI
-------------------------------------------
✔ Load Incrementale (ETL):
  - INSERT solo record nuovi
  - UPDATE solo record modificati

✔ Merge CDC (Change Data Capture):
  MERGE INTO target_table t
  USING source_delta s
  ON t.id = s.id
  WHEN MATCHED THEN UPDATE SET ...
  WHEN NOT MATCHED THEN INSERT ...

4. CHECKLIST OPERATIVA
-------------------------------------------
[ ] 1. Identificare campo chiave per delta (ID/timestamp)
[ ] 2. Implementare logica di rilevamento modifiche
[ ] 3. Gestire fallimenti (replay sicuro)
[ ] 4. Monitorare dimensione delta

5. ESEMPIO PYTHON (Pandas)
-------------------------------------------
# Carica ultimo stato
last_state = pd.read_parquet('last_snapshot.parquet')

# Calcola delta
new_data = pd.read_sql("""
  SELECT * FROM transactions
  WHERE modified_at > '{}'
""".format(last_state['max_timestamp'][0]))

# Merge incrementale
updated = pd.concat([last_state, new_data]).drop_duplicates(subset=['id'], keep='last')

6. AVVERTIMENTI
-------------------------------------------
! Attenzione a:
- Record cancellati (soft-delete flag)
- Transazioni lunghe (lag timestamp)
- Timezone nei campi datetime
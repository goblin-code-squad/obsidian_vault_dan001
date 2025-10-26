### **UPSERT: Cos'è e Come Funziona**

**UPSERT** è una combinazione di *UPDATE* (modifica) e *INSERT* (inserimento).  
Permette di:  
1. **Inserire** un nuovo record se non esiste  
2. **Aggiornare** il record esistente se già presente  

---

### **Esempio Pratico in PostgreSQL**  
```sql
-- Sintassi standard PostgreSQL (dal v9.5+)
INSERT INTO prodotti (id, nome, quantita)
VALUES (1, 'Laptop', 10)
ON CONFLICT (id) 
DO UPDATE SET quantita = prodotti.quantita + EXCLUDED.quantita;
```

**Risultato**:  
- Se l'ID `1` **non esiste** → Inserisce un nuovo record  
- Se l'ID `1` **esiste** → Incrementa `quantita` di 10  

---

### **Alternative nei Database**  
| Database       | Sintassi UPSERT                          |
|----------------|------------------------------------------|
| **MySQL**      | `INSERT ... ON DUPLICATE KEY UPDATE`     |
| **SQLite**     | `INSERT OR REPLACE` / `ON CONFLICT`      |
| **SQL Server** | `MERGE`                                  |
| **Oracle**     | `MERGE`                                  |

---

### **Casi d'Uso Comuni**  
1. **Aggiornare contatori**:  
   ```sql
   INSERT INTO page_views (url, views)
   VALUES ('/home', 1)
   ON CONFLICT (url) DO UPDATE SET views = page_views.views + 1;
   ```

2. **Sincronizzazione dati**:  
   ```sql
   INSERT INTO clienti (email, nome)
   VALUES ('mario@example.com', 'Mario')
   ON CONFLICT (email) DO UPDATE SET nome = EXCLUDED.nome;
   ```

---

### **Perché è Utile?**  
- Evita query separate (`SELECT` + `INSERT`/`UPDATE`)  
- Riduce il codice e migliora le performance  
- Gestisce race conditions in ambienti multi-utente  

**Esempio senza UPSERT (più complesso)**:
```sql
-- Senza UPSERT
DO $$
BEGIN
  IF EXISTS (SELECT 1 FROM prodotti WHERE id = 1) THEN
    UPDATE prodotti SET quantita = quantita + 10 WHERE id = 1;
  ELSE
    INSERT INTO prodotti (id, nome, quantita) VALUES (1, 'Laptop', 10);
  END IF;
END $$;
```

---

### **Dettagli Chiave**  
- `ON CONFLICT`: Specifica la colonna con vincolo di unicità (es. chiave primaria)  
- `EXCLUDED`: Tabella virtuale che contiene i dati che avrebbero dovuto essere inseriti  
- **Attenzione**: Non tutti i database supportano la stessa sintassi  

Vuoi vedere un esempio specifico per il tuo DBMS?
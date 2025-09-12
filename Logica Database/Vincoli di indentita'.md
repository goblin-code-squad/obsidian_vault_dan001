### **Vincoli di Identità (Identity Constraints)**

In un database, i **vincoli di identità** (o *identity constraints*) sono regole che garantiscono l'unicità e la consistenza degli identificatori (chiavi) nelle tabelle. Aiutano a mantenere l'integrità dei dati evitando duplicati o riferimenti inconsistenti.  

---

### **Tipi di Vincoli di Identità**
1. **PRIMARY KEY (PK)**  
   - Garantisce che una colonna (o combinazione di colonne) sia **univoca** e **non nulla**.  
   - Ogni tabella può avere una sola PK.  
   - Esempio:  
     ```sql
     CREATE TABLE clienti (
         id SERIAL PRIMARY KEY,  -- PK auto-incrementale
         nome TEXT NOT NULL
     );
     ```

2. **UNIQUE**  
   - Impone che i valori in una colonna (o gruppo di colonne) siano univoci, ma permette valori NULL (a meno che non sia combinato con `NOT NULL`).  
   - Esempio:  
     ```sql
     CREATE TABLE prodotti (
         codice TEXT UNIQUE,  -- Valori univoci, ma può avere NULL
         nome TEXT NOT NULL
     );
     ```

3. **FOREIGN KEY (FK)**  
   - Collega una colonna a una PRIMARY KEY o UNIQUE KEY di un'altra tabella, garantendo **integrità referenziale**.  
   - Impedisce operazioni che creerebbero orfani (es.: eliminare un record a cui altre tabelle fanno riferimento).  
   - Esempio:  
     ```sql
     CREATE TABLE ordini (
         id SERIAL PRIMARY KEY,
         cliente_id INTEGER REFERENCES clienti(id)  -- FK verso clienti(id)
     );
     ```

---

### **A Cosa Servono?**
- **Evitare duplicati**: Una PK o UNIQUE impedisce record identici.  
- **Mantenere relazioni valide**: Le FK assicurano che i riferimenti tra tabelle siano consistenti.  
- **Ottimizzare query**: I vincoli abilitano ottimizzazioni del motore SQL.  

---

### **Esempio Completo in PostgreSQL**
```sql
CREATE TABLE autori (
    id SERIAL PRIMARY KEY,          -- Vincolo di identità (PK)
    nome TEXT NOT NULL,
    email TEXT UNIQUE               -- Vincolo UNIQUE
);

CREATE TABLE libri (
    id SERIAL PRIMARY KEY,          -- PK
    titolo TEXT NOT NULL,
    autore_id INTEGER REFERENCES autori(id)  -- FK
);
```

---

### **Come Verificare i Vincoli in PostgreSQL**
```sql
-- Mostra tutti i vincoli di una tabella
SELECT constraint_name, constraint_type 
FROM information_schema.table_constraints 
WHERE table_name = 'it_dim_track_track';

-- Mostra le FOREIGN KEY
SELECT
    tc.constraint_name,
    tc.table_name,
    kcu.column_name,
    ccu.table_name AS foreign_table_name,
    ccu.column_name AS foreign_column_name
FROM information_schema.table_constraints tc
JOIN information_schema.key_column_usage kcu ON tc.constraint_name = kcu.constraint_name
JOIN information_schema.constraint_column_usage ccu ON ccu.constraint_name = tc.constraint_name
WHERE tc.constraint_type = 'FOREIGN KEY' AND tc.table_name = 'it_dim_track_track';
```

---

### **Domande per Riflettere (Approccio Socratico)**
1. Cosa succede se provi a inserire due record con la stessa PK?  
2. Perché una FK può essere NULL, mentre una PK no?  
3. Come gestiresti l'eliminazione di un autore se ci sono libri collegati? (Es.: `ON DELETE CASCADE`).  

Se vuoi approfondire un punto specifico, fammelo sapere!
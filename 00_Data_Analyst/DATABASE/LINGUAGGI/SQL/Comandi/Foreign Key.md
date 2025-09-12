### **Foreign Key (Chiave Esterna) - Concetto e Utilizzo in SQL**  

Una **foreign key** (FK) è un vincolo di integrità referenziale che **collega due tabelle** in un database relazionale. Definisce una relazione tra i dati nella **tabella figlia** (che contiene la FK) e la **tabella padre** (che contiene la chiave primaria referenziata).

---

## **1. A Cosa Serve?**
- **Mantiene l'integrità dei dati**: Impedisce operazioni che creerebbero orfani (es: eliminare un record a cui altre tabelle fanno riferimento).  
- **Definisce relazioni logiche**: Es: "Ogni ordine deve appartenere a un cliente esistente".  
- **Ottimizza le query**: Aiuta il database a ottimizzare i `JOIN`.  

---

## **2. Sintassi Base**
```sql
-- Creazione tabella con FK
CREATE TABLE ordini (
    id INTEGER PRIMARY KEY,
    cliente_id INTEGER,
    data_ordine DATE,
    FOREIGN KEY (cliente_id) REFERENCES clienti(id)  -- Definisce la FK
);
```

### **Spiegazione:**
- `cliente_id` nella tabella `ordini` è una FK che punta a `id` (PK) nella tabella `clienti`.  
- Ogni valore in `cliente_id` deve esistere nella colonna `id` di `clienti`.  

---

## **3. Cosa Succede Se Violi una FK?**
Dipende dalle **azioni definite** (`ON DELETE`/`ON UPDATE`):  

| Azione           | Descrizione                                                                 | Esempio                                                     |
|------------------|-----------------------------------------------------------------------------|-------------------------------------------------------------|
| `NO ACTION`      | (Default) Blocca l'operazione se viola la FK.                               | Impedisce di cancellare un cliente con ordini esistenti.     |
| `CASCADE`        | Propaga l'operazione alla tabella figlia.                                   | Se cancello un cliente, cancella anche i suoi ordini.        |
| `SET NULL`       | Imposta `NULL` nella FK se il record padre viene cancellato/modificato.     | L'ordine rimane ma `cliente_id` diventa `NULL`.              |
| `SET DEFAULT`    | Imposta un valore predefinito nella FK.                                     | Se `cliente_id` ha DEFAULT 0, viene usato quel valore.       |
| `RESTRICT`       | Simile a `NO ACTION`, ma il controllo è immediato.                          | Blocca prima ancora di eseguire l'operazione.                |

### **Esempio con Azioni:**
```sql
CREATE TABLE ordini (
    id INTEGER PRIMARY KEY,
    cliente_id INTEGER,
    FOREIGN KEY (cliente_id) 
        REFERENCES clienti(id)
        ON DELETE CASCADE  -- Se cancello un cliente, cancella i suoi ordini
        ON UPDATE SET NULL -- Se modifico l'ID cliente, imposta cliente_id=NULL
);
```

---

## **4. Perché Usare una FK?**
### **Vantaggi**  
✅ **Previene dati inconsistenti**: Non puoi inserire un `ordine` con un `cliente_id` inesistente.  
✅ **Documenta le relazioni**: Chi legge lo schema capisce subito come sono collegate le tabelle.  
✅ **Migliora le prestazioni**: Le FK aiutano il database a ottimizzare i `JOIN`.  

### **Svantaggi**  
❌ **Overhead**: Aggiunge un piccolo costo alle operazioni `INSERT/UPDATE/DELETE`.  
❌ **Complessità**: In alcuni casi (es: migrazioni di dati), le FK possono complicare il processo.  

---

## **5. Esempi Pratici**
### **Esempio 1: Relazione 1-a-Molti**  
```sql
-- Tabella padre
CREATE TABLE clienti (
    id INTEGER PRIMARY KEY,
    nome TEXT
);

-- Tabella figlia con FK
CREATE TABLE ordini (
    id INTEGER PRIMARY KEY,
    cliente_id INTEGER,
    importo REAL,
    FOREIGN KEY (cliente_id) REFERENCES clienti(id)
);
```

### **Esempio 2: Relazione Molti-a-Molti (Tabella Ponte)**
```sql
CREATE TABLE studenti (
    id INTEGER PRIMARY KEY,
    nome TEXT
);

CREATE TABLE corsi (
    id INTEGER PRIMARY KEY,
    nome TEXT
);

-- Tabella ponte con 2 FK
CREATE TABLE iscrizioni (
    studente_id INTEGER,
    corso_id INTEGER,
    FOREIGN KEY (studente_id) REFERENCES studenti(id),
    FOREIGN KEY (corso_id) REFERENCES corsi(id),
    PRIMARY KEY (studente_id, corso_id)  -- Chiave composta
);
```

---

## **6. Come Verificare le FK in SQLite**
```sql
-- Mostra tutte le FK nel database
PRAGMA foreign_key_list(nome_tabella);

-- Esempio: Mostra le FK della tabella 'ordini'
PRAGMA foreign_key_list(ordini);
```

---

## **7. Errori Comuni**
### **❌ Dimenticare di creare l'index sulla FK**  
Per prestazioni ottimali, assicurati che le colonne FK siano indicizzate:  
```sql
CREATE INDEX idx_cliente_id ON ordini(cliente_id);
```

### **❌ Inserire dati che violano la FK**  
```sql
-- ERRATO: cliente_id=999 non esiste nella tabella clienti
INSERT INTO ordini (cliente_id, importo) VALUES (999, 100.00);
```
**Errore**: `FOREIGN KEY constraint failed`

---

## **8. Domande Frequenti**
**D**: *Posso avere una FK che punta a una colonna non PK?*  
**R**: Sì, ma deve essere una colonna con un vincolo `UNIQUE`.  

**D**: *Come disabilito temporaneamente i vincoli FK in SQLite?*  
**R**:  
```sql
PRAGMA foreign_keys = OFF;  -- Disabilita
-- Operazioni...
PRAGMA foreign_keys = ON;   -- Riabilita
```

**D**: *Le FK sono obbligatorie?*  
**R**: No, ma sono fortemente consigliate per garantire l'integrità dei dati.  

---

Se hai un caso specifico da implementare, fammi sapere e ti aiuto a scrivere il codice! 🛠️
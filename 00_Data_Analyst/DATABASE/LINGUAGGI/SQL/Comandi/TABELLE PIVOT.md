In SQL, le **tabelle pivot** si creano tipicamente con l'operatore **`CASE WHEN`** (o `PIVOT` in alcuni database come SQL Server/PostgreSQL), non con `UNION` o `HAVING`.  

Ecco come realizzarle in SQLite (e altri database che non supportano direttamente `PIVOT`):

---

### **1. Tecnica base con `CASE WHEN` (per SQLite, MySQL, etc.)**  
**Esempio**: Contare quante persone hanno dato voti 4-5 a ogni cucina (trasponendo righe in colonne).  

```sql
SELECT 
    COUNT(*) AS totale_persone,
    SUM(CASE WHEN cucina_italiana BETWEEN 4 AND 5 THEN 1 ELSE 0 END) AS alta_preferenza_italiana,
    SUM(CASE WHEN cucina_cinese BETWEEN 4 AND 5 THEN 1 ELSE 0 END) AS alta_preferenza_cinese,
    SUM(CASE WHEN cucina_giapponese BETWEEN 4 AND 5 THEN 1 ELSE 0 END) AS alta_preferenza_giapponese
FROM 
    preferenze_alimentari_italia;
```

**Output**:  
```
| totale_persone | alta_preferenza_italiana | alta_preferenza_cinese | alta_preferenza_giapponese |
|----------------|--------------------------|------------------------|----------------------------|
| 300            | 150                      | 80                     | 45                         |
```

---

### **2. Alternativa con `GROUP BY` (per raggruppare dati)**  
**Esempio**: Contare persone per fascia d'età e genere (tabella incrociata).  

```sql
SELECT 
    CASE 
        WHEN eta < 20 THEN '<20'
        WHEN eta BETWEEN 20 AND 30 THEN '20-30'
        ELSE '30+'
    END AS fascia_eta,
    COUNT(CASE WHEN genere = 'Femmina' THEN 1 END) AS femmine,
    COUNT(CASE WHEN genere = 'Maschio' THEN 1 END) AS maschi
FROM 
    preferenze_alimentari_italia
GROUP BY 
    fascia_eta;
```

**Output**:  
```
| fascia_eta | femmine | maschi |
|------------|---------|--------|
| <20        | 25      | 30     |
| 20-30      | 60      | 55     |
| 30+        | 80      | 50     |
```

---

### **3. Differenze chiave con `UNION` e `HAVING`**  
- **`UNION`**: Combina risultati di query **verticalmente** (aggiunge righe), non serve per pivot.  
  ```sql
  -- Esempio NON pivot (solo unione di query)
  SELECT 'Italiana' AS cucina, COUNT(*) FROM preferenze WHERE cucina_italiana > 3
  UNION ALL
  SELECT 'Cinese', COUNT(*) FROM preferenze WHERE cucina_cinese > 3;
  ```

- **`HAVING`**: Filtra risultati **dopo** l'aggregazione, non ruota dati.  
  ```sql
  -- Esempio: Filtra solo fasce d'età con +50 femmine
  SELECT 
      fascia_eta, 
      COUNT(*) AS totale
  FROM ...
  GROUP BY fascia_eta
  HAVING COUNT(*) > 50;
  ```

---

### **4. Soluzione avanzata con `GROUP_CONCAT` (SQLite)**  
Per liste orizzontali (es. elencare tutte le città per regione):  
```sql
SELECT 
    regione_residenza,
    GROUP_CONCAT(DISTINCT citta_residenza, ', ') AS citta
FROM 
    preferenze_alimentari_italia
GROUP BY 
    regione_residenza;
```
**Output**:  
```
| regione_residenza | citta               |
|-------------------|---------------------|
| Lombardia         | Milano, Bergamo     |
| Toscana           | Firenze, Pisa       |
```

---

### **Quando usare `UNION` o `HAVING`?**  
- ✅ `UNION`: Per **stackare** risultati simili (es. report separati per anno).  
- ✅ `HAVING`: Per filtrare **dopo** un `GROUP BY` (es. "solo regioni con 100+ persone").  

---

### **Database con supporto nativo al `PIVOT`**  
In **SQL Server** o **PostgreSQL** (con estensioni):  
```sql
-- SQL Server
SELECT *
FROM (
    SELECT genere, citta_residenza 
    FROM preferenze_alimentari_italia
) AS src
PIVOT (
    COUNT(citta_residenza)
    FOR genere IN ([Femmina], [Maschio])
) AS pvt;
```

---

### **Esempio completo per la tua tabella**  
```sql
-- Pivot delle preferenze medie per regione
SELECT 
    regione_residenza,
    AVG(cucina_italiana) AS media_italiana,
    AVG(cucina_cinese) AS media_cinese,
    AVG(cucina_giapponese) AS media_giapponese
FROM 
    preferenze_alimentari_italia
GROUP BY 
    regione_residenza;
```

Se hai bisogno di un pivot specifico, fammi vedere la struttura dei dati e l'output desiderato! 😊
MODUL:
e' il resto della divisione
si usa per fare calcoli o per vedere se qu
per esempio
30 modulo 7 e' 2
il resto 
il modulo serve per capire se un numero e' pari

MODULO 100 prendi le ultime due cifre

Ecco una spiegazione completa degli **operatori in SQL** con esempi pratici e applicazioni in Data Analysis:

---

### **Tipi di Operatori SQL**
#### 1. **Operatori Aritmetici**
| Operatore | Descrizione | Esempio (in SELECT) |
|-----------|-------------|----------------------|
| `+` | Addizione | `SELECT prezzo + iva FROM prodotti` |
| `-` | Sottrazione | `SELECT quantità - scorta_min FROM magazzino` |
| `*` | Moltiplicazione | `SELECT unità * prezzo FROM ordini` |
| `/` | Divisione | `SELECT SUM(vendite) / COUNT(*) AS media` |
| `%` | Modulo (resto) | `SELECT id % 10 AS gruppo FROM clienti` |

**Esempio Reale**:
```sql
-- Calcola il margine percentuale
SELECT 
    prodotto,
    (prezzo_vendita - prezzo_costo) / prezzo_costo * 100 AS margine_percentuale
FROM prodotti;
```

#### 2. **Operatori di Confronto**
| Operatore | Descrizione | Esempio (in WHERE) |
|-----------|-------------|---------------------|
| `=` | Uguale | `WHERE stato = 'Italia'` |
| `<>` o `!=` | Diverso | `WHERE pagamento <> 'contanti'` |
| `>` | Maggiore | `WHERE quantità > 100` |
| `<` | Minore | `WHERE data < '2023-01-01'` |
| `>=` | Maggiore/Uguale | `WHERE sconto >= 10` |
| `<=` | Minore/Uguale | `WHERE rating <= 3` |
| `BETWEEN` | Intervallo | `WHERE prezzo BETWEEN 50 AND 100` |
| `LIKE` | Pattern matching | `WHERE nome LIKE 'Mar%'` |
| `IN` | Lista di valori | `WHERE città IN ('Roma','Milano')` |

**Esempio Avanzato**:
```sql
-- Filtra prodotti con scorta critica o prezzo alto
SELECT *
FROM prodotti
WHERE quantità < 20 OR prezzo > 500;
```

#### 3. **Operatori Logici**
| Operatore | Descrizione | Esempio |
|-----------|-------------|---------|
| `AND` | Entrambe vere | `WHERE stato = 'IT' AND importo > 1000` |
| `OR` | Almeno una vera | `WHERE pagato = 1 OR sconto > 0` |
| `NOT` | Negazione | `WHERE NOT città = 'Napoli'` |

**Caso d'Uso in Data Cleaning**:
```sql
-- Identifica record anomali
SELECT *
FROM vendite
WHERE (importo < 0 OR importo > 10000) AND data BETWEEN '2023-01-01' AND '2023-12-31';
```

#### 4. **Operatori per NULL**
| Operatore | Descrizione | Esempio |
|-----------|-------------|---------|
| `IS NULL` | Valore nullo | `WHERE telefono IS NULL` |
| `IS NOT NULL` | Valore non nullo | `WHERE email IS NOT NULL` |
| `COALESCE()` | Primo non-nullo | `SELECT COALESCE(telefono, 'N/D')` |

---

### **Operatori Speciali per Data Analysis**
#### 1. **Operatori di Aggregazione**
```sql
SELECT 
    regione,
    COUNT(*) AS totale_clienti,
    AVG(fatturato) AS media_fatturato,
    SUM(CASE WHEN rating > 3 THEN 1 ELSE 0 END) AS clienti_soddisfatti
FROM clienti
GROUP BY regione;
```

#### 2. **Operatori per Stringhe**
| Operatore/Funzione | Esempio |
|--------------------|---------|
| `||` (concatenazione) | `SELECT nome || ' ' || cognome AS nome_completo` |
| `SUBSTRING()` | `SUBSTRING(codice, 1, 3) AS prefisso` |
| `UPPER()`/`LOWER()` | `WHERE LOWER(città) = 'roma'` |

#### 3. **Operatori per Date**
```sql
-- Differenza tra date in giorni
SELECT data_ordine, data_consegna,
       julianday(data_consegna) - julianday(data_ordine) AS giorni_attesa
FROM ordini;
```

---

### **Errori Comuni in SQL**
❌ **Confondere `=` con `==`** (SQL usa solo `=`)  
❌ **Dimenticare che `NULL` richiede operatori speciali** (`WHERE colonna = NULL` è sbagliato!)  
❌ **Mischiare tipi di dati** (es: confrontare stringhe con numeri senza cast)  

**Esempio Problematico**:
```sql
-- SBAGLIATO: confronto tra stringa e numero
SELECT * FROM prodotti WHERE prezzo > '100';
-- CORRETTO
SELECT * FROM prodotti WHERE prezzo > 100;
```

---

### **Esercizio Pratico**
**Problema**: Trova i prodotti con:  
- Prezzo tra 50 e 150 euro  
- Quantità disponibile > 0  
- Categoria 'Elettronica' o 'Informatica'  
- Con recensioni nulle o rating >= 4  

**Soluzione**:
```sql
SELECT *
FROM prodotti
WHERE prezzo BETWEEN 50 AND 150
  AND quantità > 0
  AND categoria IN ('Elettronica', 'Informatica')
  AND (recension IS NULL OR rating >= 4);
```

Se hai bisogno di esempi specifici dal tuo materiale di studio, posso adattarli a casi concreti!
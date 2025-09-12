La funzione **`strftime()`** in SQLite è un potente strumento per formattare e manipolare date e orari. Ecco una spiegazione completa:

[[#COME CONVERTIRE LE DATE]]
### Sintassi base:
```sql
strftime(formato, timestring, [modifier1, modifier2, ...])
```

### Parametri principali:
1. **`formato`**: Stringa che specifica come formattare l'output
2. **`timestring`**: Data/ora di partenza (può essere una stringa o una data letterale)
3. **`modifier`** (opzionale): Modificatori per aggiustare la data (es: '+3 days')

### Formati più comuni:
| Codice | Significato       | Esempio |
|--------|-------------------|---------|
| `%Y`   | Anno a 4 cifre    | 2023    |
| `%m`   | Mese (01-12)      | 05      |
| `%d`   | Giorno (01-31)    | 15      |
| `%H`   | Ora (00-23)       | 14      |
| `%M`   | Minuti (00-59)    | 30      |
| `%S`   | Secondi (00-59)   | 45      |
| `%w`   | Giorno settimana (0-6, 0=domenica) | 3 |

### Esempi pratici:

1. **Data corrente formattata**:
   ```sql
   SELECT strftime('%d/%m/%Y', 'now');
   -- Output: "15/05/2023" (data di oggi)
   ```

2. **Estrazione anno da una data**:
   ```sql
   SELECT strftime('%Y', '1990-05-15');
   -- Output: "1990"
   ```

3. **Calcolare differenza tra date**:
   ```sql
   SELECT strftime('%Y', 'now') - strftime('%Y', '1990-05-15');
   -- Output: differenza in anni (età approssimativa)
   ```

4. **Aggiungere giorni a una data**:
   ```sql
   SELECT strftime('%Y-%m-%d', 'now', '+7 days');
   -- Data di oggi + 7 giorni
   ```

5. **Ultimo giorno del mese**:
   ```sql
   SELECT strftime('%Y-%m-%d', 'now', 'start of month', '+1 month', '-1 day');
   ```

### Nella tua query per calcolare l'età:
```sql
SELECT 
    strftime('%Y', 'now') - strftime('%Y', data_nascita) - 
    (strftime('%m-%d', 'now') < strftime('%m-%d', data_nascita)) AS eta
```
- `strftime('%Y', 'now') - strftime('%Y', data_nascita)` → Differenza grezza in anni
- `(strftime('%m-%d', 'now') < strftime('%m-%d', data_nascita))` → Vale 1 se il compleanno non è ancora arrivato nell'anno corrente (sottrae 1)

### Modificatori utili:
| Modificatore      | Effetto                     |
|-------------------|-----------------------------|
| `'start of month'`| Primo giorno del mese       |
| `'+N days'`       | Aggiunge N giorni           |
| `'-N years'`      | Sottrae N anni              |
| `'weekday N'`     | Prossimo giorno settimana N |

### Esempio complesso:
```sql
SELECT strftime('%A %d %B %Y', 'now', 'start of month', '+5 days');
-- "Friday 05 May 2023" (il 5 del mese corrente)
```

**Importante**: SQLite interpreta le date in formato `'YYYY-MM-DD'` come valide. Per altri formati devi prima convertirle.

## COME CONVERTIRE LE DATE

In SQLite, per convertire date da altri formati al formato standard `'YYYY-MM-DD'` (necessario per i calcoli corretti), puoi usare la funzione `substr()` per estrarre le parti della data e ricomporle. Ecco come fare per i formati più comuni:

### 1. Conversione da `'DD/MM/YYYY'` (es. "15/05/1990")
```sql
SELECT 
    data_nascita AS originale,
    substr(data_nascita, 7, 4) || '-' ||  -- Anno (posizioni 7-10)
    substr(data_nascita, 4, 2) || '-' ||  -- Mese (posizioni 4-5)
    substr(data_nascita, 1, 2) AS data_convertita  -- Giorno (posizioni 1-2)
FROM preferenze_alimentari_italia;
```

### 2. Conversione da `'DD-MM-YYYY'` (es. "15-05-1990")
```sql
SELECT 
    data_nascita AS originale,
    substr(data_nascita, 7, 4) || '-' ||  -- Anno
    substr(data_nascita, 4, 2) || '-' ||  -- Mese
    substr(data_nascita, 1, 2) AS data_convertita  -- Giorno
FROM preferenze_alimentari_italia;
```

### 3. Conversione da `'MM/DD/YYYY'` (es. "05/15/1990")
```sql
SELECT 
    data_nascita AS originale,
    substr(data_nascita, 7, 4) || '-' ||  -- Anno
    substr(data_nascita, 1, 2) || '-' ||  -- Mese
    substr(data_nascita, 4, 2) AS data_convertita  -- Giorno
FROM preferenze_alimentari_italia;
```

### 4. Per aggiornare permanentemente la colonna (se necessario)
```sql
-- Prima aggiungi una colonna temporanea
ALTER TABLE preferenze_alimentari_italia ADD COLUMN data_nascita_std TEXT;

-- Poi popolala con le date convertite
UPDATE preferenze_alimentari_italia
SET data_nascita_std = substr(data_nascita, 7, 4) || '-' || 
                       substr(data_nascita, 4, 2) || '-' || 
                       substr(data_nascita, 1, 2);

-- Opzionale: rinomina e elimina la vecchia colonna
ALTER TABLE preferenze_alimentari_italia RENAME COLUMN data_nascita TO data_nascita_old;
ALTER TABLE preferenze_alimentari_italia RENAME COLUMN data_nascita_std TO data_nascita;
```

### 5. Funzioni complete per la conversione
Crea queste funzioni personalizzate se lavori spesso con conversioni:

```sql
-- Per formato DD/MM/YYYY
CREATE FUNCTION convert_dmy(date_text TEXT) RETURNS TEXT AS
BEGIN
    RETURN substr(date_text, 7, 4) || '-' || 
           substr(date_text, 4, 2) || '-' || 
           substr(date_text, 1, 2);
END;

-- Uso:
SELECT convert_dmy('15/05/1990');  -- Restituisce '1990-05-15'
```

### 6. Verifica delle conversioni
Prima di aggiornamenti massivi, controlla sempre un campione:
```sql
SELECT 
    data_nascita, 
    substr(data_nascita, 7, 4) || '-' || 
    substr(data_nascita, 4, 2) || '-' || 
    substr(data_nascita, 1, 2) AS data_convertita
FROM preferenze_alimentari_italia
LIMIT 10;
```

### Importante:
- Le posizioni in `substr()` partono da 1 (non da 0)
- Per dati inconsistenti, aggiungi un controllo preliminare:
  ```sql
  WHERE data_nascita LIKE '__/__/____'  -- Verifica il formato
  ```
- Usa `TRIM()` se ci sono spazi bianchi: `TRIM(substr(...))`

Facciamo chiarezza con esempi pratici:

### 1. Le posizioni in `substr()` partono da 1 (non da 0)
In SQLite, la funzione `substr(stringa, inizio, lunghezza)` usa indici che iniziano da **1** (non da 0 come in molti linguaggi di programmazione).

Esempio con `'15/05/1990'`:
```
Posizione: 1 2 3 4 5 6 7 8 9 10
Carattere: 1 5 / 0 5 / 1 9 9 0
```

Per estrarre:
- Giorno (15): `substr(data_nascita, 1, 2)`
- Mese (05): `substr(data_nascita, 4, 2)`
- Anno (1990): `substr(data_nascita, 7, 4)`

### 2. Controllo preliminare del formato
La condizione `WHERE data_nascita LIKE '__/__/____'` verifica che:
- Ci siano esattamente 2 caratteri (`__`), poi /
- Altri 2 caratteri (`__`), poi /
- Infine 4 caratteri (`____`)

Esempi:
- `'15/05/1990'` → ✅ Valido
- `'5/5/90'` → ❌ Non valido
- `'15-05-1990'` → ❌ Non valido

### 3. Gestione spazi bianchi con `TRIM()`
Se le date potrebbero avere spazi (es. `' 15/05/1990 '`):
```sql
SELECT 
    TRIM(substr(data_nascita, 1, 2)) || '-' || 
    TRIM(substr(data_nascita, 4, 2)) || '-' || 
    TRIM(substr(data_nascita, 7, 4)) AS data_convertita
```

### Query completa con tutti i controlli
```sql
SELECT 
    data_nascita AS originale,
    CASE 
        WHEN data_nascita LIKE '__/__/____' THEN
            substr(TRIM(data_nascita), 7, 4) || '-' || 
            substr(TRIM(data_nascita), 4, 2) || '-' || 
            substr(TRIM(data_nascita), 1, 2)
        ELSE NULL
    END AS data_convertita
FROM preferenze_alimentari_italia
WHERE data_nascita LIKE '__/__/____';  -- Filtra solo i formati validi
```

### Esempio pratico con errori gestiti
```sql
WITH dati_puliti AS (
    SELECT 
        id,
        TRIM(data_nascita) AS data_pulita
    FROM preferenze_alimentari_italia
    WHERE data_nascita LIKE '__/__/____'
)
SELECT 
    id,
    data_pulita AS originale,
    substr(data_pulita, 7, 4) || '-' || 
    substr(data_pulita, 4, 2) || '-' || 
    substr(data_pulita, 1, 2) AS data_convertita
FROM dati_puliti;
```

Questo approccio:
1. Prima pulisce gli spazi con `TRIM`
2. Poi filtra solo i formatti validi
3. Infine converte in formato standard


Ecco una spiegazione dettagliata di come funziona `strftime()` e perché l'ordine anno-mese-giorno è cruciale in SQLite:

## Come funziona `strftime()`

`strftime()` è la funzione principale in SQLite per formattare date e tempi. La sintassi è:

```sql
strftime(formato, data_stringa)
```

Dove:
- `formato`: Specifica come visualizzare la data (es: `'%Y'` per l'anno)
- `data_stringa`: La data da formattare (o `'now'` per la data corrente)

### Formati principali:
| Codice | Significato         | Esempio |
|--------|---------------------|---------|
| `%Y`   | Anno a 4 cifre      | 2023    |
| `%m`   | Mese (01-12)        | 05      |
| `%d`   | Giorno del mese (01-31)| 15   |

---

## Perché usare anno-mese-giorno nel calcolo

L'operazione `strftime('%m-%d', data)` estrae **solo mese e giorno**, permettendo di confrontare le date senza considerare l'anno. Questo è essenziale per determinare se il compleanno è già passato nell'anno corrente.

### Esempio con data di nascita 15/05/1990:
1. **Calcolo anni grezzo**:
   ```sql
   strftime('%Y', 'now') - strftime('%Y', '1990-05-15') → 2023 - 1990 = 33
   ```
   (Ma se oggi fosse 10/05/2023, la persona non ha ancora compiuto 33 anni!)

2. **Correzione per il compleanno**:
   ```sql
   strftime('%m-%d', 'now') < strftime('%m-%d', '1990-05-15') → '05-10' < '05-15' → vero (1)
   ```
   - Se oggi è prima del compleanno, sottrai 1 anno

3. **Risultato finale**:
   ```sql
   33 (anni grezzi) - 1 (correzione) = 32 anni
   ```

---

## Esempio completo passo-passo

Per una data di nascita "15/05/1990" e oggi "10/05/2023":

1. Converti in formato SQLite:
   ```sql
   substr('15/05/1990', 7,4) || '-' || substr('15/05/1990', 4,2) || '-' || substr('15/05/1990', 1,2)
   → '1990-05-15'
   ```

2. Calcola anni grezzi:
   ```sql
   strftime('%Y', 'now') - strftime('%Y', '1990-05-15') → 2023 - 1990 = 33
   ```

3. Verifica se il compleanno è passato:
   ```sql
   strftime('%m-%d', 'now') < strftime('%m-%d', '1990-05-15') → '05-10' < '05-15' → 1 (vero)
   ```

4. Calcolo finale:
   ```sql
   33 - 1 = 32 anni
   ```

---

## Perché questo ordine è importante?

1. **SQLite confronta le date come stringhe**:  
   `'05-10' < '05-15'` è un confronto lessicografico valido solo con mese-giorno in questo ordine.

2. **Se inverti giorno-mese**:
   ```sql
   strftime('%d-%m', '1990-05-15') → '15-05'
   strftime('%d-%m', 'now') → '10-05'
   '10-05' < '15-05' → corretto
   ```
   Ma con valori come `'05-15'` (15 maggio) vs `'10-05'` (5 ottobre) darebbe risultati sbagliati:
   ```sql
   '10-05' < '05-15' → falso (errato!)
   ```

---

## Alternative per altri formati di data

Se la tua data è in formato **'YYYY-MM-DD'**, puoi semplificare:
```sql
strftime('%Y', 'now') - strftime('%Y', data_nascita) - 
(strftime('%m-%d', 'now') < strftime('%m-%d', data_nascita))
```

Se hai bisogno di gestire altri formati o casi particolari, fammelo sapere!
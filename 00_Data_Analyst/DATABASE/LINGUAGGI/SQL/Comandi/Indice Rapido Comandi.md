Qui sotto trovi i comandi fondamentali di SQLite. Clicca su ogni link per vedere la sintassi dettagliata e un esempio pratico.

- [[#CREATE TABLE]]: Crea una nuova tabella nel database.
- [[#INSERT INTO]]: Aggiunge nuove righe (record) a una tabella.
- [[#SELECT]]: Estrae dati da una o più tabelle. È il comando più usato.
- [[#WHERE]]: Filtra i record, restituendo solo quelli che soddisfano una condizione specifica.
- [[#UPDATE]]: Modifica i record esistenti in una tabella.
- [[#DELETE]]: Rimuove i record da una tabella.
- [[#ORDER BY]]: Ordina i risultati in modo ascendente o discendente.
- [[#GROUP BY]]: Raggruppa le righe che hanno gli stessi valori in colonne specificate, utile con funzioni di aggregazione (`COUNT`, `SUM`, `AVG`, etc.).
- [[#LIMIT]]: Limita il numero di righe restituite dalla query.
- [[#JOIN]]: Combina righe da due o più tabelle basandosi su una colonna correlata.

## Dettagli ed Esempi

Per tutti gli esempi, immagineremo di avere una tabella chiamata `Libri`.

### CREATE TABLE

```sql

CREATE TABLE nome_tabella (
    colonna1 tipo_dato,
    colonna2 tipo_dato,
    ...
);```

Questo comando definisce la struttura di una nuova tabella, specificando i nomi delle colonne e i tipi di dati che conterranno.

**Esempio Pratico:** Creiamo una tabella per catalogare dei libri.


```sql

CREATE TABLE Libri (
    ID INTEGER PRIMARY KEY AUTOINCREMENT,
    Titolo TEXT NOT NULL,
    Autore TEXT NOT NULL,
    AnnoPubblicazione INTEGER,
    Genere TEXT
);
```

**A cosa serve:** Crea una tabella `Libri` con 5 colonne. `ID` è la chiave primaria che si auto-incrementa, `Titolo` e `Autore` sono testi che non possono essere vuoti (`NOT NULL`).

### INSERT INTO

Usa questo comando per popolare la tabella con i dati.

**Sintassi:**

```sql
INSERT INTO nome_tabella (colonna1, colonna2, colonna3)
VALUES (valore1, valore2, valore3);
```


**Sintassi:**



[[SELECT]]

```sql 
SELECT colonna1, colonna2 
FROM tabella
WHERE condizione;
```

**Esempio**

```sql
SELECT nome, eta FROM clienti WHERE eta > 30;
```

[[Esempi SELECT|▶️ Altri esempi]] 

[[WHERE]]

```sql
SELECT * FROM tabella 
WHERE colonna = valore 
AND/OR altra_condizione;
```

**Esempio**:

```sql
SELECT * FROM prodotti 
WHERE prezzo > 100 AND stock > 0;
```

[[JOIN]]

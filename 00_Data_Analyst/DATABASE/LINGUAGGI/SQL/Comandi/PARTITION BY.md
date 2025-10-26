Caso comune:
suddividere anno mese e anno 

ordinando i dati per artista

fa una cosa simile ad una group by
ma 

> **`PARTITION BY`** divide le righe della tabella in gruppi (o "finestre") e la funzione analitica (come `ROW_NUMBER()`, `RANK()`, `AVG()`, `SUM()`) viene calcolata **indipendentemente** all'interno di ciascun gruppo, **senza collassare le righe** come farebbe un `GROUP BY`.

---

Appunti Obsidian: Capire `PARTITION BY`

### 1. Window Function

Una funzione finestra opera su un insieme di righe correlate tra loro (la "finestra") e produce un risultato per ciascuna riga della finestra.

| Funzione Analitica | Descrizione                                                                                                          |
| ------------------ | -------------------------------------------------------------------------------------------------------------------- |
| **`OVER()`**       | La clausola **obbligatoria** che definisce la finestra (il set di righe).                                            |
| **`PARTITION BY`** | **Divide** le righe in gruppi, e la funzione riparte da zero per ogni gruppo.                                        |
| **`ORDER BY`**     | **Ordina** le righe all'interno di ciascun gruppo. Cruciale per funzioni di ranking (`RANK()`) o cumulate (`SUM()`). |

### 2. Differenza Cruciale: `GROUP BY` vs. `PARTITION BY`

|Caratteristica|`GROUP BY`|`PARTITION BY`|
|---|---|---|
|**Righe nel Risultato**|Collassa (riduce) le righe. Una riga per ogni gruppo.|Mantiene **tutte** le righe della tabella originale.|
|**Scopo**|Aggregazione (calcola una singola statistica per il gruppo).|Analisi (calcola una statistica **per riga** basata sul gruppo).|

### 3. Esempio con Chinook: Vendite Mensili per Artista

Immaginiamo di voler confrontare le vendite totali di un album rispetto alla media delle vendite degli album di quello stesso artista. Dobbiamo calcolare la **vendita media per artista**.

#### 🎯 Obiettivo:

Calcolare la **media** delle vendite totali per ogni **Artista** (della colonna `Name` della tabella `Artist`) e visualizzare tale media **accanto** ad ogni singola traccia venduta.

#### 📝 Query SQL (PostgreSQL):

SQL

```
SELECT
    T.Name AS NomeTraccia,
    A.Name AS NomeArtista,
    I.InvoiceId,
    I.Quantity,
    
    -- Calcola la somma delle quantità vendute per ogni Artista
    SUM(I.Quantity) OVER (PARTITION BY A.ArtistId) AS TotaleVendutoArtista
    
FROM InvoiceLine AS I
JOIN Track AS T ON I.TrackId = T.TrackId
JOIN Album AS AL ON T.AlbumId = AL.AlbumId
JOIN Artist AS A ON AL.ArtistId = A.ArtistId
ORDER BY A.Name, T.Name, I.InvoiceId;
```

#### 🧠 Spiegazione del `PARTITION BY`

1. **Funzione Finestra:** Usiamo la funzione di aggregazione `SUM(I.Quantity)`.
    
2. **Definizione della Finestra:** La clausola `OVER (PARTITION BY A.ArtistId)` dice a PostgreSQL:
    
    - **"Prima di calcolare la somma, raggruppa tutte le righe che hanno lo stesso `ArtistId`."**
        
    - La somma (TotaleVendutoArtista) verrà calcolata **solo** per quel gruppo (quell'artista).
        
3. **Risultato:** Il valore di `TotaleVendutoArtista` sarà **identico** per tutte le righe associate allo stesso artista, indipendentemente dalla traccia o dalla fattura. La riga singola (e i suoi dettagli) viene mantenuta.
    

### 4. Esempio Più Comune: Classifiche (Ranking) 

Il caso d'uso più comune è la creazione di classifiche (`RANK()`, `ROW_NUMBER()`). Vogliamo classificare le tracce **all'interno di ciascun album**, non in tutta la libreria.

SQL

```
SELECT
    AL.Title AS Album,
    T.Name AS Traccia,
    T.TrackId,
    
    -- Assegna un numero di riga unico per ogni traccia,
    -- ripartendo da 1 per ogni nuovo album.
    ROW_NUMBER() OVER (PARTITION BY AL.AlbumId ORDER BY T.Name) AS NumeroTracciaAlbum
    
FROM Track AS T
JOIN Album AS AL ON T.AlbumId = AL.AlbumId
WHERE AL.AlbumId IN (1, 2) -- Limite per chiarezza
ORDER BY AL.Title, NumeroTracciaAlbum;
```

#### 🧠 Spiegazione

- `PARTITION BY AL.AlbumId`: Le righe sono raggruppate per album.
    
- `ORDER BY T.Name`: All'interno di ciascun album, le tracce vengono ordinate per nome.
    
- `ROW_NUMBER()`: La numerazione inizia da **1** per il primo album, arriva a `N`, e poi **ricomincia da 1** per il secondo album.

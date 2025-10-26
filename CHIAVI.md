
in uno star scheme
## 1. Chiave Primaria (PK) e Chiave Foreign (FK)

Queste sono regole di database management, non tipi di dati: definiscono la **relazione** tra le tabelle.

| Tipo di Chiave           | Dove si Trova                                               | Ruolo                                                                                                                                                  |
| ------------------------ | ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Chiave Primaria (PK)** | **Tabella di Dimensione** (es. `ids_atto` in `DIM_ATTO`)    | **Identificatore univoco** per ogni riga della tabella. Garantisce che non ci siano duplicati in quella tabella.                                       |
| **Chiave Foreign (FK)**  | **Tabella dei Fatti** (es. `ids_atto` in `FATTO_INCARICHI`) | Un **puntatore** che collega una riga della Tabella dei Fatti alla riga corrispondente nella Tabella di Dimensione. Rinforza l'integrità referenziale. |

**Nel modello:** La `ids_atto` è la **PK** nella `DIM_ATTO` e la **FK** nella tua futura Tabella dei Fatti. Non e' necessario comunque farla effettivamente la PK in questo caso, in analitics non servono in quanto non aggiungiamo righe.

---
## 2. Chiave Naturale

La chiave naturale è l'identificatore di un'entità **derivato dai dati di origine**.

|Caratteristica|Ruolo|Esempio nel tuo caso|
|---|---|---|
|**Definizione**|Uno o più attributi che identificano in modo univoco un'entità nel mondo reale o nei dati sorgente.|La combinazione di **`numero_pg_atto`** e **`anno_pg_atto`** per un atto. Oppure `ragione_sociale` + `codice_fiscale` per un soggetto.|
|**Problema nel DWH**|Non sono univoche tra sorgenti diverse (es. `id` di un atto) o sono lunghe, testuali e complesse da usare per i join.|**Duplicati:** Se due sistemi sorgente usano lo stesso ID naturale, creano duplicati.|

**Il tuo problema:** Quando hai unito le strutture per la `DIM_STRUTTURA`, la chiave naturale (il nome della struttura) era duplicata tra le due sorgenti.

---

## 3. Chiave Surrogata (Surrogate Key)

La chiave surrogata è la **soluzione** ai problemi della chiave naturale. È una chiave artificiale, creata dal processo ETL.

| Caratteristica  | Soluzione al Problema                                                                                                                                                                                                                 | Esempio nel tuo caso                                                                                                                            |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Definizione** | Un semplice numero intero (generalmente sequenziale) senza alcun significato per l'utente, creato e gestito dal database.                                                                                                             | **`ids_atto`**, **`ids_struttura`**, **`-1`** (il fittizio).                                                                                    |
| **Benefici**    | **Univocità Assoluta:** Puoi creare una riga anagrafica univoca anche se la chiave naturale non lo è. **Efficienza:** I join sono più veloci perché si basano su numeri interi semplici (che è il ruolo della **PK** e della **FK**). | **`ids_atto`** risolve il problema dei duplicati creato dalla `UNION ALL`. **L'ID `-1`** risolve il problema dei valori `NULL` (dati mancanti). |

### La Relazione Finale (La risposta alla tua domanda)

**Il tuo processo ETL:**

1. Prendi le **Chiavi Naturali** (es., nome struttura).
    
2. Le pulisci e le raggruppi per risolvere i problemi di duplicazione.
    
3. Assegni a ciascun gruppo univoco una **Chiave Surrogata** (es., `ids_struttura = 1, 2, 3...`) se c'e' bisogno
    
4. La Chiave Surrogata diventa la **Chiave Primaria (PK)** della tua dimensione.
    
5. Questa Chiave Surrogata viene copiata nella Tabella dei Fatti, dove agisce come **Chiave Foreign (FK)**.

come si crea?


|   |
|---|
|`SELECT`<br><br>  `ROW_NUMBER() OVER (...)` `as` `athlete_num,`<br><br>  `...`<br><br>`FROM` `athletes;`|

The `OVER()` clause has two optional subclauses: `PARTITION BY` and `ORDER BY`. We will show examples using several different `OVER()` clauses.

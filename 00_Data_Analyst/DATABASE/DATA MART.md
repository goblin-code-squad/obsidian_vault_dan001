1. [[Fact Table]] (tabella con tutte le misure)
2. [[Dimensioni]] organizzate in gerarchie
3. [[Mapping o Transcodifica]]
4. 

---

attenzione: in import ricordarsi in integration di correggere le minuscole e gli spazi

attenzione al double counting che senza group by non si possono evitare

non costruire anagrafiche per valori NULL o string vuote ( ' ' ) perche a volte non funziona il distinct (si puo' usare anche left join)

tagliare anagrafiche inutili
("in" sul fatto)

esemepio

dim_paese = { (1, 'ITA'), (2, 'FRA'), (3, 'GER'), (4, 'SPA'), (-1, 'fittizio') }

fact_vendite = {(1, 10), (2, 4), (3, 56), (-1, 2)}

cioe 
```sql 
create table dim_paese as
select * from integration.it_dim_paese
where id_paese 
IN
(select id_paese from fact_vendite)
```


---
##  Concetti Chiave e Fasi del Data Warehouse (DW)

### Data Mart

- **Definizione/Esempio:** Hai menzionato un esempio di **[[DATA MART]]** relativo alla soluzione di un assignment della Week 12.
    
    - _(Nota: un Data Mart è una versione ridotta di un Data Warehouse, focalizzata su un'area aziendale specifica, come "Vendite" o "Marketing")._
        

---

## 🗺️ Fasi di Caricamento e Preparazione Dati

Gli appunti descrivono le fasi tipiche di un processo **ETL/ELT** (Extract, Transform, Load) o di un'architettura di dati.

### 1. Landing (Area di Atterraggio/Staging)

- **Scopo:** Ricevere i dati grezzi estratti dalle fonti sorgente.
    
- **Regole di Trasformazione (Minime):**
    
    - Le colonne vengono lasciate **più o meno uguali** rispetto alla sorgente.
        
    - Si eseguono **miglioramenti basilari** come la rimozione di spazi superflui.
        
    - **Non si deve fare il renaming** (rinomina delle colonne) in questa fase.
        

---

### 2. Integration (Area di Integrazione/Trasformazione)

Questa fase è cruciale per la pulizia, l'uniformità e l'arricchimento dei dati, prima che questi passino al Data Mart o al Data Warehouse finale.

#### 🎯 Tappe da Eseguire

1. **Data Tagging:** (Da fare **prima possibile**).
    
    - Consiste nell'**aggiungere delle colonne** (o tag/etichette) che servono per arricchire i dati (ad esempio, aggiungendo informazioni di classificazione o metadati).
        
2. **Renaming:** Eseguire la rinomina delle colonne per adottare una **convenzione di naming standardizzata** a livello aziendale.

nelle naming convention IT_table non e' uguale alle originali perche' magari ho o tolto delle colonne

ATTENZIONE: il fittizio e' l'unico caso in cui si usa INSERT

nella dimensione ci deve essere un solo elemento per

#### 🗑️ Regole di Scarto/Filtro

- **Esempio di Scarto:** "Perché scartare quelli con **importo null**? Perché qui la cosa importante era appunto l'importo."
    
    - _Spiegazione:_ Se una metrica cruciale (come l'importo) è necessaria per l'analisi (ad esempio, per popolare il Data Mart), le righe in cui tale metrica è mancante (`NULL`) devono essere scartate per garantire l'integrità del processo di analisi.
        


Hai sollevato il punto cruciale! Il problema del **double counting** (doppio conteggio) è causato dalla duplicazione dei dati durante le JOIN tra tabelle con relazioni uno-a-molti o molti-a-molti.

Per evitarlo, devi assicurarti che ogni riga della tabella dei Fatti venga conteggiata **una sola volta** quando si eseguono aggregazioni.

Ecco le tre strategie principali per prevenire il double counting, sia a livello di modellazione del Data Warehouse che a livello di query SQL.

---

## 🏗️ 1. Soluzioni a Livello di Modellazione (Prevenzione)

La causa principale del doppio conteggio è la struttura del tuo Data Warehouse. Devi isolare le relazioni molti-a-molti o gestirle con tabelle ponte.

### A. Rimuovere le Relazioni Molti-a-Molti (M:N)

Se hai una tabella dimensionale (come la nostra `Prodotto_Categoria`) che può avere più righe per una singola chiave della tabella dei Fatti (`Prodotto_ID`), stai introducendo il rischio di duplicazione.

- **Soluzione:** Spesso, la metrica soggetta a doppio conteggio (come l'Importo Venduto) deve rimanere **solo** nella tabella dei Fatti. Le metriche che sono intrinsecamente legate a una Dimensione (ad esempio, il costo di un prodotto o il budget di una categoria) dovrebbero essere mantenute nella Dimensione.
    

### B. Creare Viste (Views) o Tabelle a Grana Singola

Se devi comunque unire la Tabella dei Fatti con una dimensione "molti", assicurati di utilizzare una vista o una tabella che aggrega quella dimensione **al livello di dettaglio della Fatto**.

- Ad esempio, invece di unire la `Vendite` (grana: riga di transazione) con la `Prodotto_Categoria` (grana: prodotto-categoria), potresti:
    
    1. Creare una **Vista A** con i dati delle vendite (`Vendita_ID`, `Importo`, ecc.).
        
    2. Creare una **Vista B** che riassume solo le informazioni che ti servono dalla dimensione, al livello di **`Prodotto_ID` unico**, prima di unirla.
        

---

## 🔍 2. Soluzioni a Livello di Query SQL (Correzione)

Quando la struttura non può essere modificata o la query deve toccare più tabelle, si usano funzioni SQL specifiche.

### A. Utilizzare `COUNT(DISTINCT...)` per i Conteggi

Quando devi contare gli elementi (ad esempio, il numero di transazioni, il numero di clienti unici), devi sempre usare `DISTINCT` sulla chiave unica della tabella dei Fatti.

|Aggregazione Errata (Double Counting)|Aggregazione Corretta|
|---|---|
|`COUNT(V.Vendita_ID)`|**`COUNT(DISTINCT V.Vendita_ID)`**|
|`COUNT(PC.Categoria)`|**`COUNT(DISTINCT PC.Categoria)`**|

### B. Utilizzare una Funzione Analitica

Nei database moderni, le **Funzioni Analitiche (o Window Functions)** come `ROW_NUMBER()` o `SUM() OVER(...)` sono il modo più potente per gestire i totali senza duplicare le righe.

**Esempio per il calcolo del Totale Venduto (corretto) senza duplicazione:**

1. Identifica una riga unica per ogni record della Tabella dei Fatti che stai per aggregare.
    
2. Somma l'Importo **solo per quella riga unica**.
    

SQL

```
SELECT
    SUM(CASE
        -- Assegna il valore 1 solo alla prima riga unica di Vendita_ID trovata in un raggruppamento
        WHEN ROW_NUMBER() OVER (PARTITION BY V.Vendita_ID ORDER BY PC.Categoria) = 1
        THEN V.Importo
        ELSE 0
    END) AS Totale_Venduto_Corretto
FROM
    Vendite V
JOIN
    Prodotto_Categoria PC ON V.Prodotto_ID = PC.Prodotto_ID;
```

Questa tecnica somma l'importo **una sola volta** per ogni `Vendita_ID`, anche se la `JOIN` ha creato quattro righe (come nell'esempio precedente).

---

## 📏 3. Regola del Grano (Granularity Rule)

Come regola generale, quando esegui una JOIN per un'analisi, chiediti sempre:

> **"Qual è la _grana_ (livello di dettaglio) della mia Tabella dei Fatti?"**

- Se la grana è **riga di transazione** (`Vendita_ID`), devi aggregare i tuoi risultati o le tue JOIN a quel livello, altrimenti stai sommando $50.00 (Importo) per due Categorie, e quindi stai contando $100.00 di vendite.
    

In sintesi: **usa `COUNT(DISTINCT...)`** e **le funzioni analitiche** per le correzioni immediate, ma **modella con attenzione** per prevenire il problema alla radice!


per [[anagrafica]] : devo scartare NULL e vuoti, li associo poi all'anagrafica col fittizio

quando creo anagrafica
select...
where colonna is not null and colonna_key  <> ' '

significa
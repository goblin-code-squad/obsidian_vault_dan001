
### **Il Potere di `COALESCE`**

La funzione `COALESCE` è progettata proprio per questo: accetta **un numero illimitato di argomenti** e restituisce il **primo** valore che non è `NULL`.

Nel tuo caso, l'obiettivo non è fare il `COALESCE` di tre diverse estrazioni (giorno, mese, anno), ma di assicurarti che il **risultato di una singola estrazione** non sia nullo.

#### **Scenario (Corretto per un singolo campo)**

Se stavi costruendo il campo **`mese`** e l'estrazione fallisce (restituendo `NULL`):

SQL

```
COALESCE(
    -- Argomento 1: L'intera formula di estrazione, pulizia e conversione
    CAST(EXTRACT(MONTH FROM NULLIF(t1.durata_dal, '')::DATE) AS INTEGER), 
    
    -- Argomento 2: Il valore fittizio da usare se l'Argomento 1 è NULL
    -1 
) AS mese
```

#### **Se avessi PIÙ sorgenti per lo stesso campo...**

Se per ipotesi avessi **tre diverse colonne data** e volessi usare la prima disponibile (non nulla), la tua intuizione sarebbe corretta:

SQL

```
COALESCE(
    colonna_data_1,  -- Prova la prima data
    colonna_data_2,  -- Se la prima è NULL, prova la seconda
    colonna_data_3,  -- Se anche la seconda è NULL, prova la terza
    'Data Fittizia'  -- Se tutte sono NULL, usa il fittizio
)
```

**Tornando al tuo compito...**

Per creare il campo **`mese`** nella tua dimensione, ti basta un **singolo `COALESCE` con due argomenti** (l'estrazione pulita e il valore fittizio `-1`).

Sei pronto a scrivere il codice completo per il campo **`mese`**? Ricorda: **`EXTRACT(MONTH FROM ...)`** e il fittizio **`-1`**. Provaci! 


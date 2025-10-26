CASE WHEN

SELECT * CASE WHEN
MODUL=0 THEN 
ELSE result
SELECT 


select case

when 'a'='b' then 'vero'

when 'a'='A' then 'case insensitive'

else 'case sensitive'

end;


qui per esempio e' vero quindi blocca a vero


`END AS` non è un comando SQL completo, ma rappresenta la **chiusura** e l'**assegnazione di un alias** a una **espressione condizionale** chiamata `CASE`.

In pratica, `END AS` viene utilizzato per dare un nome (un alias) alla colonna che risulta dall'applicazione della logica condizionale `CASE`.

---

##  Il Ruolo di `END AS` e l'Espressione `CASE`

L'espressione `CASE` è usata per eseguire una logica **"se-allora-altrimenti" (if-then-else)** e restituire un valore in base alle condizioni specificate.

La sua sintassi standard è:

SQL

```
CASE
    WHEN condizione_1 THEN risultato_1
    WHEN condizione_2 THEN risultato_2
    -- ... altre condizioni ...
    ELSE risultato_default  -- Opzionale, se nessuna condizione è vera
END
AS Nome_Nuova_Colonna  -- <--- Ecco dove si usa END AS
```

### Cosa fa esattamente `END AS`

1. **`END`:** Indica al database che la definizione logica della clausola `CASE` è terminata.
    
2. **`AS Nome_Nuova_Colonna`:** Assegna un nome descrittivo al **risultato** di tutta la logica `CASE` (il valore che hai definito con `THEN` o `ELSE`).
    

### Esempio Pratico

Supponiamo tu voglia classificare i prodotti in base al prezzo.

SQL

```
SELECT
    NomeProdotto,
    Prezzo,
    CASE
        WHEN Prezzo >= 100 THEN 'Alto'
        WHEN Prezzo >= 50 THEN 'Medio'
        ELSE 'Basso'
    END AS Fascia_Prezzo  -- <--- Il risultato della logica CASE viene chiamato 'Fascia_Prezzo'
FROM
    Prodotti;
```

**Risultato:** Viene creata una nuova colonna chiamata **`Fascia_Prezzo`** che contiene i valori 'Alto', 'Medio' o 'Basso'.
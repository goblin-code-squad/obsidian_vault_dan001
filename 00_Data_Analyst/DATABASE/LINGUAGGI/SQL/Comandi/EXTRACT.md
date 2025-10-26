
---

## 📝 Appunti SQL per la Dimensione Tempo (PostgreSQL)

### **Obiettivo: Estrazione e Pulizia di un Componente Temporale (Giorno)**

Quando usi `EXTRACT` in PostgreSQL, il risultato è spesso di tipo `DOUBLE PRECISION` (numeri con la virgola, es. `10.0`). Per la Dimensione Tempo, abbiamo bisogno di un **numero intero** (`INTEGER`).

#### **Query Esempio (Estrae il giorno come Intero)**

SQL

```
SELECT
    -- 1. Pulizia e Conversione a DATE:
    --    Gestisce stringhe vuote ('') e le converte in un tipo DATE gestibile.
    NULLIF(data_sorgente, '')::DATE AS data_pulita,

    -- 2. Estrazione e Casting:
    --    Estrae il numero del giorno (es. 10.0) e lo converte in INTEGER (es. 10).
    CAST(
        EXTRACT(DAY FROM NULLIF(data_sorgente, '')::DATE) 
    AS INTEGER) AS giorno_intero_pulito

FROM
    (VALUES 
        ('2025-10-10'), 
        ('2025-11-25'), 
        (''),             -- Esempio di dato sporco (stringa vuota)
        (NULL)            -- Esempio di NULL
    ) AS tmp(data_sorgente);
```

#### **Funzioni e Tipi di Dato Chiave**

|Funzione / Operatore|Scopo|Note|
|---|---|---|
|**`NULLIF(x, '')`**|Sostituisce la stringa vuota `''` con `NULL`.|Essenziale per la pulizia dei dati (data cleansing).|
|**`::DATE`**|Operatore di _Type Casting_, converte una stringa valida in tipo `DATE`.|Necessario prima di usare `EXTRACT` o `TO_CHAR`.|
|**`EXTRACT(DAY FROM ...)`**|Estrae la componente temporale (Giorno, Mese, Anno) da un tipo `DATE`.|Restituisce un tipo numerico con virgola (`DOUBLE PRECISION`).|
|**`CAST(... AS INTEGER)`**|Converte il risultato di `EXTRACT` in un numero intero.|Elimina la virgola finale (es. `10.0` diventa `10`).|

---


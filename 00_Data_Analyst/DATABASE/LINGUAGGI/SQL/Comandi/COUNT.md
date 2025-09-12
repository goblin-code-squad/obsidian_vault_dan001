La differenza tra `COUNT(*)` e `COUNT(nome_colonna)` è fondamentale in SQL. Te lo spiego con esempi pratici:

### Differenza chiave:
1. **`COUNT(*)`**  
   Conta **tutte le righe** della tabella, indipendentemente dai valori NULL.

2. **`COUNT(nome_colonna)`**  
   Conta solo le righe dove **la colonna specificata NON è NULL**.

---

### Esempio concreto:
Immagina questa tabella `preferenze_alimentari_italia`:

| id | cucina_italiana | cucina_cinese |
|----|-----------------|---------------|
| 1  | 5               | NULL          |
| 2  | NULL            | 3             |
| 3  | 4               | 2             |
| 4  | NULL            | NULL          |

```sql
SELECT 
    COUNT(*) AS totale_righe,
    COUNT(cucina_italiana) AS conteggio_italiana,
    COUNT(cucina_cinese) AS conteggio_cinese
FROM preferenze_alimentari_italia;
```

Risultato:
```
| totale_righe | conteggio_italiana | conteggio_cinese |
|--------------|--------------------|------------------|
| 4            | 2                  | 2                |
```

### Perché?
- `COUNT(*)` = 4 (conta tutte le righe)
- `COUNT(cucina_italiana)` = 2 (solo righe 1 e 3, le altre hanno NULL)
- `COUNT(cucina_cinese)` = 2 (solo righe 2 e 3)

---

### Applicato alla tua query:
Quando fai:
```sql
COUNT(*) - COUNT(cucina_italiana) AS "N.di non risposte"
```
Stai calcolando:  
*(Tutte le righe) - (Righe con valore non NULL) = (Righe con valore NULL)*

Nell'esempio sopra:
- Non risposte per cucina italiana: 4 - 2 = 2
- Non risposte per cucina cinese: 4 - 2 = 2

---

### Esempio reale dalla tua tabella:
Se vuoi verificare con i tuoi dati:
```sql
SELECT 
    COUNT(*) AS totale_persone,
    COUNT(cucina_italiana) AS risposte_italiana,
    COUNT(*) - COUNT(cucina_italiana) AS non_risposte_italiana
FROM preferenze_alimentari_italia;
```

Questo ti darà il numero effettivo di persone che:
- Hanno risposto (`COUNT(colonna)`)
- Non hanno risposto (`COUNT(*) - COUNT(colonna)`)

---

### Extra: come contare esplicitamente i NULL
Un altro modo equivalente è:
```sql
SELECT 
    SUM(CASE WHEN cucina_italiana IS NULL THEN 1 ELSE 0 END) AS non_risposte_italiana
FROM preferenze_alimentari_italia;
```
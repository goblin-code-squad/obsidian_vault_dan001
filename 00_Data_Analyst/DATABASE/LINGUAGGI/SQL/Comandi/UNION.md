# Sintassi di `UNION` in SQL

L'operatore `UNION` viene utilizzato per combinare i risultati di due o più query `SELECT` in un unico set di risultati, eliminando automaticamente i duplicati.

## Sintassi base

```sql
SELECT colonna1, colonna2, ...
FROM tabella1
[WHERE condizioni]
UNION
SELECT colonna1, colonna2, ...
FROM tabella2
[WHERE condizioni];
```

## Regole fondamentali

1. **Stesso numero di colonne**: Tutte le query devono avere lo stesso numero di colonne
2. **Tipi di dati compatibili**: Le colonne corrispondenti devono avere tipi di dati compatibili
3. **Ordine delle colonne**: Le colonne vengono unite in base alla loro posizione nell'elenco

## Esempio pratico

```sql
-- Unione di clienti e fornitori in un unico elenco di contatti
SELECT nome, cognome, 'Cliente' AS tipo, email
FROM clienti
WHERE attivo = 1
UNION
SELECT nome, cognome, 'Fornitore' AS tipo, email
FROM fornitori
WHERE certificato = 1;
```

## Varianti di UNION

### `UNION ALL` (mantiene i duplicati)

```sql
SELECT prodotto FROM magazzino_A
UNION ALL
SELECT prodotto FROM magazzino_B;
```

### `UNION` con ordinamento

```sql
SELECT nome, cognome FROM dipendenti
UNION
SELECT nome, cognome FROM clienti
ORDER BY cognome, nome;
```

## Esempio con la tua tabella

```sql
-- Seleziona città con preferenze per cucina italiana o cinese
SELECT citta_residenza, 'Italiana' AS cucina_preferita
FROM preferenze_alimentari_italia
WHERE cucina_italiana = 5
UNION
SELECT citta_residenza, 'Cinese' AS cucina_preferita
FROM preferenze_alimentari_italia
WHERE cucina_cinese = 5;
```

## Limitazioni

1. Non puoi usare `UNION` con `ORDER BY` nelle singole query (solo alla fine)
2. Gli alias di colonna vengono presi dalla prima query
3. Le query `UNION` non possono contenere clausole `FOR UPDATE` o `LOCK IN SHARE MODE`

Vuoi vedere un esempio più specifico applicato al tuo database?



mette le rige della seconda query dopo la prima

unisce due righe



in Sequel fa differenza tra assenza di valore o valore vuoto
fare attenzione ([[Null]])

le maiuscole hanno un valore numerico maggiore xche le vede in ASCII

```sql
SELECT nome, cognome
FROM persone
ORDER BY congnome ASC
LIMIT 3,3;
```

```sql
SELECT nome, cognome
FROM persone
ORDER BY cognome ASC
LIMIT 2,4;
```
la limitazione serve per limitare i dati in modo da non cercare tutto

si possono fare delle operazioni matematiche
somma numeri e lettere 

[[JOIN]] non funziona sempre
si possono concatenare con 
|| 

concatenando si puo fare che i due termini che si attaccano sono uguali
per esempio
AMA CIAO
oppure
AMAC IAO
se ci metto 
SELECT COUNT (
		DISTINCT nome || "uderscore" || cognome 
		)

AS per selezionare colonne dando nomi piu' umani
si potrebbe omettere MA NON FARLO (per lui dopo qualcosa se tu metti spazio qualcosaltro lo stai rinominando)

si pososno unire due query con [[UNION]]



per inserire 

[[UPDATE]]

```sql
SELECT DISTINCT nome FROM persone
```

seleziona gli UNIQUE di nome

```sql
SELECT DISTINCT nome, cognome FROM persone
```
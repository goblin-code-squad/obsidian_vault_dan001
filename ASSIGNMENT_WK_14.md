soluzione e tips
n.b. in produzione non si droppa mai lo schema, non si fa nel reale perche' si possono ricavare il dati nuovi dal timestamp, lo facciamo qui perche' e' una esercitazione

la select star e' una brutta abitudine, meglio mettere le colonne reali scrivendole perche' perdi il controllo delle colonne che importi e se qualcuno in futuro aggiunge colonne con milion di dati si spacca tutto

nelle tabelle errore la accettiamo


query importanti per creare tabella errori

```sql
select *, 'Warning: Responsabile mancante' as error_code

from openbo_landing."LT_INCARICHI_CONFERITI"

where "RESPONSABILE_DELLA_STRUTTURA_CONFERENTE" is null or "RESPONSABILE_DELLA_STRUTTURA_CONFERENTE"=''

union all
```

qui per esempio  si vede 
la select  che riprende tutte le cose che hai scelto e nel contempo crei una colonna come errore_code
poi gli da una were dove dico che quel dato e' nullo o ' '  cioe' vuoto

(a volte si crea anche una anagrafica degli errori mettendo un errore ID, che e' utile perche' puoi modificare l'anagrafica e rinominare tutti gli errori)

per creare un IDS per la data, qui facciamo tutto coi numeri.
in questo caso io non ho potuto farlo perche' avevo preso i dati come text

```sql 
(extract(year from giorno_inizio)*10000+extract(month from giorno_inizio)*100+extract(day from giorno_inizio))::int as ids_giorno
```


per esempio qui si puo' fare una "from" da una union con una select subquery
niceee

```sql
from ( 
select giorno_inizio
from tt_incarichi_collaborazione
union
select giorno_inizio
from tt_incarichi_conferiti)
```
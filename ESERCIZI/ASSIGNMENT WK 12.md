ANDREA:  
Il data-tagging e’ aggiungere delle colonne che servono per aggiungere dei dati al database, servono per il processo di  
Appena portiamo i dati nell’integration e’ da fareeee

  

Landing: le colonne le lasciamo piu’ o meno uguali ma le miglioriamo (togliamo spazi per esempio.  Nel landing non si deve fare pero’ il renaming

  

Integration: 1. Data Taggin (da fare prima possibile)

2. Fare Renaming.

Perche’ scartare quelli con importo null? Perche’ qui la cosa importante era appunto l’import

ATTENZIONE:  
Update and Delete sono transazione (quindi vengono scritte nel transaction log)  
Quelle operazioni sono “aggiunte” alla scrittura riga per riga cella per cella, ogni modifica la scrive nel transation log (serve per avere una memoria dei cambiamenti, fotografa praticamente il DB per sicurezza)  
Da evitare: ALTER TABLE (RENEAME, ADD), DELETE, COPIARE IN NUOVE TABELLE

Meglio usare Truncate che fa una sola operazione - si tratta di economia di velocita’ del database. Non cancelliamo i dati con DELETE ma selezioniamo i dati con una query e rifacciamo

  
SPRECHIAMO SPAZIO IN FAVORE DELLA VELOCITA’

DOUBLE COUNTING: il problema piu’ comune nei dbwh
  
Il database non esegue sempre la query, fa “un piano di accesso” quindi a volte fa cose diverse e bisogna forzare il piano di accesso

ATTENZIONE:

capita a volte che dicano c'e' una sorgente che e' piu' affidabile e quindi prendiamo le angrafiche da li'  epoi quelle che mancano le prendi da un altra parte

incarchi_di_collaborazione e' la sorgente piu' affidabile

usare la group by su una chiave e poi usi MAX sugli altri campi, riduce il set informativo ed in alcuni casi puo' essere un errore
siccome quando creo un'anagrafica usando questa cosa, se uso due sorgenti rischio di creare livelli aggregati misti di dati il cui risultato finale e' double counting

bisogna fare il trim del fatto e anche della dimensione

quando ho una snowflake scheme la cosa si complica ancora di piu'
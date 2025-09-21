Quando ti connetti a un database da Python, il **cursore** è l'oggetto che ti permette di eseguire comandi SQL e di navigare tra i risultati. Immaginalo come il cursore del mouse che si muove sui dati della tabella nel database.

[[FETCHALL]]

inserire codice

**Flusso di lavoro tipico:**

1. **Connessione:** Ti connetti al database.
    
2. **Creazione Cursore:** Apri un cursore da quella connessione.
    
3. **Esecuzione:** Usi il cursore per eseguire una query SQL.
    
4. **Recupero Dati:** Usi il cursore per prendere i risultati (`fetch`).
    
5. **Chiusura:** Chiudi il cursore e la connessione.
    

Python

```
import psycopg2

# 1. Connessione (i dati sono di esempio)
conn = psycopg2.connect("dbname=test user=postgres password=secret")

# 2. Creazione Cursore
cur = conn.cursor()

# 3. Esecuzione di una query SQL
cur.execute("SELECT * FROM mia_tabella;")

# 4. Recupero dei risultati
risultati = cur.fetchall() # Prende tutte le righe
for riga in risultati:
    print(riga)

# 5. Chiusura
cur.close()
conn.close()

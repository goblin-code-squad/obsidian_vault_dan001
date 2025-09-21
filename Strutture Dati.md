- **Lista (`list`):** Una collezione ordinata e modificabile di elementi. Si crea con le parentesi quadre.
    
    Python
    
    ```
    numeri = [10, 20, 30, 40]
    ```
    
- **Dizionario (`dict`):** Una collezione di coppie chiave-valore. Si crea con le parentesi graffe.
    
    Python
    
    ```
    persona = {"nome": "Anna", "eta": 25}
    ```
    
Hai ragione, ottima osservazione! Le tuple sono un elemento fondamentale e vanno assolutamente incluse. Chiedo scusa per la dimenticanza.

Integro subito la sezione sulle tuple. Puoi aggiungerla al tuo file Obsidian sotto le "Strutture Dati".

---

### Strutture Dati

- **Lista (`list`):** Una collezione ordinata e **modificabile** di elementi. Si crea con le parentesi quadre `[]`.
    
- **Dizionario (`dict`):** Una collezione di coppie chiave-valore. Si crea con le parentesi graffe `{}`.
    
- **Tupla (`tuple`):** Una collezione ordinata e **immutabile** di elementi. Una volta creata, non puoi modificarla (né aggiungere, né rimuovere, né cambiare elementi). Si crea con le parentesi tonde `()`.
    
    Python
    
    ```
    # Esempio di tupla
    coordinate = (44.4949, 11.3426) # Ad esempio, latitudine e longitudine
    
    # Puoi accedere agli elementi come in una lista
    print(coordinate[0]) # Stampa 44.4949
    
    # Ma se provi a modificarla, otterrai un errore!
    # coordinate[0] = 45.0 # Questo codice genererà un TypeError
    ```
    
    **Quando si usa?** Le tuple sono utili per dati che non devono cambiare, come le coordinate geografiche, i codici RGB di un colore o le credenziali di accesso a un database che vuoi proteggere da modifiche accidentali.
    

---

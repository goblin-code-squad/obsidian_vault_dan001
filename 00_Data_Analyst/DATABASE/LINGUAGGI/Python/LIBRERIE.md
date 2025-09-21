Una **libreria** (o modulo) è una raccolta di funzioni e codice pre-scritto da altri che puoi "importare" nel tuo script per aggiungere nuove funzionalità senza doverle scrivere da zero.

- **Importazione:** Si usa la parola chiave `import`.
    

Python

```
# Importa l'intera libreria
import math
print(math.sqrt(16)) # Uso una funzione della libreria

# Importa solo una parte specifica
from math import sqrt
print(sqrt(16)) # Ora posso usarla direttamente
```

**Librerie essenziali per te:**

- **`matplotlib`:** La libreria principale per creare grafici e visualizzazioni.
    
    - L'istogramma che hai creato usa probabilmente il sottomodulo `pyplot`.
        
        Python
        
        ```
        import matplotlib.pyplot as plt
        
        dati = [1, 2, 2, 3, 3, 3, 4, 4, 5]
        plt.hist(dati, bins=5) # Crea un istogramma
        plt.ylabel('Frequenza')
        plt.show() # Mostra il grafico
        ```
        
- **`pandas`:** Fondamentale per manipolare e analizzare dati tabulari (come i fogli di calcolo o le tabelle SQL).
    
- **`psycopg2`:** Il "driver" che permette a Python di comunicare con il tuo database PostgreSQL.
    
